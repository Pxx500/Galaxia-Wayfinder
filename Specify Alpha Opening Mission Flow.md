---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by:
  - "[[Define Alpha Transport Roles]]"
  - "[[Define Alpha Celestial Knowledge Layers]]"
claimed_by: local-wayfinder-reconciliation
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Specify Alpha Opening Mission Flow

## Question

When should the opening progression provide reusable Rocket transport after the accepted first observation launch? The payload, local launch flow, team map unlock and initial visibility rules below are already settled.

## Accepted Requirements

- The Silo can dispatch a Rocket to deploy a satellite into the orbit of its current world without opening the Star Map or selecting another celestial destination.
- Local orbital satellite deployment remains an ordinary launch capability after the first mission. It is not an opening-only launch system.
- The opening payload is an ordinary Prospecting Satellite. After deployment, it continues discovery and detailed scanning through the normal satellite system.
- The first successful deployment of a team Prospecting Satellite into the starting world's orbit unlocks the team's Star Map. Building a satellite or beginning a launch does not suffice.
- The developer authors an object's default visibility as part of its celestial definition. This represents prior observational knowledge of objects visible in the sky, not knowledge of their atmosphere or deposits.
- Opening the Star Map exposes those initially known objects. It does not generate a new initial list based on tier, grant full profiles, or require the player to discover a visibly known body again.
- Default object knowledge and access to the Star Map are separate. Even when objects are already known by definition, the map remains locked before orbital Prospecting Satellite deployment.

## Remaining Decision

The fate of the early launch vehicle remains provisional. Most Rockets, modules, and equipment should support recycling or recovery, but the earliest Rocket designs may be expendable and lost after deployment as a natural progression step. The owner has not fixed the number of expendable launches, the applicable designs, or the later recovery mechanism. Do not assume an automatic return to the starting Silo for the opening mission.

This is a balance and vehicle-design follow-up. Do not repeatedly ask the owner to choose an exact number before the surrounding Rocket progression exists. Recyclability and reuse are distinct: recovering materials does not necessarily return a flight-ready Rocket.

## Current Implementation Boundary

Read-only inspection on 2026-09-12 found that `registry/items/special/ItemGalacticMap.java:19` opens the map directly without the required satellite-deployment check in this entry point. `registry/celestial/CelestialRegistry.java:524` gives registered bodies `discoveredUnknown()` starting knowledge rather than consulting a configurable per-body visibility value. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

The satellite activation requirement and developer-authored starting visibility remain accepted intent. The earlier owner report that per-body visibility already exists is not confirmed by these current paths. Neither observation settles the early Rocket's fate or requires reopening the accepted map-unlock decision.

## Provenance

Owner decisions in the Wayfinder conversation on 2026-09-10. The owner also reports that developer-authored default visibility already exists in code. This note records that intended source of starting knowledge without replacing it with a new visibility calculation.

The owner subsequently expressed a provisional preference for expendable earliest Rockets while retaining recycling as the general mod direction. Automatic return was proposed but not accepted.
