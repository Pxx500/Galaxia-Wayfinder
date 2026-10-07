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

## Question

What separate Alpha responsibilities, unlock relationships, payloads, and endpoint requirements belong to Rockets, Spaceships, and Hammers so they form complementary transport systems rather than interchangeable logistics methods?

## Resolution

Alpha transport methods overlap through capability-based trade-offs instead of exclusive destination or cargo whitelists. Rockets provide reusable general surface access, first-arrival bootstrap, player transport, cargo transport, and built-in docking at high propellant and maintenance cost. Spaceships provide slow, reusable, high-capacity player and cargo transport between prepared physical or Automated Facility Docks. Hammer provides fast, low-throughput, cargo-only delivery between prepared sending and receiving infrastructure, with route topology, gravity, atmosphere, and direction controlling cost and feasibility. Their practical unlock order emerges from recipes and required infrastructure rather than a separate transport-access level.

## Accepted Requirements

- [[Define Satellite Manufacturing and Deployment Progression]] owns the accepted `Deploy to Orbit` mode for satellite payloads. It targets an orbit rather than a receiver, while ordinary Hammer freight still requires a receiver. The local and Big Hammer deployment ranges remain working balance direction.

- A manual player-carrying Rocket mission may target the surface of a Celestial Object that has no team Transport Endpoint. This is the bootstrap path for first arrival and infrastructure construction.
- An unmanned Cargo Rocket may use the same Unprepared Landing flow as a manually dispatched one-shot mission. It may deliver bootstrap cargo before the destination has a team Transport Endpoint.
- The player may optionally provide surface X/Z coordinates for that manual landing. The landing system determines the actual surface height.
- Without explicit coordinates, the landing starts from the departure location's X/Z coordinates mapped directly onto the destination world. A Rocket departing near X=100, Z=100 therefore first searches near X=100, Z=100 on Luna.
- The landing system searches around the requested or inherited X/Z position for a valid stable landing site rather than placing the Rocket blindly at the exact coordinate.
- A valid site must place the Rocket on actual supporting terrain rather than in a hazardous fluid or empty space. Physical asteroid-belt travel must resolve to actual terrain in the Regional Dimension rather than void. Persistent Star Map asteroids remain non-visitable infrastructure targets under Define Asteroid Belt Physical Travel and Beacons.
- Unprepared Landing exposes a preflight `Search for Landing Site` action. The scan resolves the requested or inherited X/Z target into one concrete valid landing position before the Rocket departs.
- Landing-site selection is deterministic. The same destination, starting coordinates, and relevant world state produce the same selected site.
- The scan prefers the nearest valid site to the initial X/Z target. It expands its search in a fixed order and uses a stable tie-break when several candidates are equally close.
- The search may move thousands of blocks from the initial X/Z coordinates when necessary to find stable terrain. This is acceptable because the exact result is shown before departure and the player may choose different coordinates and scan again.
- Alpha prevents overlapping Unprepared Landings through a minimal landing-site reservation. Accepting a mission reserves the resolved Rocket footprint before departure.
- Landing scans treat both physically occupied Rocket footprints and pending landing reservations as invalid, then deterministically select the next nearest stable site.
- Cancelling a mission releases its pending landing reservation. After arrival, the physical Rocket's occupied footprint continues to keep later scans from selecting the same space.
- This unprepared landing target is not a Transport Endpoint and cannot be stored in an automated Vehicle Schedule. Automated logistics still require an exact Transport Endpoint or Endpoint Group.
- After an unmanned Unprepared Landing, the Rocket and its cargo remain physically at the resolved site until the player reaches it and builds the infrastructure needed to handle them.
- Transport eligibility is capability-based rather than assigned through vehicle-to-destination whitelists. Players may move items with Rockets, Spaceships, Hammers, or later transport systems whenever the concrete vehicle, endpoints, route, and mission satisfy their requirements.
- Transport systems overlap deliberately. Their roles emerge from trade-offs in endpoint access, atmosphere response, throughput, speed, reusability, fuel use, operating cost, and required infrastructure rather than exclusive cargo permissions.
- The practical Alpha unlock sequence emerges from infrastructure. Rockets establish the first off-world footholds, Hammer becomes useful after its sending, receiving, and orbital infrastructure exists, and Spaceships become useful after orbital Shipyards and Docks exist at both ends.
- Recipes, material tiers, and the required physical infrastructure control when each method becomes available. Galaxia does not add a separate abstract transport level or destination whitelist.
- Reusable cargo ships provide high-volume space-to-space freight between locations that do not require a major gravity-well ascent.
- Spaceships may carry both players and cargo between eligible space-to-space endpoints.
- Unmanned Spaceships have no maximum mission duration. Their role is slow, high-capacity bulk transport with a high reusable vehicle cost and relatively low fuel and per-unit transport cost.
- Crewed Rockets, cargo Rockets, and crewed Spaceships provisionally use the 180-second maximum transfer duration. This split remains balance-sensitive and may change in response to concrete route or acceleration findings.
- Orbital shipyards build, dock, refuel, and transfer cargo for cargo ships.
- HAMMER provides fast cargo logistics for airless surfaces and other objects without atmosphere, trading low throughput and high per-unit cost for short delivery time.
- Hammer is permanently cargo-only. It never transports players.
- HAMMER is broadly capable but has difficulty operating through atmosphere.
- Hammer routes belong to two infrastructure families. Local Hammer transport connects a surface with that Celestial Object's orbit in either direction, while orbital Hammer transport connects one orbital endpoint with another orbital endpoint.
- Direct surface-to-surface Hammer transport is not generally available, but sufficiently close related bodies such as a planet and its moon may support it. The exact route boundary remains a gameplay-balance decision rather than an absolute topology rule.
- Longer Hammer logistics are expected to pass through orbital infrastructure, preserving the need to build and maintain space assets without forcing unnecessary transfer micro on every short local route.
- Every Hammer delivery requires compatible sending infrastructure and receiving infrastructure. Surface-to-orbit uses a surface Cannon and orbital Target, orbit-to-surface uses an orbital Cannon and surface Target, and orbit-to-orbit uses orbital infrastructure at both ends.
- Hammer shot feasibility and operating cost depend on the relevant gravity well, atmospheric conditions, and direction of travel. These physical route properties may make a shot more expensive or impossible rather than acting as an arbitrary destination whitelist.
- Atmospheric density provides an independent hard feasibility constraint only for a Hammer shot launched from a surface. A sufficiently dense source atmosphere may block surface-to-orbit or direct surface-to-surface launch regardless of gravity, energy affordability, or other favorable route properties.
- The hard atmospheric limit is intended to block Hammer launch on only a small number of exceptionally dense-atmosphere destinations. Surface launch should remain possible on most planets.
- Orbit-to-surface Hammer delivery is not prohibited by atmospheric density. Aerodynamic braking is helpful on descent, while wind or dispersion may make delivery more difficult without making the route categorically impossible.
- For a direct surface-to-surface route, the hard atmospheric check applies to the source atmosphere rather than the destination atmosphere.
- Airless surfaces remain Hammer's natural low-friction operating environment.
- Cargo contents do not contribute mass to Hammer cost or feasibility. Exact surface-to-surface distance limits and cost tuning belong to [[Define Flight Progression Balance Invariants]].
- Rockets provide general surface access but have high per-flight propellant consumption, especially for surface ascent and other surface-to-orbit or orbit-to-surface maneuvers. Individual Rocket modules may also create recurring repair or replacement costs through [[Define Automated Rocket Turnaround and Module Wear]].
- Every Rocket has built-in docking capability by default. Docking is not an optional Rocket module or a special vehicle configuration.
- Rockets may use compatible physical orbital Docks and logical Docks exposed by Automated Facilities in addition to surface Silo or Rocket Pad endpoints.
- Spaceships provide low per-unit bulk transport between prepared space endpoints, including zero-gravity asteroid Outpost Docks. They cannot perform planetary surface-to-orbit ascent.
- A Spaceship requires a compatible dock-capable Transport Endpoint at both departure and arrival. It cannot target a surface directly or use Unprepared Landing.
- A dock-capable endpoint may be a physical Dock in a player-accessible world or the logical transport endpoint exposed by a docking module in an Automated Facility.
- Vehicle Schedules treat physical and Automated Facility docking as the same endpoint capability. Their internal cargo handling and service execution may differ without changing the Spaceship's targeting model.
- Rockets may also fly space-to-space routes, but they are less efficient there than Spaceships.
- Transport eligibility should ultimately depend on multiple route and vehicle variables rather than atmosphere alone; atmosphere remains one contributor rather than the transport-role boundary.
- Vehicle acceleration and its relationship to achievable transfer duration use the provisional model documented below and in [[Define Destination Access Levels]].

## Historical Acceleration Research

These are findings from the original research checkout, not a fresh implementation audit. The provisional maneuver model is owned by Define Destination Access Levels.


- The current orbital transfer model uses impulsive Lambert trajectories. It calculates required departure and capture velocity changes but does not model vehicle thrust, mass, fuel flow, or burn duration inside the trajectory.
- Adding full continuous-thrust trajectory optimization would replace the current problem with a substantially more expensive optimal-control search. It is not suitable as the default synchronous Star Map route calculation, especially across large destination sets.
- A low-cost model can retain Lambert route generation and use vehicle thrust and current mass afterward to determine whether its required maneuvers can be completed quickly enough for that route approximation.
- This feasibility check adds little cost compared with generating the existing route candidates. A vehicle that fails a fast candidate may still qualify for a slower candidate.
- Current Rocket data exposes thrust, mass, and fuel, but those values are not yet internally consistent enough for reliable physical burn-duration calculations. Spaceship propulsion does not yet have an equivalent concrete model.
- The acceptable burn-duration tolerance for treating a maneuver as impulsive remains a balance value to be tuned.

## Acceleration Model Decision

Alpha retains impulsive Lambert route generation and adds a boolean Burn Feasibility result for each maneuver required by the selected mission.

Burn Feasibility is derived for a specific vehicle state and maneuver. It is not a stored vehicle tier or one global property of a Rocket or Spaceship.

- Surface takeoff checks whether current thrust relative to mass can overcome local gravity and atmospheric conditions, and whether the vehicle has enough delta-v for ascent.
- An orbital departure or capture burn checks whether the vehicle has enough propellant and delta-v and can deliver the maneuver within the accepted burn-duration window.
- The provisional Alpha check calculates burn duration for the current single-stage vehicle and compares it with a configurable fraction of the local orbital dynamic timescale `sqrt(r^3 / mu)`.
- Burn duration does not extend or redefine the Lambert candidate transfer time. Orbital cruise between maneuver burns is unpowered coasting.
- Escaping a gravity well may require a sequence of successful takeoff and orbital maneuvers rather than one generic burn check.
- A mission is feasible only when every maneuver in its selected route is feasible. Player-facing feedback names the exact failed maneuver and concrete limiting factor.

The shared burn-duration tolerance remains an implementation-time balance value. The model itself is provisional and may be replaced if profiling or gameplay testing shows that the approximation is unsuitable.

## Current Hammer Implementation Boundary

Source inspection on 2026-09-12 found that `registry/outpost/logistics/HammerDispatchPlanner.java:202` uses a one-tick, fixed-delta-v same-body path and shared planetary anchors for small-versus-large eligibility. Different-body shot energy uses total route delta-v, while the player's delta-v condition checks departure delta-v. The inspected candidate checks do not implement the accepted directional atmosphere limit or complete surface/orbit endpoint topology.

`registry/celestial/station/attachments/TileHammerCannon.java:199` still constructs a large UV module with a tiering TODO. Proper physical Hammer progression remains the already accepted implementation requirement. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. These observations do not reopen the transport or atmosphere rules.
