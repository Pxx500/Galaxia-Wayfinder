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

# Physical Room Validation Recovery


## Scope

Deferred under [[Consolidate Physical Station Architecture]]. Retain the existing room lifecycle. Manual-approval persistence and asynchronous recovery remain undecided, not prerequisites for the earlier Station integration.

## Constraints

- Rebuild derived connectivity paths and wall markers at startup rather than persisting optimization caches. This does not discard Station identity or room environmental state.
- The earlier manual-validation direction requires player action for creation and revalidation, with immediate geometric invalidation after required-boundary destruction.
- Cached geometry may support background validation. Airlock structure affects geometry, while door openness affects pressure separately.
- Device-connectivity recalculation retains the last confirmed service state until disconnection is confirmed. That rule does not retain room approval after known boundary destruction.
- Missing geometry is not proof of exterior. Chunk unload is not destruction.

## Open Decisions

1. Does startup automatically reconstruct and check previously approved rooms, or require Validate again?
2. What room availability and pressure state applies while chunks or initial verification are incomplete?
3. Does relevant construction change reject a running validation and require another click, or restart it within the original request?
4. Which changes make a result obsolete? A whole-Station revision is conservative but can reject work after unrelated changes. More precise dependencies require additional bookkeeping.

## Unaccepted Recommendation

Persist approval intent rather than optimization caches. Reconstruct previously approved rooms at startup when data becomes available, but require Validate for new rooms and rooms invalidated by construction. This would be an explicit exception to manual checks and is not accepted.

Rejecting stale validation results is also proposed, not a selected user-visible recovery policy. Worker scheduling and duplicate-click handling can be derived after that policy is settled.

## Provenance

Discussed on 2026-09-13 and deferred on 2026-09-16. Startup cache rebuilding predates manual room approval and does not override it.

## Gameplay Flow

Under the earlier manual-validation direction, the player validates new rooms and revalidates rooms after required boundary destruction. Whether previously approved rooms recover automatically after startup remains open. The current integration retains the existing room lifecycle.
