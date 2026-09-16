---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
secondary_areas:
  - Area - Travel and Logistics
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Destination Access Levels

## Question

What distinct access outcomes must Galaxia model between discovering a destination and operating there, including reconnaissance, crew arrival, landing, extraction, sustained operation, cargo export, and safe return?

## Resolution

Galaxia does not model destination access as a stored tier, linear state, or destination whitelist. Access is evaluated for the concrete mission and operation through reusable physical constraints such as route energy and duration, local gravity and atmosphere, endpoint compatibility, vehicle capability, and existing infrastructure. Route feasibility, environmental warnings, operational capability after arrival, cargo export, and return capability remain separate outcomes. A player may physically reach a destination before being able to exploit or safely return from it, and every failure or warning names the concrete missing capability or hazardous condition.

## Accepted Access Contract

- A celestial object does not store a technology tier, linear access level, `landed` state, or universal `operational` state.
- Access is evaluated for a concrete mission and separates physical route reachability, mission viability, and the ability to perform progression-relevant operations.
- Vehicle eligibility is derived from concrete capabilities, route conditions, endpoint requirements, and current vehicle state. Destinations do not whitelist or ban transport classes merely to enforce their intended roles.
- Physically reaching a later destination may be allowed before the player can extract, process, export, or safely return with its progression material.
- Player-facing failures must name concrete route, vehicle, environmental, payload, infrastructure, or operation requirements rather than an unexplained destination tier.

The reusable access contract is resolved. Flight formulas remain provisional until implementation experiments, and progression protection still requires concrete route evidence in Define Flight Progression Balance Invariants. Resolving this ticket does not establish that all ten tiers are balanced.

## Constraint Design Rules

- Constraints derive from authored celestial, environmental, route, vehicle, payload, or infrastructure facts. Destinations do not receive unexplained tier locks.
- The same input must produce the same consequence everywhere. A new constraint must not exist only to give one destination a progression niche.
- One capability should answer a reusable family of conditions and normally unlock or improve multiple routes or operations.
- A mission evaluates only the constraints relevant to its route, payload, endpoints, and intended operation.
- Route feedback must name the exact transition being evaluated, such as reaching the target orbit, landing on the target, taking off from the target, reaching the return orbit, or landing at the return destination. Avoid generic labels such as `destination reachable`, `arrival possible`, `local departure`, or `return route possible`.
- The planner shows only transitions that belong to the selected mission. An orbit-only mission does not display landing or surface takeoff checks.
- Candidate constraints are not automatically Alpha requirements. They enter scope only when concrete destination content justifies a reusable gameplay system.

## Candidate Constraint Catalogue

| Constraint family | Physical or systemic source | Access affected | Natural consequence | Possible response | Current standing |
|---|---|---|---|---|---|
| Transfer energy | Relative orbits and route geometry | Outbound and return travel | Required delta-v changes with the selected route | Propulsion, staging, refueling, alternate route | Foundation |
| Transfer duration | Trajectory, distance, and selected transfer energy | Route selection | A route exceeding the permitted real-time mission duration is unavailable; spending more delta-v may make a faster route possible | Faster trajectory, stronger vehicle, or tuned celestial layout | Foundation |
| Surface gravity | Body mass and radius | Landing, ascent, return | Required acceleration, landing energy, and ascent delta-v increase | Higher thrust, suitable landing system, orbital infrastructure | Foundation |
| Atmosphere | Surface pressure and authored drag coefficient | Landing and ascent | Atmosphere increases ascent delta-v and reduces the powered braking delta-v required for landing | More vehicle delta-v for ascent; atmospheric braking for landing | Foundation |
| Endpoint form | Surface, orbit, station, or remotely managed object | Arrival, transfer, departure | A vehicle needs a compatible way to land, dock, or transfer cargo | Landing system, docking capability, Hammer, local infrastructure | Foundation |
| Thermal environment | Solar flux, atmosphere, albedo, and rotation | Crewed presence and infrastructure after arrival | The destination exposes the mission to a temperature hazard | Player-facing advisory; later protection or infrastructure response | Advisory |
| Radiation environment | Solar exposure, radiation belts, atmosphere, and magnetosphere | Crewed presence and infrastructure after arrival | The destination exposes the mission to a radiation hazard | Player-facing advisory; later shielding or remote-operation response | Advisory |
| Illumination cycle | Rotation, orbit, and occlusion | Power generation and sustained operation | Solar generation varies by location and time | Storage, alternate power, orbital placement | Candidate |
| Particulate environment | Rings, belts, debris, dust, and local impact activity | Vehicles and persistent infrastructure | Impacts or abrasion increase risk or upkeep | Shielding, redundancy, maintenance | Candidate |
| Atmospheric weather and chemistry | Atmospheric composition and dynamics | Surface landing and operation | Storms, corrosion, or suspended dust constrain equipment | Sealing, compatible materials, protected infrastructure | Candidate |
| Terrain and substrate | Surface generation and material properties | Landing, construction, extraction | Suitable sites and equipment vary with terrain | Site choice, landing equipment, specialized construction | Candidate |

## Environmental Hazard Advisories

- Temperature and radiation do not affect orbital route feasibility or `Landing possible` in the current Alpha direction.
- A celestial object's Star Map information presents environmental hazards as factual properties of that object or location without evaluating a mission.
- A flight-planning or dispatch screen evaluates those properties against the concrete selected vehicle, the traveling player's equipped protection, and any other mission-relevant protection that actually exists.
- The planner retains one visible triangular environmental-status indicator. Red represents a critical state, yellow a warning state, and green means every relevant environmental property is currently handled.
- Environmental status does not make the underlying maneuver physically impossible. For a manual launch, a red state is shown prominently and requires acknowledgement, after which the player may continue and the resulting gameplay consequences, including vehicle destruction, occur normally.
- The indicator remains hoverable in every state. Its tooltip summarizes all relevant properties, their protection checks, and which protections are satisfied or missing.
- This evaluation uses concrete mission state and equipment rather than inferring a general player technology tier.
- Exact exposure consequences and infrastructure responses remain open until their gameplay systems are designed.

## Warning Versus Physical Feasibility

- Environmental danger and physical maneuver feasibility are separate outcomes.
- A warning means the maneuver can occur but exposes the mission to a consequence.
- A failed physical check means the vehicle cannot perform that maneuver in its current state. The game does not need to invent an explosion or other punishment.
- Manual input does not have to be disabled for every physical failure. For example, a rocket with insufficient thrust-to-weight ratio may ignite but remain on the surface because it cannot lift off.
- Planned feasibility and execution-time world conditions are separate checks. The Star Map planner evaluates the selected vehicle, endpoints, and route; actual execution evaluates current local conditions such as the launch structure, landing site, and unobstructed movement path.
- A locally blocked maneuver does not invalidate the planned route. The asset enters a concrete blocked or waiting state and emits an event through [[Define Team Notification System]].
- Automatic retry and recovery policy belongs to [[Define Space Transport Dispatch Model]].
- Environmental hazards are currently expected to be stable authored properties. Creating a dispatcher route counts as accepting the known hazard state, so automated missions do not need a recurring `Allow critical hazards` control.
- If hazards later become dynamic, automatic-dispatch policy must be revisited.
- A vehicle that cannot execute its configured mission reports the blocked or failed state through [[Define Team Notification System]].

## Atmospheric Entry and Ascent

- Atmosphere is a reusable mission constraint rather than a destination-specific gate.
- Atmosphere increases the delta-v required for surface ascent through drag.
- Atmosphere reduces the powered braking delta-v required for landing.
- Airless bodies avoid ascent drag but require fully powered landing.
- Alpha does not model atmospheric composition, entry heating, corrosion, or engine-atmosphere interaction for mission feasibility.
- A surface-to-surface mission is evaluated as three distinct phases: surface ascent to parking orbit, orbital transfer between parking orbits, and destination entry and landing.
- The Lambert transfer planner evaluates only the orbital-transfer phase. Local gravity and atmosphere affect the endpoint phases instead.
- Reaching a destination's orbit does not imply that the current vehicle can enter its atmosphere or land on its surface.
- The player-facing planner combines atmospheric entry and touchdown into one concrete `Landing possible` result. Its tooltip breaks the result down into atmospheric braking, remaining powered braking, local gravity, and available propellant rather than exposing several overlapping top-level statuses.
- The current celestial model already authors local gravity, surface pressure, and a Star Map atmospheric-drag multiplier.
- Atmospheric flight difficulty uses surface pressure as a physical input and may include an explicitly authored, non-physical balance coefficient such as the current Star Map atmospheric-drag multiplier. The exact formula remains open for implementation prototyping.
- Alpha derives one shared atmospheric delta-v adjustment from surface pressure and the authored drag coefficient. The same adjustment is added to ascent delta-v and subtracted from powered landing delta-v; the two directions do not have separate balance multipliers.
- Atmospheric braking cannot reduce required powered landing delta-v below zero.
- Surface ascent and landing do not share a mirrored base delta-v cost. Ascent must always be substantially more demanding than landing on the same body, including on an airless body.
- The base ascent and base landing calculations remain separate and may both use local gravity, body radius, and parking-orbit data. Their exact formulas and ratio remain open for implementation prototyping.
- Surface ascent requires both sufficient propellant and sufficient thrust-to-weight ratio to produce positive acceleration against local gravity.
- Surface ascent and powered landing are finite-duration maneuvers. Their burn duration affects propellant demand because the vehicle continues fighting local gravity while thrusting.
- Powered landing must verify that the vehicle can generate sufficient deceleration before touchdown; available delta-v alone is not enough. Atmospheric braking reduces the powered portion of this requirement.
- Alpha may prototype these surface maneuvers with a bounded iterative calculation: derive ideal maneuver delta-v, calculate burn duration and changing vehicle mass, add gravity losses from that duration, and repeat until the result stabilizes or fails to converge.
- Galaxia should use the most physically grounded model that remains computationally and operationally practical. Expensive trajectory detail may be approximated, but only where the more realistic calculation would create meaningful cost or complexity.
- Performance must be measured with a representative development save before optimizing this calculation. Do not add speculative caching or reduce model fidelity without profiling evidence.
- The current orbital planner does not use those facts for surface ascent, atmospheric entry, or landing feasibility. Rocket ascent and landing in the dimension are currently movement behavior rather than mission-planning calculations.
- The exact reusable entry, landing, and ascent calculation remains open.

## Mission Duration Constraint

- Galaxia measures transfer time internally in orbital simulation units. In the current model one OSU equals one server tick, and `TransferRoute.tofSeconds()` converts twenty OSU to one real second.
- Mission duration uses real seconds. It does not introduce simulated days, life-support days, or a separate endurance-resource model.
- A candidate route whose transfer duration exceeds the permitted maximum is rejected with a concrete `Mission too long` reason.
- The duration constraint participates in route selection. The planner must choose among routes that satisfy both the vehicle's delta-v envelope and the duration limit rather than select a route first and reject it afterward.
- A weak vehicle may have enough delta-v for a slow transfer but fail the duration limit. A stronger vehicle may spend more delta-v on a faster transfer and pass the same limit.
- The initial Alpha maximum transfer duration is 180 real seconds for mission types subject to the duration limit.
- Crewed Rockets, cargo Rockets, and crewed Spaceships provisionally use the 180-second maximum.
- Unmanned Spaceship missions are exempt from this maximum and may use substantially slower transfers.
- Hammer uses its own route constraints and is expected to occupy the fast-transport role rather than rely on the universal mission-duration rule.
- This vehicle split is a working Alpha rule and may change when acceleration research, route behavior, or concrete balance findings demonstrate a need.
- When no valid route fits the limit, the planner reports `Mission too long` and the calculated transfer duration. Exact final UI copy remains open.

## Provisional Orbital Burn Feasibility

- The Alpha route search provisionally uses impulsive Lambert candidates with fixed candidate transfer times.
- For each candidate, the current single-stage vehicle calculates departure and capture burn duration from thrust, specific impulse or exhaust velocity, changing mass, available propellant, and required delta-v.
- Each burn is compared with the local orbital dynamic timescale `sqrt(r^3 / mu)`. A candidate is feasible only when its burn duration remains below a configurable fraction of that timescale.
- The fraction is a balance parameter and remains undecided.
- Burn duration does not extend or redefine the candidate transfer time. The 180-second mission-duration rule evaluates the candidate transfer time separately.
- Full continuous-thrust trajectory optimization is outside the provisional Alpha model. Caching or other performance changes require evidence from representative profiling.
- Alpha provisionally treats orbital cruise between maneuver burns as unpowered coasting with no propellant consumption. Propellant is consumed by surface ascent, transfer departure, capture, and powered landing burns.
- Continuous low-thrust cruise would require a separate propulsion and trajectory model and is not part of this provisional Lambert-based rule.
- Before this rule can drive gameplay, the vehicle capability model needs internally consistent single-stage mass, thrust, propellant, and engine data.
- This is a working Alpha model. Implementation findings may replace it if the approximation produces unsuitable behavior.

## Existing Orbital Tuning Levers

- Central-body gravitational parameter and orbital semi-major axes affect orbital speed, transfer duration, and required delta-v together.
- Orbital eccentricity and phase affect transfer geometry and available routes.
- Planetary gravity and radius can affect local landing, ascent, and orbit requirements independently from the star-centered transfer.
- The current `orbitSpeed` magnitude is not an independent speed control when a positive gravitational parameter is present; orbital speed is derived from gravity and orbital radius. Its sign still selects orbital direction.
- Celestial rendering size currently contributes to a transfer periapsis constraint and should not be treated as an intentional balance lever.

## One-Way Mission

A mission is one-way when its current vehicle, route, and available infrastructure allow the planned arrival but do not currently provide every transition needed for a return.

- A crewed one-way mission remains possible but displays a central confirmation dialog before launch. The player must explicitly acknowledge the missing return capability.
- A cargo-only one-way mission remains possible and shows a yellow warning triangle. Hovering it explains that the mission is one-way and identifies the unavailable transition; it does not require a confirmation dialog.
- One-way status is not a permanent destination lock. Early cargo missions may deliberately deliver the equipment and materials needed to establish refueling or other return infrastructure for later missions.
- The planner evaluates current vehicle capability and existing infrastructure. Materials that a player might later assemble into return infrastructure do not silently count as an available return path.
