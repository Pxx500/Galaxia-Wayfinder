---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by:
  - "[[Resolve Physical Station Controller Succession]]"
  - "[[Define Physical Station Room Ownership]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/grilling
---

# Define Physical Station Change Tracking

## Question

How should Physical Stations avoid unnecessary device-connectivity recomputation while keeping construction data compact and inspectable?

## Provenance

Owner discussion following commit `fe27e3e5` in the local Galaxia session, recorded on 2026-09-13. The owner requested recording the decisions in Wayfinder before further implementation. This ticket records design intent, not completed optimization work.

## Resolution

Accepted as the working direction for device connectivity, compact construction data and thread debugging. Room-validation lifecycle and airlock classification now have separate open owning tickets. This resolved status does not mean the entire Station validation design is finished. Measure representative workloads before claiming a performance gain.

On 2026-09-16, [[Consolidate Physical Station Architecture]] retained this construction-connectivity direction while deferring the room-redesign tickets. Do not read the earlier room-approval references below as requirements for the current airlock PR integration.

### Connectivity Witness

- Build one connected, branching network of actual construction paths joining all required functional points, including the main controller. The conversational name is the invisible thread.
- Every functional object registered with the Station must participate in path generation. Structural blocks can carry paths without becoming required destinations themselves.
- Prefer short connections heuristically. A new destination can join the nearest reachable part of the existing connected path network, not only another machine. Independent nearest-neighbor pairs must not leave disconnected groups.
- Store only a path-membership marker at construction positions. Persistent parent pointers, per-device route records and incremental tree repair are not required.
- Removing an unmarked structural block leaves the selected functional connections intact. Removing a marked block invalidates the witness and triggers full connectivity and path-marker recomputation.
- A cut witness means recomputation is required, not that devices are necessarily disconnected. Another valid route may exist.
- A disconnected fragment retaining its Station ID does not gain service merely from that ID. Adding a functional object there must establish connectivity before enabling its Station-dependent functions.
- Device registration changes, main-controller changes and reconnection of inactive construction must update or invalidate the witness as appropriate.
- Attaching a new functional point can extend the existing witness. Obsolete path marks after device removal may remain until a later rebuild because they only cause extra invalidations, not false connectivity.

### Room Boundary Evidence

Room rules are owned by [[Define Manual Physical Room Validation]] and [[Define Airlock Space Classification]]. The earlier proposal that a single exterior-wall bit could independently resolve sealing was superseded by the manual-validation discussion. A connectivity witness does not prove room sealing, and an unknown airlock side is not automatically exterior.

### Targeted Updates

- Track device connectivity, room approval and pressure, and functional-device changes separately. Avoid rebuilding unrelated state for every block event. This is not permission to automatically revalidate rooms.
- Coalesce a series of changes into one pending update. An explosion must not cause a full recomputation for every affected block.
- Preserve the last confirmed service-connectivity state while recomputation is pending. Do not interrupt energy or inventory access merely because a selected path was cut. Withdraw services only after actual disconnection is confirmed. The owner accepts the short delay in withdrawing services in exchange for avoiding transient outages when another route exists.
- Room-boundary invalidation, changes inside rooms and pressure propagation are addressed by the open room tickets. Removing a shared boundary must not silently create a newly approved merged room.
- A direct spatial ownership index is an optional profiling-driven improvement, not a requirement to create another persistent Station identity store.

### Compact Construction Coordinates

- Group recorded construction positions by 16 by 16 by 16 chunk sections. Store the section position once and use local coordinates within that section.
- The accepted simple representation uses 12 coordinate bits, four per axis, inside a 16-bit entry. The remaining four bits can hold small markers such as path membership. Specific room flags must follow the current room design, not the superseded single-bit exterior test.
- Do not repeat Station identity in every entry when ownership is already expressed by the containing collection. Richer information applies only to the positions that need it, rather than mandatory empty fields on every block.
- Omitting a false field does not automatically save a bit. Collection membership can encode classification, while packed flags can be cheaper than separate coordinate lists. The later accepted section-local representation is the preferred baseline, not a requirement to duplicate positions into several lists.
- The estimate of approximately 200 kB for 100,000 two-byte entries excludes section headers, room associations, functional data, container overhead and Java heap overhead. It is not a measured file size or RAM claim.
- Additional room references and face associations need separate storage where present. Two bytes per construction entry is not a promise that all Station validation data fits in two bytes per block. The later 1 to 3 MB estimate for a sample Station was also illustrative and excluded room-interior representation, worker snapshots, Minecraft world data and inventories.

### Derived Data Lifecycle

- Do not persist the connectivity witness or derived wall markers. Recompute them when the world or server starts, rather than trusting an old optimization cache from disk.
- This does not remove persistent Station identity or room environmental state. Rebuilding derived data at startup reduces stale-cache risk but does not replace correct handling of live world changes.
- Startup reconstruction must account for unloaded chunks. Its interaction with later manual room validation is unresolved in [[Define Physical Room Validation Recovery]]. Do not infer that every room must be manually revalidated after a restart or that every room can automatically resume without checking.

### In-World Thread Debug View

- Provide a switchable in-world debug visualization that highlights all construction blocks marked as part of the selected Station's connectivity witness.
- The owner must be able to enter the world, enable this debug view and inspect the actual thread layout and branches on the physical Station.
- Visualize the same path-membership data used by connectivity invalidation, not a separately generated approximate network.
- This is a diagnostic overlay, not a modification of physical blocks. Exact activation controls and rendering choices remain implementation details. The visualization has not yet been implemented.

## Rejected or Superseded Directions

- Maintaining parent pointers and repairing individual tree branches was unnecessary complexity for the owner's intended marker-and-rebuild design.
- Connecting every functional destination independently to the main controller is not required. Destinations may connect to any reachable part of the existing connected witness.
- Marking a spanning tree of every structural block would remove the intended benefit. The witness connects required functional points through a subset of construction.
- A coordinate slice containing other blocks is not proof of connectivity. Actual construction paths provide that proof.
- A bounded local connectivity search, such as a small cube around a removed block, was discussed earlier. It is not an additional mandatory layer on top of the accepted witness scheme.
- A geometrically awkward Station is a performance workload, not inherently player abuse. Missing placement or destruction callbacks are world-integration defects, not a flaw unique to this optimization.
- Automatic per-change room rediscovery, a mandatory persistent air-space graph and a single exterior-wall bit as sole authority were explored but are not the current accepted room model.

## Remaining Implementation Evidence

No measured speedup has been established. Evaluate path-generation cost, witness density, full-rebuild frequency, room-check cost and memory independently. Ordinary walls, shared boundaries, detached fragments and batches of edits matter more than speculative adversarial geometry.

Exact pathfinding heuristics, compact-storage containers and invalidation scheduling remain implementation choices to derive when work begins. There is no accepted mandatory global spatial index, per-air-block store or exact performance target.

[[Station Construction Pathfinding Research]] was reviewed as source evidence. Unit-cost six-face movement permits exact BFS. A* to any marked target is another candidate, but its heuristic cost and worst-case exploration must be counted. The source set does not establish that standard 2D JPS is valid for our 3D construction graph or select a final path-generation algorithm.

This decision does not authorize silently changing service semantics or claiming optimization of room checks from connectivity markers alone. It is not an implementation task list or a save-format specification.
