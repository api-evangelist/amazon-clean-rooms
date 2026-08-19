---
generated: '2026-08-13'
method: generated
name: Create a Clean Rooms collaboration and join it
description: Stand up a multi-party AWS Clean Rooms collaboration, invite partner accounts, and create the creator's own membership so work can begin.
api: openapi/amazon-clean-rooms-collaborations-api-openapi.yml
apis:
  - openapi/amazon-clean-rooms-collaborations-api-openapi.yml
  - openapi/amazon-clean-rooms-memberships-api-openapi.yml
operations: [CreateCollaboration, GetCollaboration, ListCollaborations, CreateMembership, ListMemberships]
source: >-
  operationIds verified verbatim in
  openapi/amazon-clean-rooms-collaborations-api-openapi.yml and
  openapi/amazon-clean-rooms-memberships-api-openapi.yml. Cross-cutting rules
  from conventions/amazon-clean-rooms-conventions.yml,
  errors/amazon-clean-rooms-error-codes.yml and
  rate-limits/amazon-clean-rooms-rate-limits.yml.
---

# Create a Clean Rooms collaboration and join it

A collaboration is the shared environment. Creating it does **not** put you in it — the creator
must also create a membership, and so must every invited partner, before anyone can configure
tables or run a query.

## Auth
- AWS Signature Version 4 against `https://cleanrooms.{region}.amazonaws.com` with the service
  name `cleanrooms`. See `authentication/amazon-clean-rooms-authentication.yml`.
- The calling principal needs the `cleanrooms:CreateCollaboration` and
  `cleanrooms:CreateMembership` IAM permissions (covered by `AWSCleanRoomsFullAccess`).

## Before you start
- **There is no idempotency key.** A retried `CreateCollaboration` creates a *second*
  collaboration. Before retrying a failed create, call `ListCollaborations` and match on `name`.
  See `conventions/amazon-clean-rooms-conventions.yml`.
- Region is part of the SigV4 credential scope. Sign for the same Region you are calling.

## Steps
1. **Create the collaboration** — `CreateCollaboration` (`POST /collaborations`) with `name`,
   `description`, `creatorDisplayName`, `creatorMemberAbilities` (e.g. `["CAN_QUERY"]`),
   `queryLogStatus` (`ENABLED` to keep an audit trail of every query run), and `members[]` —
   each entry an `accountId`, `displayName` and `memberAbilities`. Capture `collaboration.id`
   and `collaboration.arn` from the response.
2. **Confirm the shape you got** — `GetCollaboration` (`GET /collaborations/{collaborationIdentifier}`)
   with the id from step 1. Verify `queryLogStatus` and `creatorAccountId` before inviting anyone
   to act on it. Members invited per collaboration defaults to 5 (adjustable).
3. **Create your own membership** — `CreateMembership` (`POST /memberships`) with
   `collaborationIdentifier` = the collaboration id and `queryLogStatus`. This is the resource that
   every later query, job, table association and privacy budget hangs off. Capture `membership.id`.
4. **Verify** — `ListMemberships` (`GET /memberships`) filtered by `status=ACTIVE` and confirm the
   new membership appears with the expected `collaborationId`.

## Partner side
Each invited account performs step 3 for itself. Until a partner creates its membership, its
`memberStatus` on the collaboration is `INVITED`, not `ACTIVE`, and it cannot associate tables.

## Errors
- `ValidationException` (400) — inspect `fieldList[]` for the offending field.
- `AccessDeniedException` (403) — missing `cleanrooms:*` permission on the calling principal.
- `ThrottlingException` (**400**, not 429) — back off exponentially. Default quota is 5 req/s per
  operation per Region per account. See `errors/amazon-clean-rooms-error-codes.yml`.

## Events
Subscribe to the EventBridge `Collaboration Created`, `Invited To Collaboration` and
`Membership Created` detail-types on `source: aws.cleanrooms` to drive the flow reactively rather
than polling. See `asyncapi/amazon-clean-rooms-events.yml`.

## Teardown
`DeleteCollaboration` (`DELETE /collaborations/{collaborationIdentifier}`) requires that the
collaboration have no active memberships first.
