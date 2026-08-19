---
generated: '2026-08-13'
method: generated
name: Configure a table for a Clean Rooms collaboration
description: Wrap an underlying AWS Glue, Athena or Snowflake table as a Clean Rooms configured table with an explicit column allowlist so partners can query it without seeing raw data.
api: openapi/amazon-clean-rooms-configured-tables-api-openapi.yml
operations: [CreateConfiguredTable, ListConfiguredTables]
source: >-
  operationIds verified verbatim in
  openapi/amazon-clean-rooms-configured-tables-api-openapi.yml. Analysis-rule and
  association operations referenced below are documented in the AWS Clean Rooms
  API Reference (llms/amazon-clean-rooms-llms.txt) but are NOT in the captured
  OpenAPI — they are named as documentation, not as spec operations.
---

# Configure a table for a Clean Rooms collaboration

A configured table is the privacy boundary around your own data. It names the underlying table and
the **only** columns that may ever be used, before any partner can reference it.

## Auth
- AWS SigV4, service `cleanrooms`. The principal needs `cleanrooms:CreateConfiguredTable` and read
  access to the underlying catalog (Glue/Athena/Snowflake connection secret).

## Steps
1. **Create the configured table** — `CreateConfiguredTable` (`POST /configuredTables`) with:
   - `name` and `description`
   - `tableReference` — e.g. `{"glue": {"databaseName": "...", "tableName": "..."}}`
   - `allowedColumns[]` — the explicit allowlist. Default quota is 100 columns per configured table.
   - `analysisMethod` — `DIRECT_QUERY`
   Capture `configuredTable.id` and `configuredTable.arn`.
2. **Verify** — `ListConfiguredTables` (`GET /configuredTables`) and confirm the new table appears
   with the expected `analysisMethod` and `analysisRuleTypes`. Page with `nextToken` / `maxResults`
   (max 100).

## What comes next (documented, not in the captured spec)
The captured OpenAPI in this repo covers create/list only. The full flow published in the AWS Clean
Rooms API Reference continues with:
- `CreateConfiguredTableAnalysisRule` — attach an `AGGREGATION`, `LIST` or `CUSTOM` rule constraining
  how the table may be queried (join columns, aggregate columns, minimum aggregation thresholds).
- `CreateConfiguredTableAssociation` — bring the configured table into one specific collaboration
  under a membership.
- `CreateConfiguredTableAssociationAnalysisRule` — the association-side constraints.
Only after association does the table appear to partners as a `Schema` in the collaboration.

## Constraints worth planning around
- Configured tables per account: 250 (adjustable). Table associations per membership: 100.
- Analysis rule JSON size: 100 KB, **not** adjustable.
- Complex nested types (`ARRAY`, `MAP`, `STRUCT`) are not supported for Amazon Athena data sources.

## Errors
- `ValidationException` (400) with `fieldList[]` — most often an `allowedColumns` entry that does
  not exist in the underlying table.
- `AccessDeniedException` (403) — the Clean Rooms service role cannot read the underlying table.
- No idempotency key: a retried create makes a second configured table. List and match on `name`
  before retrying. See `conventions/amazon-clean-rooms-conventions.yml`.

## Events
`Configured Table Association Created` / `Updated` / `Deleted` and the association analysis-rule
events are published to EventBridge on `source: aws.cleanrooms`.
See `asyncapi/amazon-clean-rooms-events.yml`.
