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
- The opening payload is the special scripted satellite owned by [[Define Satellite Manufacturing and Deployment Progression]], not an unrestricted ordinary Prospecting Satellite.
- Its first successful deployment into Overworld orbit grants the shared launch achievement and unlocks the team's Star Map. Possessing the achievement provides passive Luna resource scan progress. The achievement does not wait for the scan to finish. Building the satellite or beginning a launch does not suffice.
- The developer authors an object's default visibility as part of its celestial definition. This represents prior observational knowledge of objects visible in the sky, not knowledge of their atmosphere or deposits.
- Opening the Star Map exposes those initially known objects. It does not generate a new initial list based on tier, grant full profiles, or require the player to discover a visibly known body again.
- Default object knowledge and access to the Star Map are separate. Only Overworld resources are initially known. Luna is already known as an object but its resources remain unknown until surveyed. The map remains locked before the opening satellite's deployment.

## Accepted Early Reuse Milestone

On 2026-09-17 the owner confirmed repeatable Rocket use during the Luna transport stage. The earliest Rockets do not support the later unattended transport automation. Early orbital production supplies upgraded control electronics for that automation. Physical reuse itself depends on the mission and recovery conditions, not a technology flag.

The examples of repeated satellite launches do not prescribe a fixed launch count. Regular Luna supply should support a reusable automated loop once the relevant technology and servicing infrastructure are available. This does not choose a Gantry servicing machine or imply automatic return for the opening launcher.

The owner subsequently clarified that the orbital capability should be obtainable before the player needs to visit Luna, but is optional for that trip. A player may instead fly manually to Luna with a capable early Rocket. There is no mandatory Station-completion or automation-unlock check for lunar travel.

The preferred upgrade is additional control electronics fitted to the same Rocket, granting automatic flight and control, rather than requiring a wholly different Rocket. The owner clarified that Rockets are reusable whenever the mission permits recovery and another flight. Reuse is not an inherent property restricted to a later Rocket class.

## Mission Plan And Recovery Contract

The owner clarified that the player specifies a concrete sequence of actions and the Rocket carries actual fuel. The planner evaluates that sequence, not an assumed round trip. For example, `reach orbit -> deploy satellite -> return and land` may lack sufficient fuel. Removing the return action can make the outbound deployment feasible without making the Rocket recoverable afterwards.

[[Define Rocket Missions Without Recovery]] resolves the terminal state for an intentional mission without a recovery ending. The planner warns that the Rocket disappears after the mission. An initial deployment ending in orbit without a feasible recovery can use this contract. Successfully deployed payloads and achievements remain credited.

If the plan includes a feasible landing or docking maneuver at an orbital pad, that recovery action remains part of the plan. An occupied destination pad does not hold the Rocket at its previous departure point. It flies to the destination, then waits there before docking until capacity is available. Waiting retains the fuel needed for the remaining maneuver and follows the existing no-waiting-consumption rule.

Later orbital infrastructure can receive a Rocket, but receiving it does not create return fuel. Return still requires actual supplies and a feasible flight. Fuel, payload and early vehicle capability need balance validation rather than an arbitrary reusable/non-reusable vehicle flag.

This is consistent with [[Define In-Flight Delivery Handling for Unavailable Physical Stations]]: ordinary temporary destination unavailability retains the vehicle and planned recovery. The opening example has no feasible onward recovery action, rather than being a valid pad arrival that happens to find its pad occupied.

## Working Satellite Revision

[[Define Satellite Manufacturing and Deployment Progression]] owns the accepted special map-unlocking satellite followed by orbital-material-based functional satellites. The first satellite must remain obtainable from starting-world materials, without depending on the Station whose access it enables.

## Remaining Decisions

- The concrete Station activity or production result that grants the technology, aligned with [[Define Alpha Technology Knowledge Contract]]. No automatic station-visit unlock or new research minigame was selected.
- The opening satellite's exact capabilities under the proposed satellite progression, owned by Define Satellite Manufacturing and Deployment Progression.

Exact early vehicle designs and launch counts remain content work. Recyclability and reuse are distinct: recovering materials does not necessarily return a flight-ready Rocket.

## Current Implementation Boundary

Read-only inspection on 2026-09-12 found that `registry/items/special/ItemGalacticMap.java:19` opens the map directly without the required satellite-deployment check in this entry point. `registry/celestial/CelestialRegistry.java:524` gives registered bodies `discoveredUnknown()` starting knowledge rather than consulting a configurable per-body visibility value. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

The satellite activation requirement and developer-authored starting visibility remain accepted intent. The earlier owner report that per-body visibility already exists is not confirmed by these current paths. These historical observations do not verify the newer recovery contract or require reopening the accepted map-unlock decision.

## Provenance

Owner decisions in the Wayfinder conversation on 2026-09-10. The owner also reports that developer-authored default visibility already exists in code. This note records that intended source of starting knowledge without replacing it with a new visibility calculation.

The owner initially expressed a provisional preference for expendable earliest Rockets while retaining recycling as the general direction. Later clarification makes recoverability a consequence of the planned actions, actual fuel and infrastructure. Orbital electronics unlock automation rather than granting physical reusability. Automatic return not included in the player's plan is not assumed.

On 2026-10-07 the owner resolved intentional missions without recovery and their planning warning in [[Define Rocket Missions Without Recovery]].
