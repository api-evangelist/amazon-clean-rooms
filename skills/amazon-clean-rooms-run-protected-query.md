---
generated: '2026-08-13'
method: generated
name: Run a protected query and collect the results
description: Submit a privacy-constrained SQL query against a Clean Rooms collaboration, await the asynchronous result, and read it from the configured S3 output location.
api: openapi/amazon-clean-rooms-protected-queries-api-openapi.yml
operations: [StartProtectedQuery, ListProtectedQueries]
source: >-
  operationIds verified verbatim in
  openapi/amazon-clean-rooms-protected-queries-api-openapi.yml. GetProtectedQuery
  is documented in the AWS Clean Rooms API Reference
  (llms/amazon-clean-rooms-llms.txt) and carries its own 20 req/s quota, but is
  NOT in the captured OpenAPI — it is named below as documentation, not as a spec
  operation.
---

# Run a protected query and collect the results

A protected query is **asynchronous**. `StartProtectedQuery` returns a resource in `SUBMITTED`
state; the answer arrives later, in S3, and only if the analysis rules and privacy budget allow it.

## Auth
- AWS SigV4, service `cleanrooms`. The membership must hold the `CAN_QUERY` member ability, and
  a separate member may hold `CAN_RECEIVE_RESULTS` — the runner is not necessarily the receiver.

## Steps
1. **Submit** — `StartProtectedQuery` (`POST /memberships/{membershipIdentifier}/protectedQueries`)
   with:
   - `type`: `SQL`
   - `sqlParameters.queryString`: the SQL (or reference an approved analysis template)
   - `resultConfiguration.outputConfiguration.s3`: `{bucket, keyPrefix, resultFormat}`
   Capture `protectedQuery.id` and the initial `status` (`SUBMITTED`).
2. **Await completion.** Two options, in order of preference:
   - **Event-driven (preferred):** subscribe to EventBridge `source: aws.cleanrooms` with
     `detail-type` in `["Protected Query Succeeded", "Protected Query Failed",
     "Protected Query Cancelled", "Protected Query Timed Out"]`. See
     `asyncapi/amazon-clean-rooms-events.yml`.
   - **Polling:** `GetProtectedQuery` (documented in the API Reference; quota 20 req/s — the highest
     read quota in the service, deliberately sized for this poll). Poll with backoff; a query may run
     up to the 24-hour timeout.
3. **Enumerate history** — `ListProtectedQueries`
   (`GET /memberships/{membershipIdentifier}/protectedQueries`) filtered by `status`, paged with
   `nextToken` / `maxResults` (max 100). Results are sorted most-recent first.
4. **Read the results** from the S3 location in `resultConfiguration`. The API returns metadata and
   statistics, never the rows.

## Terminal states
`SUCCESS`, `FAILED`, `CANCELLED`, `TIMED_OUT`. Intermediate: `SUBMITTED`, `STARTED`, `CANCELLING`.

## Constraints worth planning around
- Concurrent SQL queries per account: 5 in us-east-1, 2 elsewhere (adjustable).
- Concurrent ongoing queries per membership: 5, **not** adjustable.
- Query text length: 90 KB (500 KB on the Spark analytics engine).
- Query run time: 24 hours before timeout.
- Configured tables per protected query: 15 (adjustable).

## Privacy behaviour that changes results
- Analysis rules can reject the query outright, or silently remove result rows that fail a minimum
  aggregation threshold.
- With differential privacy enabled, noise is added and the query consumes epsilon from the privacy
  budget. `PreviewPrivacyImpact` (documented in the API Reference) estimates how many aggregations
  remain before submitting.

## Cost
Compute is billed at $2.00 per CRPU-hour (us-east-1), per-second with a 60-second minimum for Spark
SQL, 32 CRPUs allocated by default — and $4.00 per CRPU-hour when differential privacy is applied.
The collaboration's payment configuration decides *which member* is billed.
See `plans/amazon-clean-rooms-plans-pricing.yml`.

## Errors
- `ValidationException` (400) — SQL that violates the analysis rule, or a column outside the allowlist.
- `AccessDeniedException` (403) — membership lacks `CAN_QUERY`, or the service role cannot write the
  S3 output prefix.
- `ThrottlingException` (**400**, not 429, no `Retry-After`) — back off exponentially.
- **No idempotency key.** A retried `StartProtectedQuery` runs — and bills — a second query. Confirm
  with `ListProtectedQueries` before resubmitting. See `conventions/amazon-clean-rooms-conventions.yml`.
