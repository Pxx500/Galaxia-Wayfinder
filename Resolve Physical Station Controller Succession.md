---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Resolve Physical Station Controller Succession

## Question

When a Physical Station controller is destroyed but another eligible controller survives in its Station graph, may that controller preserve the same Station asset identity, or must destruction always end the original identity?

## Resolution

Accepted on 2026-09-13. A Physical Station retains one Station asset ID across succession between its connected controllers. Each controller knows its Station membership. One is the main controller, and a surviving controller takes over when the main controller is destroyed. Temporary disformation and chunk unload are not controller destruction. This replaces the earlier rule that destroying the main controller necessarily ends the Station identity.

Machines belonging to the Station inherit its Station ID as membership, not as a replacement for their individual identities. Station-local named routing and arrival-time receiver selection are owned by [[Define Transport Endpoint Identity and Registration]].

## Construction Membership and Availability

Provisionally accepted on 2026-09-13 for implementation and profiling:

- The Station owns one durable identity. Its controllers and physical machines refer to that identity as membership.
- Membership propagates through face-connected Station construction blocks, including walls, floors, panels, glass, and airlock construction. Airlock door state affects sealing, not membership.
- Construction membership is represented outside individual block Tile Entities. Placement and removal update that representation. A new controller adopts the Station identity of its connected construction instead of requiring airlock adjacency.
- Previously built unassigned construction can acquire membership when connected to a Station. Building rooms before airlocks must not prevent joining one Station.
- The main controller determines the active connected fragment. Disconnected fragments retain membership but lose Station-provided functionality. Reconnecting restores availability without changing identity.
- Station inactivity does not command independent GregTech machines to stop. Station plugs stop supplying Station energy, and affected machines may subsequently stop through their ordinary power-loss behavior.
- Every controller displays its main or secondary role. A Make Master action explicitly transfers the role within the same Station, including from a disconnected fragment. The newly selected main controller determines the active fragment.
- Destroying the main controller elects a deterministic successor only from the fragment active immediately before destruction. A controller in an already disconnected fragment cannot automatically take over.
- If no eligible successor remains in the previously active fragment, the Station retains its identity and remains inactive until a player selects a surviving controller with Make Master.
- Chunk unload and temporary disformation are not destruction and never trigger succession.
- Joining construction with different Station IDs must not silently merge ownership or choose an arbitrary ID. Explicit merge was discussed as the preferred direction, but no full merge contract was selected. On 2026-09-16 the owner deferred this low-priority edge case after requesting a check of existing code. [[Define Physical Station Merge Contract]] preserves that scope and evidence without making a new merge feature a prerequisite for current work.

These decisions replace airlock-driven Station membership, not the separate physical room geometry and sealing rules. Performance and world-update coverage must be verified during implementation rather than assumed from the model.

## Previous Decision

Define Transport Endpoint Identity and Registration originally tied exact endpoint identity to controller lifetime. Station membership and succession now follow the resolution above. Define In-Flight Delivery Handling for Unavailable Physical Stations still distinguishes temporary unavailability from permanent destruction.

## Current Code Evidence

Read-only inspection on 2026-09-12 found an explicit successor branch in `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/station/TileStation.java:572`. Lines 587 through 598 transfer the same backing asset ID to the successor and keep the asset enabled. Deletion occurs when no such handoff retains the identity and the event is not unload.

## Scope

This is a Station-specific identity rule, not authorization to change code. It does not give a rebuilt individual endpoint its predecessor's exact ID. No new requirement to retain a Station after all its controllers are destroyed has been accepted.
