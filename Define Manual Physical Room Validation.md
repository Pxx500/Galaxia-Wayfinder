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

# Define Manual Physical Room Validation

## Current Scope

Deferred on 2026-09-16 under [[Consolidate Physical Station Architecture]]. Keep the existing room implementation and validation lifecycle for the current PR integration. The earlier manual-only lifecycle below is historical accepted direction, not a requirement to implement during this merge. Surface tracing, interval traversal and room-separation proposals are not selected. The unresolved questions remain unresolved.

## Question

How is an arbitrary-shaped Physical Station Room manually validated, and which later construction changes invalidate that approval without automatically discovering rooms again?

## Earlier Accepted Direction

Owner discussion on 2026-09-13, after the initial physical Station rework:

- Creating or restoring a valid room requires the player to click Validate. Room discovery and revalidation are not automatically repeated after every construction change.
- The owner requested immediate invalidation after destruction of a required room boundary and manual Validate after repair. The assistant interpreted this as revoking geometric approval. The later shared-wall example exposed uncertainty about the exact consequences, especially pressure. Do not interpret it as approval for automatic atmosphere deletion after every wall change.
- Room geometry is independent of Station construction connectivity. Keeping the last confirmed device-connectivity state during a thread rebuild does not postpone the separately accepted immediate room invalidation.
- Room shape is not restricted to a box, a rectangle or another authored template.
- A valid airlock counts as a geometric boundary regardless of whether its door is currently open. Door openness affects pressure and does not invalidate geometry or a running geometry check. Destruction or structural failure of the airlock can invalidate the boundary.
- Multiple controllers serving the same physical enclosure must not duplicate room state, volume or costs. Controller changes must not create independent overlapping copies of one room.

## Accepted Search Baseline

The owner accepted bounded room discovery after the Internet research:

- Start in the intended interior adjacent to the selected controller and traverse six-face-connected available space until stopped by recognized sealing boundaries.
- Bound the search using the complete construction relevant to validation, expanded with an exterior margin. This is a search bound, not a prescribed room shape.
- Reaching a confirmed exterior margin proves an opening to the exterior. Exhausting the reachable interior without such an opening confirms enclosure only when the required geometry data is complete.
- Missing or unloaded data is unknown, not automatically empty or exterior. A truncated or exhausted work budget is not proof of a valid room.
- Use cached geometry for the computation. Multithreaded computation must not read live Minecraft world or Tile Entity state. The immutable-input and result-freshness contract still needs its final policy in [[Define Physical Room Validation Recovery]].

## Boundary Data Direction

Discussed to support fast invalidation. The behavioral requirement is accepted, while exact representation remains a design choice:

- Validation records which construction boundaries the room depends on. A reverse relation from boundary position to dependent rooms enables direct invalidation without searching the Station after each removal.
- A shared wall can belong to multiple rooms. One room may touch several faces of the same block, such as a pillar. Counting distinct room IDs is not equivalent to counting covered faces.
- Side-aware room relations may be retained where needed for airlock or boundary classification. They need not be represented as full records on every construction block or as new Tile Entities.
- The earlier single exterior-wall bit is not a sufficient authority for room classification or freshness. The current manual-invalidating contract does not require proving actual exterior exposure every time a certified boundary is destroyed.

## Open Decisions

1. Which placements or replacements inside an already valid room invalidate it? A new sealing partition may divide the space without removing an old boundary. Ordinary furniture or machinery should not accidentally imply the same policy without a decision.
2. After shared-wall removal, both dependent rooms can become invalid, but the ownership and environmental-state treatment of the space discovered by a later Validate still needs definition. Do not automatically merge and approve rooms merely because a wall vanished.
3. If several existing controllers validate the same space, what are the user-visible ownership and configuration rules beyond the settled requirement that the physical room is not duplicated?
4. The owner challenged the interpretation of immediate invalidation: removing a shared internal wall and removing an exterior wall need not have the same pressure consequence. The assistant interpreted required-boundary destruction as revoking geometric approval, not proving venting. Confirm this interpretation and resolve pressure consequences in [[Define Airlock Space Classification]] before implementation. Do not treat all wall changes as immediate atmosphere deletion.

## Recommendation Awaiting Owner Approval

Distinguish changes to sealing geometry from ordinary non-sealing contents. Invalidate affected room approvals for topology-changing partitions or boundary replacements, without performing automatic revalidation. Do not treat this recommendation as an accepted requirement yet.

## Research Evidence

[[Voxel Room Detection Algorithms Research]] establishes six-face connected-component methods and their assumptions. [[Voxel Game Room Validation Research]] supplies an archived Space Engineers precedent for finite grid bounds and face-based airtightness. These sources do not select Galaxia gameplay policy or guarantee a speedup.

## Potential Optimization: Empty-Interval Traversal

Status: retained as a candidate, not required for the first implementation. Owner requested this record on 2026-09-13.

- Represent uninterrupted empty stretches along one axis as intervals and search their connections instead of placing every empty voxel in the traversal queue. Overlapping intervals in adjacent rows or slices preserve six-face connectivity.
- An ordered index of sealing obstacles on each line could identify the entire gap between obstacles without reading every empty coordinate. The expected benefit depends on avoiding per-voxel discovery of those gaps, not merely renaming a voxel loop as a batch.
- Index construction and maintenance, interval fragmentation, boundary extraction and temporary memory all contribute to cost. Large uniform spaces may benefit, while highly fragmented layouts may not.
- A missing obstacle entry proves a gap only when the input data is complete. A gap is not automatically exterior. It must connect to the confirmed exterior margin. Thin walls and one-voxel openings must retain exact behavior.
- This is the scanline or span-traversal family of ideas, not a commitment to a particular library, index, axis arrangement or complexity claim. It does not resolve the separate open pressure and invalidation policies.

## Implementation and Measurement Direction

The owner emphasized moving toward a working implementation, testing representative cases and optimizing measured weaknesses rather than indefinitely designing speculative shortcuts. Establish correct baseline behavior, measure its costs, and compare optional optimizations against that baseline. No unmeasured speedup or mandatory interval representation is accepted.

This instruction records the development approach. It does not silently resolve open gameplay decisions or authorize immediate implementation merely because this candidate has been documented.

## Superseded Proposals

- Continuously discovering every enclosed space after every block change.
- Treating a single exterior-wall flag or local air-neighbor count as a complete room model.
- Requiring a persistent global map of every air voxel or a section-component graph before manual validation can work.

The initial code commit predates this manual-validation design. This ticket is not an implementation-completion claim or a deferred implementation checklist.

## Discussion Checkpoint

On 2026-09-13, the owner remained uncertain after proposing a search from a destroyed wall. The proposed automatic leak check is recorded, with its unaccepted status, in [[Define Airlock Space Classification]]. The owner asked to save the discussion and report completion. Room validity versus actual depressurization remains open. No further implementation or automatic-check exception was approved by that request.
