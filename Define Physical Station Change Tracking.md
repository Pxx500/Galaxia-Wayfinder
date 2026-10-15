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

How can Physical Stations avoid unnecessary connectivity recomputation while keeping construction data compact and inspectable?

## Resolution

Use a connected construction-path witness, compact section-local coordinates and batched updates. This is accepted design intent, not measured optimization or completed implementation. Room validation and airlock classification remain separately deferred under [[Consolidate Physical Station Architecture]].

## Connectivity Witness

- Connect all registered functional points, including the main controller, through one branching network of actual construction paths. Structural blocks can carry paths without becoming destinations.
- Prefer short paths heuristically. New points may join any reachable part of the connected witness. Independent nearest-neighbor pairs must not leave disconnected groups.
- Store path membership, not persistent parent pointers, per-device routes or incremental tree repair.
- Removing an unmarked structural block preserves the selected connections. Removing a marked block triggers full connectivity and marker recomputation. A cut witness does not prove disconnection because another route may exist.
- Retained Station IDs do not give disconnected fragments service. Adding a functional object there must establish connectivity before enabling Station-dependent functions.
- Registration changes, main-controller changes and reconnection must update or invalidate the witness. New destinations can extend it. Obsolete marks after removal may wait for a rebuild because they cause extra invalidation, not false connectivity.

## Targeted Updates

Track device connectivity, room approval and pressure, and functional changes separately. Coalesce edits so an explosion does not trigger one full recomputation per block.

Keep the last confirmed service state while connectivity recomputation is pending. Withdraw energy or inventory access only after actual disconnection is confirmed. The accepted short delay avoids outages when an alternate path exists.

A connectivity witness does not prove sealing or authorize automatic room revalidation. Boundary dependencies and unknown airlock sides follow [[Define Manual Physical Room Validation]] and [[Define Airlock Space Classification]]. A direct spatial ownership index is optional and profiling-driven.

## Compact Construction Data

Group positions into 16 by 16 by 16 chunk sections. Store the section once and pack four local coordinate bits per axis into a 16-bit entry. The remaining four bits can hold small markers such as witness membership.

Do not repeat Station identity where the containing collection already owns it. Richer room references and face associations need separate data only where required. A single exterior-wall bit cannot establish sealing.

Two bytes per position describes the packed entry, not total memory or file size. Section headers, collections, room interiors and associations, functional data, worker snapshots, world data and inventories add cost.

## Derived Data Lifecycle

Rebuild connectivity witnesses and derived wall markers at startup rather than persisting optimization caches. Preserve persistent Station identity and room environmental state. Unloaded chunks and interaction with manual approval remain unresolved in [[Define Physical Room Validation Recovery]].

## Thread Debug View

Provide a switchable in-world overlay of the selected Station's actual witness marks and branches. It must visualize the same membership data used by invalidation, not an approximate separately generated network. Activation and rendering are implementation choices. The overlay is not yet implemented.

## Algorithm and Measurement Boundary

Measure generation cost, witness density, rebuild frequency, room-check cost and memory separately on ordinary walls, shared boundaries, detached fragments and edit batches.

[[Station Construction Pathfinding Research]] supports exact BFS for unit-cost six-face movement and identifies A* to any marked target as another candidate. It does not validate ordinary 2D JPS for this 3D graph or select an algorithm.

No mandatory global spatial index, per-air-block store, local cube-search layer or exact performance target is accepted. A spanning tree covering every structural block would defeat the intended selective witness.

## Provenance

Owner discussion following `fe27e3e5` on 2026-09-13. The connectivity direction was retained on 2026-09-16 while room redesign was deferred.
