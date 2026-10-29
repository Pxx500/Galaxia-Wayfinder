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

# Destination Access Levels

## Accepted Decision

Destination access is evaluated for a concrete mission and operation, not stored as a tier, linear access state, `landed` flag, universal `operational` state or whitelist. Reaching a body does not prove ability to extract, process, export or return. Failures name concrete missing route, vehicle, environmental, payload, infrastructure or operational requirements.

Constraints come from authored facts and apply consistently everywhere. A reusable capability should answer a family of conditions, normally improving multiple routes. New constraints require concrete content justification, not a one-destination progression niche. This contract is resolved, not proof that all ten Ore Tiers are balanced.

## Separate Outcomes

- Physical reachability, mission viability, operations after arrival, export and return are separate.
- Feedback names exact selected transitions, such as reaching target orbit, landing, taking off or landing at the return destination. Orbit-only plans do not show irrelevant surface checks.
- [[Define Vehicle Capability and Route Requirements]] owns concrete single-stage vehicle and explanation requirements. [[Define Rocket Route Fuel Budgets]] owns actual-fuel delta-v allowances and candidate selection.
- Planned route feasibility and execution-time local conditions differ. A blocked structure, landing site or movement path puts the asset in a concrete blocked/waiting state and emits a team event, not retroactive route invalidity. [[Define Space Transport Dispatch Model]] owns retry.

## Environmental Advisories

Temperature and radiation do not change orbital feasibility or `Landing possible` in current Alpha. Object information states factual hazards. Planning evaluates them against the selected vehicle, traveling player's equipped protection and other existing relevant protection, not player technology tier.

Use one hoverable triangular status: red critical, yellow warning, green all relevant environmental conditions handled. Hover summarizes properties, protection checks and satisfied/missing protection.

A manual red launch requires prominent acknowledgement but remains possible, with normal consequences including destruction. A physically impossible maneuver instead fails for its concrete reason, without an invented punishment. Manual ignition may still be allowed when insufficient thrust simply leaves the Rocket on the ground.

Hazards are currently stable authored facts. Creating an automated route accepts them, without a repeated `Allow critical hazards` option. Revisit policy if hazards become dynamic. Exact exposure consequences and protection/infrastructure systems remain open.

## Atmosphere, Ascent And Landing

A surface-to-surface mission has separate ascent-to-parking-orbit, orbital transfer and entry/landing phases. Lambert evaluates only the transfer. Reaching orbit does not imply surface access.

- Atmosphere adds ascent delta-v and reduces powered landing delta-v. Airless landing is fully powered.
- Use one shared atmospheric adjustment derived from pressure and authored drag coefficient. Add it on ascent and subtract it on landing, never below zero. Do not add separate directional balance multipliers.
- Ascent and landing have separate base calculations. Ascent must be substantially harder even on an airless body. Gravity, radius and parking orbit may inform both. Exact formulas and ratio remain open.
- Takeoff requires enough propulsion supplies and thrust-to-weight for positive acceleration against local gravity.
- Surface burns have finite duration and gravity losses. Powered landing also needs sufficient deceleration before touchdown, not delta-v alone. Atmospheric braking reduces the powered portion.
- Present one `Landing possible` result. Its tooltip breaks down atmospheric braking, powered braking, local gravity and propellant.
- Alpha feasibility excludes composition, entry heating, corrosion and engine-atmosphere interaction.
- Prefer the most physically grounded practical model. A bounded iteration of ideal delta-v, duration/changing mass and gravity losses is a prototype option, not a selected exact formula.
- Measure with a representative development save before adding caching or sacrificing fidelity. Exact surface calculation remains open.

## Working Mission Duration Rule

One orbital simulation unit currently equals one server tick. `TransferRoute.tofSeconds()` converts 20 OSU to one real second. Duration uses real seconds, not simulated days or a new endurance resource.

The provisional maximum transfer duration is 180 seconds for crewed Rockets, cargo Rockets and crewed Spaceships. Unmanned Spaceships have no maximum and may use slow bulk routes. Hammer has its own constraints and fast-transport role.

Filter candidates by duration and actual delta-v/vehicle feasibility before choosing. A weak vehicle may afford only a slow route that fails duration, while a stronger one can afford a faster route. If none qualify, show the localized `Mission too long` reason and calculated duration.

The vehicle split and 180-second value are balance-sensitive, not final route validation.

## Provisional Orbital Burn Model

Use impulsive Lambert candidates with fixed transfer times. For the current single-stage vehicle, calculate each departure/capture burn from thrust, Isp/exhaust velocity, changing mass, propellant and delta-v. Compare burn duration with a configurable fraction of local `sqrt(r^3 / mu)`. The fraction remains undecided.

Every required maneuver must pass. Burn duration does not extend candidate transfer time, which is checked separately against mission duration. Cruise is provisionally unpowered coasting. Propellant is consumed in ascent, departure, capture and powered landing.

Continuous-thrust optimization and low-thrust cruise require another model and are outside this provisional choice. Internally consistent vehicle data and measured practical behavior are required before gameplay use. Implementation findings may replace this approximation.

## Other Constraint Candidates

Transfer energy, duration, surface gravity, atmosphere and endpoint form are foundations. Thermal/radiation hazards are advisories. The following are candidates only, not automatic Alpha requirements:

- Illumination/occlusion affecting power and storage
- Particulates, debris and abrasion affecting upkeep
- Atmospheric weather/chemistry affecting protected operation
- Terrain/substrate affecting sites, construction and extraction

## Orbital Tuning Facts

Central gravity and semi-major axes affect speed, duration and delta-v together. Eccentricity/phase change geometry. Local body gravity/radius affect endpoint maneuvers independently from star-centered transfer.

With positive attractor gravity, `orbitSpeed` magnitude is not an independent speed control, although its sign chooses direction. Rendering size currently enters a periapsis constraint and is not an intentional balance lever.

## One-Way Missions

A one-way mission has feasible planned arrival without every currently available return transition.

- Crewed missions require a central acknowledgement dialog before launch.
- Cargo-only missions show a yellow hover warning naming the unavailable return transition, without a dialog.
- Delivered infrastructure can enable later return, but materials the player might build later do not count as currently available infrastructure.
- [[Define Rocket Missions Without Recovery]] separately permits an intentional terminal ending with a disappearance warning. A missing recovery plan is not the same as an occupied feasible pad.

## Implementation Boundary And Related Decisions

The inspected planner did not calculate surface ascent, entry or landing from authored gravity, pressure and drag. In-dimension Rocket movement did not establish mission-planning feasibility. The prototype gap is dated in [[Define Vehicle Capability and Route Requirements]], not a current audit.

- [[Define Flight Progression Balance Invariants]]
- [[Define Alpha Transport Roles]]
- [[Define Team Notification System]]

## Gameplay Flow

The player plans a concrete mission and sees whether its selected transitions are feasible, including separate surface checks when relevant. Environmental advisories compare hazards with the selected vehicle and equipped protection. A critical manual launch requires acknowledgement but may proceed.

Arrival alone does not guarantee operation, export or return. A crewed one-way mission requires acknowledgement, while cargo-only missions show a warning. Local obstructions encountered during execution produce a blocked or waiting state and a team event.
