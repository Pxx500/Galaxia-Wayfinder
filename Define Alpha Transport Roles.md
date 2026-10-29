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

# Alpha Transport Roles

## Transport Roles

Transport methods overlap. Vehicle, route, endpoint and infrastructure capabilities determine eligibility, not cargo permissions, destination whitelists or abstract transport levels. Recipes and infrastructure create the practical unlock order.

| Transport | Role and trade-off | Endpoint requirements |
| --- | --- | --- |
| Rocket | First-arrival bootstrap, players and cargo, general surface access, high propellant and module-lifecycle cost | Prepared surface or orbital endpoints, or manual Unprepared Landing |
| Spaceship | Slow reusable high-capacity space-to-space player/cargo freight, expensive vehicle with low fuel/per-unit cost | Compatible physical or Automated Facility Docks at both ends |
| Hammer | Fast low-throughput, high-per-unit-cost freight, permanently cargo-only | Compatible sender and receiver for ordinary freight |

Rockets establish footholds. Hammers become useful as sending, receiving and orbital infrastructure develops. Orbital Shipyards support Spaceship construction and servicing, while compatible Docks at both ends enable their routes.

## Rocket Bootstrap And Docking

Every Rocket has built-in docking for surface Silos/Pads, physical orbital Docks and logical Automated Facility Docks. Space-to-space Rocket travel is allowed but less efficient than Spaceship freight. Reuse depends on mission recovery, not a vehicle-class flag.

A manually dispatched crewed or unmanned cargo Rocket may use Unprepared Landing before a destination has team infrastructure:

- Optional X/Z coordinates select the search origin. Without them, use departure X/Z directly in the destination world, for example X=100, Z=100 on both worlds. The system determines height.
- Preflight `Search for Landing Site` displays one stable terrain position before departure, never hazardous fluid or void. Players can change coordinates and rescan.
- Search deterministically for the nearest site using fixed expansion and equal-distance tie-breaks for the same destination, coordinates and world state. Moving thousands of blocks is acceptable because the result is shown in advance.
- Accepting reserves the Rocket footprint. Scans reject occupied footprints and pending reservations. Cancellation releases the reservation, and physical occupancy protects the space after arrival.
- An unprepared target is not a Transport Endpoint and cannot be stored in an automated schedule. Automated logistics need an exact endpoint or group.
- After an unmanned landing the physical Rocket and cargo remain until the player arrives and builds handling infrastructure.
- Physical belt travel must land on Regional Dimension terrain. Persistent Star Map asteroids remain non-visitable infrastructure targets under [[Define Asteroid Belt Physical Travel and Beacons]].

## Spaceships

Spaceships cannot ascend from a planetary surface, target a surface directly or use Unprepared Landing. Zero-gravity asteroid Outpost Docks are eligible space endpoints. Physical and Automated Facility docks have the same targeting capability, though servicing may differ.

Orbital Shipyards build, dock, refuel and transfer cargo. Unmanned Spaceships have no maximum mission duration. [[Define Destination Access Levels]] owns the provisional 180-second maximum for crewed Rockets, cargo Rockets and crewed Spaceships and the provisional maneuver model.

## Hammer Freight

Local Hammer transport connects a surface and its orbit in either direction. Orbital transport connects orbital endpoints and normally handles longer routes. Direct surface-to-surface freight may work between sufficiently close related bodies, such as a planet and moon. Its exact boundary remains balance work, not a topology ban.

- Surface-to-orbit requires surface Cannon and orbital Target. Orbit-to-surface requires orbital Cannon and surface Target. Orbit-to-orbit needs both orbital installations.
- Gravity, atmosphere and direction determine shot feasibility and cost. Airless surfaces are naturally easier.
- Surface launches have a hard atmospheric-density limit intended to exclude a few exceptionally dense worlds, while allowing most planets. Surface-to-surface freight uses the source atmosphere.
- Density does not prohibit orbital-to-surface freight. Braking helps descent, though wind and dispersion can make it harder.
- Cargo contents add no mass to feasibility or cost. Exact cost and close-body limits belong to [[Define Flight Progression Balance Invariants]].

Satellite deployment needs no receiver and is not ordinary freight. [[Define Satellite Manufacturing and Deployment Progression]] owns `Deploy to Orbit`. [[Define Hammer Satellite Deployment Reach]] defines its stricter atmosphere-free surface restriction, same-orbit local reach and whole-star-system Big Hammer reach. Freight retains its density threshold.

## Implementation Evidence And Provenance

On 2026-09-12, `registry/outpost/logistics/HammerDispatchPlanner.java:202` used a fixed one-tick/delta-v same-body path and planetary anchors for family eligibility. Different-body energy used total delta-v, while the player condition checked departure delta-v. Directional atmosphere limits and complete surface/orbit topology were absent. `registry/celestial/station/attachments/TileHammerCannon.java:199` hardcoded a large UV module. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

Hammer satellite origin and reach were resolved on 2026-10-07.

## Related Decisions

- [[Define Alpha Transport Technology Baseline]]
- [[Define Automated Rocket Turnaround and Module Wear]]
- [[Define Vehicle Capability and Route Requirements]]

## Gameplay Flow

Players use Rockets to establish footholds and carry people or cargo, including by manually landing at an unprepared site. Once compatible infrastructure exists, Spaceships provide reusable high-capacity space freight and Hammers provide fast, lower-throughput cargo transport.

The player chooses a route based on the vehicle and endpoints available. Unprepared landing requires a preflight site search and cannot be saved as an automated endpoint. Ordinary Hammer freight requires compatible sending and receiving infrastructure.
