---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by:
  - "[[Resolve Physical Station Controller Succession]]"
  - "[[Define Transport Endpoint Identity and Registration]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Physical Station Merge Contract


## Question

How should joining independently identified Physical Stations handle surviving identity, ownership, controllers and logistics references?

## Deferred Direction

Joining construction with different Station IDs must not silently merge ownership or select an arbitrary identity. Placing a connecting block is already a manual action. No separate command, confirmation or explicit merge interaction is accepted.

This is a low-priority edge case and must not block current work. If revisited, decide identity, ownership and reference handling together. Station-local endpoint groups are scoped by Station identity, while endpoint identities and shared Routing Names remain distinct. Controller succession and splitting an existing Station are already settled elsewhere.

## Historical Implementation Evidence

Read-only inspection of master `b1e42710` on 2026-09-16 found airlock-based membership in `TileStation.attemptBoot` and `StationGraph.connectPiece/rebuild`. That is not a construction-based merge of independent Station assets and routing references.

The separate `station-construction-identity` rework guarded conflicting ownership:

- `Station.blockAdded` claimed a new block only when its six neighbors identified exactly one Station. With two IDs, the block stayed placed but unclaimed, without a notification.
- `claimConnectedConstruction` stopped before applying additions on encountering another Station.
- A controller touching different Station identities refused boot.

Paths are under `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/station/`. These inspected guards are not an accepted final merge design or evidence that the rework is integrated into master.

## Unselected Behavior

Rejecting placement, choosing a surviving Station, rewriting references, automatic merging and a separate confirmation were not accepted. Room discovery and optimization remain separately deferred.

## Provenance

Owner direction on 2026-09-16.

## Related Topics

- [[Resolve Physical Station Controller Succession]]
- [[Define Transport Endpoint Identity and Registration]]
