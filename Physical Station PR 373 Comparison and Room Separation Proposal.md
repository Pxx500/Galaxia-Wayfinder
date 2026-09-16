---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Physical Station PR 373 Comparison and Room Separation Proposal

Source: Owner conversation and read-only review of https://github.com/GTNewHorizons/Galaxia/pull/373
Imported: 2026-09-16

## Source Snapshot

Reviewed on 2026-09-16 during [[Consolidate Physical Station Architecture]]. The snapshot below preserves the earlier conversation. That owning decision now records the selected scope and authorization to review and merge the PR if ready. Earlier statements that no merge was authorized describe the snapshot's original time.

This is discussion intake, not a new accepted architecture or an implementation plan. The PR review and subsequent room-separation proposal had been discussed in chat but had not been recorded in the Vault before this checkpoint.

### Existing Decisions Remain Settled

The existing decision note Resolve Physical Station Controller Succession already records construction membership outside individual block Tile Entities, updated on placement and removal, with controllers adopting the identity of connected construction. Define Physical Station Change Tracking owns the accepted runtime path markers, compact coordinates, batching, startup cache reconstruction and debug overlay requirements.

The owner objected to repeatedly explaining that ordinary construction blocks do not need Tile Entities. This was already understood and recorded. Do not present it as a new proposal or reopen it as a decision. Explain differences from the PR against that established baseline.

### Reviewed Code, Not New Requirements

Reviewed PR head: `ecdba756e3f19705ca890b903d8a1c42afbf9151`. This is a pinned historical inspection, not a claim about later PR revisions. Local review checkout: `C:/Users/Pxx500/Documents/GitHub/Galaxia/worktrees/review-physical-stations-373`.

- Ordinary construction blocks report placement and destruction through the GregTech machine-update mechanism. They do not immediately register their position into a Station-owned membership map by inspecting their neighbors.
- Controllers discover and retain their own geometry. Room, Power Room and Dock behaviors select allowed boundaries and supported devices. Enclosed geometry uses boundary discovery and bounded interior traversal, with existing bitsets, coarse 4 by 4 by 4 cells and fast revalidation. These optimizations predate the PR diff.
- A formed room controller registers its coordinates with each discovered airlock. The airlock stores at most two controller positions. It does not discover the neighboring rooms itself, and those list slots do not establish physical side identity.
- Controllers use airlock registrations to discover a shared StationGraph. The main controller owns this graph. A Station asset points to the main controller. Individual controllers hold room geometry, oxygen and environmental devices.
- Door state does not determine Station membership. Controllers separately traverse open airlock connections to calculate a shared sealed/unsealed result. An airlock with fewer than two registered controllers is treated as external. This is not a geometric proof of exterior access.
- The PR develops airlock construction, orientation, collision, redstone, proximity controls and GUI. The assistant recommended retaining these capabilities while changing Station membership and room ownership. That recommendation has not been accepted as an integration plan.
- Code inspection found an auto-seal setting without a corresponding leak-closing implementation, and a secondary-controller boot path that can leave backingStation absent and skip oxygen updates. These were code-path findings, not in-game reproductions.

The earlier local implementation is separate: branch `station-construction-identity`, commit `fe27e3e541f0d6013b099e1d2a697129b3e624a4`. It introduced construction membership and shared room ownership before the later manual-validation and optimization discussions. Do not conflate the PR, that implementation and the proposed design.

### Owner's Latest Proposal

The owner suggested separate rooms whose ordinary construction does not connect directly. Rooms would connect through scaffolding that does not propagate room checking, or through airlock blocks that count toward validation but do not propagate checking to the other side.

The assistant interpreted this as independently enclosed rooms with no shared walls or ceilings, and asked whether that interpretation was correct. The owner has not confirmed that detail. Do not record a ban on shared walls or ceilings as accepted.

The owner then paused that design discussion to understand the existing PR architecture and expressed uncertainty about whether its airlock responsibilities were desirable. The current conversation is about understanding and comparing ownership and data flow, not approval to implement the separation proposal.

### Further Comparison and Boundary-Tracing Proposal

The owner reaffirmed interest in Station-wide construction membership and connectivity paths for functional devices both inside and outside rooms. The assistant recommended this model for device connectivity while retaining a separate room-validation capability. Paths preserve evidence of connectivity between already registered functional points, rather than replacing initial device discovery. No measured speedup was claimed.

The owner then requested a short comparison to seek a combined architecture, and proposed detecting rooms by following the wall together with immediately adjacent interior air instead of exploring the entire air volume. This could avoid requiring separately built room shells. The earlier interpretation that shared walls and ceilings would be forbidden remains unconfirmed.

This boundary-tracing idea is a candidate, not an accepted replacement algorithm. The assistant identified a correctness requirement: a traversal can follow the rim of a hole onto the outside surface while still observing wall-adjacent air. Completing that traversal alone does not prove enclosed air. Any exact surface-based method must distinguish the air-facing sides and correctly classify enclosure, including corners and separate internal surfaces. Potential surface-area savings are not measured, and room volume and position-membership queries remain part of evaluating the representation.

### Outstanding Distinctions

- Construction membership, room geometry and air connectivity remain separate questions.
- Stopping a shell traversal at an airlock is part of the new proposal, not an already implemented PR behavior.
- Boundary invalidation versus actual depressurization remains unresolved. Missing room registration must not silently become proof of exterior in the proposed model.
- No new implementation, merge, publication or acceptance of the assistant's preservation recommendations was authorized by this discussion.

[[Sources]]
