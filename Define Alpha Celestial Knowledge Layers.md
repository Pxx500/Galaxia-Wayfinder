---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Alpha Celestial Knowledge Layers

## Knowledge and Scanning

For the currently designed Alpha scope, modeled facts are known or unknown. This does not permanently commit all future Alpha content to binary detail.

- First object knowledge includes the orbit needed to plan flight immediately, without an additional research task.
- Discovery alone does not reveal deposits.
- A completed detailed satellite scan reveals environment, atmosphere, relevant hazards and resource profile without a separate research mission.
- Atmospheric probes and extra environmental-information missions are outside current scope.

Starting visibility is separate from scanning. [[Specify Alpha Opening Mission Flow]] owns authored known objects. Only Overworld resources start known. Luna is already known with unknown resources, and the Primitive Telescope Satellite achievement supplies its scripted passive celestial-profile survey under [[Define Satellite Manufacturing and Deployment Progression]]. That is not a physical-world ore scan or a new global scan-tier system.

## Implementation Gaps

Read-only inspection on 2026-09-12 at master `7f66da49` found automatic asteroid DETECTION then PROFILE work in one continuous process. All hidden objects in a scope are detected before profiling starts, so a body's profile is not necessarily the next completed job. No second player scan action is needed.

The inspected sidebar exposed environment after detection, before PROFILE. Registered bodies started discovered outside the asteroid queue and bypassed the minor-body ore gate. Those environment and registered-resource paths do not satisfy the accepted detailed-scan boundary. First-level planner access was not verified end to end.

Evidence under `src/main/java/com/gtnewhorizons/galaxia/`:

- `registry/celestial/AsteroidFieldDiscoveryPolicy.java:75,95`
- `client/gui/orbitalGUI/OrbitalPinnedInfoContentBuilder.java:31,110,117`
- `registry/celestial/CelestialRegistry.java:524`

This is dated source evidence, not runtime verification or a fresh code audit.

## Provenance

Owner decision on 2026-09-10 establishes first-level flight planning and later environment/resource disclosure. The 2026-09-17 opening clarification establishes the Luna bootstrap.

## Gameplay Flow

Once the player knows an object, its orbit is available for flight planning, but its deposits remain unknown. A completed detailed satellite scan reveals its environment, atmosphere, relevant hazards and resource profile without a separate research mission.

At the opening, Luna is already known but its resources are not. The Primitive Telescope Satellite achievement supplies its passive celestial-profile survey, not a physical ore scan.
