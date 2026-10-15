---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Alpha Transport Roles

## Accepted Decision

Transport methods deliberately overlap. Eligibility follows concrete vehicle, route, endpoint and infrastructure capabilities, not exclusive cargo permissions, destination whitelists or abstract transport levels. Recipes and physical infrastructure create the practical unlock order.

| Transport | Role and trade-off | Endpoint requirements |
| --- | --- | --- |
| Rocket | First-arrival bootstrap, players and cargo, general surface access, high propellant and module-lifecycle cost | Prepared surface or orbital endpoints, or manual Unprepared Landing |
| Spaceship | Slow reusable high-capacity space-to-space player/cargo freight, expensive vehicle with low fuel/per-unit cost | Compatible physical or Automated Facility Docks at both ends |
| Hammer | Fast low-throughput, high-per-unit-cost freight, permanently cargo-only | Compatible sender and receiver for ordinary freight |

Rockets establish footholds. Hammer becomes useful with sending, receiving and orbital infrastructure. Spaceships become useful once orbital Shipyards and Docks exist at both ends. Accepted intent does not certify complete route implementation.

## Rocket Bootstrap And Docking

Every Rocket has built-in docking, not an optional module. It can use surface Silos/Pads, physical orbital Docks and logical Automated Facility Docks. Space-to-space Rocket travel is allowed but less efficient than Spaceship freight. Reuse depends on mission recovery, not a later vehicle-class flag.

A manually dispatched crewed or unmanned cargo Rocket may use Unprepared Landing before a destination has team infrastructure:

- Optional X/Z coordinates select the search origin. Without them, inherit departure X/Z directly in the destination world, for example X=100, Z=100 on both worlds. The system determines height.
- Preflight `Search for Landing Site` resolves and displays one actual stable terrain position before departure, not hazardous fluid or void. The player may change coordinates and rescan.
- Use deterministic nearest-site search with fixed expansion order and stable equal-distance tie-breaks for the same destination, coordinates and relevant world state. Moving thousands of blocks is acceptable because the result is shown in advance.
- Accepting the mission reserves the resolved Rocket footprint. Scans reject existing Rocket footprints and pending reservations. Cancellation releases the reservation. After arrival physical occupancy protects the space.
- An unprepared target is not a Transport Endpoint and cannot be stored in an automated schedule. Automated logistics need an exact endpoint or group.
- After an unmanned landing the physical Rocket and cargo remain until the player arrives and builds handling infrastructure.
- Physical belt travel must land on Regional Dimension terrain. Persistent Star Map asteroids remain non-visitable infrastructure targets under [[Define Asteroid Belt Physical Travel and Beacons]].

## Spaceships

Spaceships cannot perform planetary surface-to-orbit ascent, target a surface directly or use Unprepared Landing. Zero-gravity asteroid Outpost Docks are eligible space endpoints. Physical and Automated Facility docking expose the same targeting capability even if servicing differs.

Orbital Shipyards build, dock, refuel and transfer cargo. Unmanned Spaceships have no maximum mission duration. [[Define Destination Access Levels]] owns the provisional 180-second maximum for crewed Rockets, cargo Rockets and crewed Spaceships and the provisional maneuver model.

## Hammer Freight

Local Hammer transport connects a surface and that body's orbit in either direction. Orbital Hammer transport connects orbital endpoints. Longer routes normally use orbital infrastructure. Direct surface-to-surface freight may work between sufficiently close related bodies, such as a planet and moon. Its exact boundary remains balance work, not an absolute topology ban.

- Surface-to-orbit requires surface Cannon and orbital Target. Orbit-to-surface requires orbital Cannon and surface Target. Orbit-to-orbit needs both orbital installations.
- Gravity, atmosphere and direction determine shot feasibility and cost. Airless surfaces are naturally easier.
- Only surface-launched freight has a hard atmospheric-density limit, intended to exclude a small number of exceptionally dense worlds while allowing most planets. It applies to the source atmosphere for direct surface-to-surface freight.
- Atmospheric density does not prohibit orbital-to-surface freight. Braking helps descent, while wind/dispersion can make delivery harder without a categorical ban.
- Cargo contents add no mass to feasibility or cost. Exact cost and close-body limits belong to [[Define Flight Progression Balance Invariants]].

Satellite deployment is a scoped receiver-free operation, not ordinary freight. [[Define Satellite Manufacturing and Deployment Progression]] owns `Deploy to Orbit`. [[Define Hammer Satellite Deployment Reach]] owns its accepted atmosphere-free surface restriction, same-orbit local reach and whole-star-system Big Hammer reach. These stricter deployment rules do not replace freight's density threshold.

## Implementation Evidence And Provenance

Read-only inspection on 2026-09-12 found that `registry/outpost/logistics/HammerDispatchPlanner.java:202` used a fixed one-tick/delta-v same-body path and planetary anchors for family eligibility. Different-body energy used total delta-v, while the player condition checked departure delta-v. The directional atmosphere limit and complete surface/orbit topology were absent. `registry/celestial/station/attachments/TileHammerCannon.java:199` hardcoded a large UV module. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

The transport contract remains accepted. Hammer satellite origin/reach were resolved by the owner on 2026-10-07, superseding their earlier provisional status.

## Related Decisions

- [[Define Alpha Transport Technology Baseline]]
- [[Define Automated Rocket Turnaround and Module Wear]]
- [[Define Vehicle Capability and Route Requirements]]
