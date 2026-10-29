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

# Manual Physical Room Validation


## Scope

Deferred under [[Consolidate Physical Station Architecture]]. Retain the existing room implementation and validation lifecycle. The earlier manual-only direction below is not a requirement for the current integration. Surface tracing, interval traversal and room-separation proposals remain unselected.

## Retained Design Direction

- Creating or restoring a room requires the player to click Validate rather than automatic rediscovery after every construction change.
- Destruction of a required boundary immediately invalidates geometric approval. This does not itself prove venting or authorize atmosphere deletion.
- Room geometry is independent of Station construction connectivity. Retaining device service during connectivity recalculation does not postpone room invalidation.
- Rooms may have arbitrary shapes.
- A structurally valid airlock is a geometric boundary regardless of door state. Openness affects pressure. Destruction or structural failure may invalidate the boundary.
- Multiple controllers must not duplicate one enclosure's state, volume or costs.

## Accepted Search Baseline

Six-face discovery starts in the intended interior adjacent to the selected controller. Recognized sealing boundaries stop traversal. The complete relevant construction, expanded with an exterior margin, bounds the search rather than prescribing room shape.

Reaching a confirmed exterior margin proves an opening. Exhausting reachable interior confirms enclosure only with complete geometry data. Missing or unloaded data is unknown, and an exhausted work budget does not prove enclosure.

Computation uses cached geometry. Background work must not read live Minecraft world or Tile Entity state. Input immutability and result freshness remain under [[Define Physical Room Validation Recovery]].

Validation records boundary dependencies so removal can invalidate affected rooms directly. Shared walls may serve several rooms, and a room may touch several faces of one block. Exact storage and side-aware relations remain design choices. A single exterior-wall bit is insufficient.

## Open Decisions

1. Which placements or replacements invalidate approval? New sealing partitions can divide space, but ordinary furniture and machinery need not follow the same rule.
2. After shared-wall removal, how does later Validate assign ownership and configuration without automatically merging and approving rooms?
3. How do multiple controllers validating the same space expose ownership and configuration to the player?
4. How does geometric invalidation affect pressure when no exterior route is known? [[Define Airlock Space Classification]] owns unresolved-side behavior. [[Define Celestial Capability Rules]] settles equalization of sealed joined rooms and proven vacuum breaches, not every invalidation case.

Distinguishing topology-changing construction from ordinary contents is a recommendation, not a settled invalidation policy.

## Deferred Optimization

Empty-interval traversal is a candidate, not a requirement. Connected spans could avoid per-voxel queues if a complete sealing-obstacle index finds gaps without visiting every empty position. Index maintenance, fragmented layouts, boundary extraction and temporary memory must be measured. Thin walls and one-voxel openings must remain exact.

Establish a correct baseline and measure representative workloads before selecting an optimization. No speedup, persistent global air-voxel map, section-component graph or mandatory interval representation is accepted.

## Provenance

Discussed on 2026-09-13 and deferred on 2026-09-16. [[Voxel Room Detection Algorithms Research]] and [[Voxel Game Room Validation Research]] provide algorithm evidence, not gameplay policy. [[Define Airlock Space Classification]] owns the unapproved damage-origin leak-search candidate.

## Gameplay Flow

The earlier direction has the player build an enclosed space and select Validate at its controller. Destroying a required boundary invalidates its geometric approval, but does not by itself prove a leak. This manual-only lifecycle is deferred, so the current integration retains the existing room lifecycle.
