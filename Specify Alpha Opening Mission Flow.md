---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by:
  - "[[Define Alpha Transport Roles]]"
  - "[[Define Alpha Celestial Knowledge Layers]]"
claimed_by: null
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Specify Alpha Opening Mission Flow

## Accepted Opening Flow

The Silo can deploy a satellite into its current world's orbit without opening the Star Map or choosing another celestial destination. This remains an ordinary local launch capability after the opener.

The opening is a scenario of the ordinary persistent Rocket, payload and Vehicle Schedule systems. It must not use a separate scripted launch executor or an opening-only transport model. The Factorio Space Age-inspired place, action and generated-route flow follows [[Define Space Transport Dispatch Model]] and [[Define Rocket Route Fuel Budgets]]. A pre-map local editor must preserve the same execution semantics even when it exposes fewer destinations.

1. Build the Primitive Telescope Satellite from starting-world materials under [[Design Early Orbital Production Recipe Chain]].
2. Successfully deploy it into Overworld orbit. Building the item or starting launch is insufficient.
3. Grant the Galaxia team launch achievement and unlock the team's Star Map immediately. The achievement supplies passive Luna celestial-profile scan progress, rather than waiting for scan completion.

[[Define Satellite Manufacturing and Deployment Progression]] owns achievement sharing and the scripted survey. The payload does not require a registered satellite asset, worker or simulated lifecycle and does not scan physical-world blocks or ore deposits.

## Initial Knowledge

The developer authors default visibility on each celestial definition to represent prior observation. Opening the map exposes those known objects without generating a new tier-based list, granting full profiles or requiring rediscovery.

Map access and object knowledge are distinct. Only Overworld resources start known. Luna is already known as an object, but its resources are unknown until the survey. The map remains locked until successful opening deployment.

## Reuse And Automation

Rockets are reusable whenever their planned recovery, actual fuel and infrastructure permit another flight. They do not gain physical reusability from a later vehicle flag.

Early Rockets can fly manually to Luna. Optional orbital production, obtainable before that trip, supplies upgraded control electronics that add automatic flight/control to the same Rocket. No mandatory Station-completion or automation-unlock check gates lunar travel.

Regular Luna supply should support a reusable automated loop once technology and servicing exist. Repeated satellite-launch examples do not prescribe a fixed launch count or automatic return for the opener. Recycling materials and recovering a flight-ready Rocket are distinct outcomes.

## Mission Recovery

Evaluate the concrete action sequence, not an assumed round trip. `reach orbit -> deploy satellite -> return and land` may exceed actual fuel. Removing return can make deployment feasible without making the Rocket recoverable.

[[Define Rocket Missions Without Recovery]] permits that deliberate ending with a warning that the Rocket disappears after the mission. Successfully deployed payloads and achievements remain credited.

A planned feasible pad landing/docking remains a recovery action even if the pad is occupied. Depart, reach the destination and wait there with maneuver fuel intact under [[Define In-Flight Delivery Handling for Unavailable Physical Stations]]. Waiting consumes no fuel or wear and is not disposal. An orbital receiver does not create return fuel.

## Content And Implementation Boundary

[[Design Early Orbital Production Recipe Chain]] owns concrete payload, orbital-material, automation-controller and technology-acquisition recipes and their acceptance status. Early designs, mission fuel/payload balance, exact launch counts and the repair machine are not selected by this flow.

Read-only inspection on 2026-09-12 found direct opening in `registry/items/special/ItemGalacticMap.java:19` without the deployment prerequisite, and `registry/celestial/CelestialRegistry.java:524` used `discoveredUnknown()` rather than per-body default visibility. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. These dated gaps are not a current audit or proof that the accepted opening is implemented.

## Provenance

Owner decisions on 2026-09-10 establish local pre-map launch and authored visibility. Clarifications on 2026-09-17 make orbital automation optional before Luna and physical reuse mission-dependent. The 2026-10-07 decision accepts deliberate missions without recovery. The recipe-chain note records the selected Primitive Telescope Satellite name.
