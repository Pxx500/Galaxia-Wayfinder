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

Can surviving controllers preserve a Physical Station's identity after its main controller is destroyed?

## Resolution

A Physical Station has one durable asset ID across succession between its controllers. Controllers and machines carry that ID as membership, not as a replacement for their individual identities. This supersedes ending Station identity whenever the main controller is destroyed.

## Construction Membership and Availability

Provisionally accepted for implementation and profiling:

- Membership propagates through face-connected Station construction, including walls, floors, panels, glass and airlock construction. Door state affects sealing, not membership.
- Membership is represented outside individual block Tile Entities and updated on placement and removal. New controllers adopt their connected construction's identity without airlock adjacency.
- Unassigned construction can join when connected. Rooms may be built before airlocks.
- The main controller selects the active connected fragment. Disconnected fragments retain membership but lose Station-provided functionality. Reconnection restores availability without changing identity.
- Station inactivity stops Station plugs supplying energy, not independent GT machines directly. Their ordinary power-loss behavior may stop them later.
- Each controller displays its main or secondary role. Make Master can transfer the role within the same Station, including from a disconnected fragment.
- Main-controller destruction elects a deterministic successor only from the fragment active immediately before destruction.
- If that fragment has no eligible successor, retain identity and stay inactive until the player selects a surviving controller with Make Master.
- Chunk unload and temporary disformation are not destruction and never trigger succession.
- Different Station IDs must not silently merge. [[Define Physical Station Merge Contract]] defers the unresolved merge edge case.

These rules replace airlock-driven membership, not room geometry or sealing. Performance and world-update coverage require implementation evidence.

## Identity Boundary

[[Define Transport Endpoint Identity and Registration]] owns Station-local routing and arrival-time receiver selection. A rebuilt endpoint does not inherit its predecessor's exact ID. [[Define In-Flight Delivery Handling for Unavailable Physical Stations]] distinguishes temporary unavailability from permanent destruction.

No rule to retain a Station after all its controllers are destroyed is accepted.

## Implementation Evidence and Provenance

Accepted on 2026-09-13. Read-only inspection on 2026-09-12 found a successor branch in `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/station/TileStation.java:572`, with the backing asset ID transferred at lines 587 through 598. That earlier code does not establish implementation of the later construction-centric model.
