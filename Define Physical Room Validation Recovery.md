---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by:
  - "[[Define Physical Station Room Ownership]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Physical Room Validation Recovery

## Current Scope

Deferred on 2026-09-16 under [[Consolidate Physical Station Architecture]]. The current PR integration retains the existing room lifecycle. A new manual-approval persistence contract or asynchronous validation recovery policy is not required for that merge. The earlier questions below remain open for a later room-design discussion.

## Question

How do manual room approvals survive startup, incomplete chunk data and construction changes while background validation is running?

## Accepted Constraints

- The owner chose rebuilding derived connectivity paths and wall markers at startup rather than persisting those optimization caches.
- Station identity and room environmental state are not discarded by that cache decision.
- The owner later required room creation and revalidation to be manual, with immediate invalidation of known boundary destruction.
- Geometry validation can use cached Station data rather than live world access. Airlock presence and structural correctness matter to geometry, while door openness affects pressure separately.
- During ordinary device-connectivity recalculation, retain the last confirmed service state until actual disconnection is confirmed. This is not an accepted rule to retain room validity after known boundary destruction.

## Open Decisions

1. After a server restart, are previously approved rooms automatically reconstructed and checked, or must players click Validate again? The cache-rebuild decision alone did not resolve this later interaction with manual room approval.
2. What room availability and pressure state applies while required chunks are missing or initial verification is incomplete? Unload is not destruction, and missing geometry is not proof of exterior.
3. When relevant construction changes during background validation, should the job reject its result and request another click, or automatically restart within the player's original request? Rejection was proposed but not explicitly accepted.
4. Which changes invalidate the result? Whole-Station revisions are simple but can discard a room check because of unrelated distant work. More precise dependencies add bookkeeping. This is an implementation choice constrained by the selected user-visible policy, not a mandate for a new versioning service.

## Recommendation Awaiting Owner Approval

Persist the player's room approval intent, not the derived optimization cache. On startup, reconstruct previously approved rooms automatically when data is available. Discovering new rooms and restoring rooms explicitly invalidated by construction changes would still require Validate. This is a proposed explicit exception to manual checks, not an existing accepted rule.

For an in-progress manual validation, prefer rejecting an obsolete result rather than accepting stale geometry. Queue limits, duplicate-click handling and worker scheduling can be derived during implementation after the observable policy is settled.

## Provenance

Owner discussion on 2026-09-13. This ticket exposes the overlap between earlier startup cache rebuilding and the later manual-validation decision. It intentionally leaves the overlap unresolved rather than interpreting one rule as silent approval to override the other.
