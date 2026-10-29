---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
blocked_by: []
claimed_by: null
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Rocket Route Fuel Budgets

## Mission Routes

Rocket missions use place, action and route tiles. Connecting two places creates the route tile. Each route has a player-set delta-v allowance and a fuel-efficiency or speed priority. This extends Vehicle Schedules in [[Define Space Transport Dispatch Model]], not a separate Flight Plan.

Actual propulsion resources, current mass and propulsion determine usable delta-v. Forecasts guide planning. Departure checks enforce the allowance against the actual target and vehicle.

## Budget And Candidate Selection

- Each allowance caps all propulsive delta-v for the route, including ascent, departure, capture and landing where applicable. There is no unbudgeted landing charge. Wait if no feasible candidate fits.
- Before departure, usable delta-v must cover all remaining allowances through the next replenishment or mission end. Actual servicing must supply the resources. Tank capacity is not fuel, freight fluids are not propulsion supplies, and oxidizer and provisional coolant are checked independently.
- Recalculate after replenishment, changes to engines, propellant or structure, or capability loss. Include the closing leg and last-to-first boundary of a loop. Without replenishment, only finitely many laps are covered.
- An allowance is not a separate tank or fuel burned in advance. Unused propellant stays aboard without automatically increasing later allowances.
- For unchanged propulsion and structural mass, usable delta-v is effective exhaust velocity multiplied by `log(current mass / terminal mass after usable propellant is exhausted)`. Actual successive burns subtract their delta-v, using a consistent consumable-mixture model. Covering summed allowances preserves coverage of remaining allowances, but does not prove adequate thrust, maneuver time, departure windows or endpoint compatibility.
- Fuel-efficiency priority minimizes delta-v among eligible candidates. Speed priority minimizes transfer time. Apply the cap, vehicle feasibility and vehicle-class duration rule before ranking. The cap controls waiting for a later window. There is no player-configured duration limit.
- Retain alternatives needed for individual burns, duration and vehicle feasibility. The minimum-total-delta-v sample can discard the only feasible candidate. Compression by total delta-v and duration alone requires every relevant constraint to be monotonic in those dimensions.
- Fuel left after a cheap leg preserves usable delta-v but can lengthen finite burns or change thrust-to-weight feasibility. Guidance states and refreshes its assumed vehicle condition. Burns consume real resources, not a fixed liters-per-delta-v coefficient.
- The active flight retains its trajectory and maneuver obligations. Reloading neither rerolls travel nor charges fuel twice. An occupied pad does not recalculate interplanetary travel. The Rocket arrives and waits with maneuver fuel intact, rather than being disposed of.

## Route Forecasts

Forecasts contain orbital delta-v candidates and transfer durations. Local maneuvers and gravity losses are evaluated for the actual Rocket. The Star Map uses the shared planner. OrbitalMechanics owns motion, while the vehicle owns resources, allowances and execution.

For the selected allowance, guidance estimates percentage of time available and/or approximate maximum wait in seconds. Availability measures qualifying time, not window count. Time until the next window is separate. Loading, replenishment, maintenance and pad occupancy are excluded.

| Motion relative to the transfer attractor | Treatment |
| --- | --- |
| Local same-body transitions | Evaluate applicable ascent, landing and docking rather than treating an interplanetary-planner rejection as a movement ban |
| Planar circular planets around one star or sibling moons around one planet | Complete relative-phase cycle under the current rotation-invariant planar model |
| Equal signed angular speeds | Actual fixed relative phase, not hypothetical phases |
| Opposite directions | Signed relative angular speeds |
| Selected asteroids in the current rigid SOL belt | Shared source-radius, target-radius and fixed-separation table, without an evolving time axis |
| Circular planet and supported belt | Shared representative-radius phase family |
| Two supported circular belts, when needed | Shared family covering both radii, including mixed inner/outer combinations, not all asteroid pairs |
| Planet to another planet's moon, hierarchical moon to asteroid, eccentric or nested motion | Bounded actual phase-path forecast or explicitly unavailable data |
| Different star systems | Require a supported route/attractor model before applying any forecast formula |

For circular motion, `phi(t) = phi_0 + (omega_B - omega_A) * t`. Unequal signed speeds repeat after `2*pi / abs(omega_B - omega_A)`. Equal speeds give fixed geometry. Use effective OrbitalMechanics speeds. With positive attractor gravity, authored orbitSpeed magnitude is not independent orbital speed.

A hierarchical route repeats only when all relevant phases repeat in the same frame. A near alignment or floating-point least common multiple is not proof. Preserve direct Overworld-to-Callisto travel rather than substituting Jupiter or requiring a parent-orbit stop. Inclination support would require reclassifying the current planar assumptions.

For a proven periodic profile, measure availability over the full cycle and include gaps crossing its boundary. For bounded forecasts, state coverage and longest observed gap without joining the ends or presenting an unfinished trailing gap as a finite maximum. No qualifying samples means no window found in that coverage, not permanent impossibility. Missing, stale, incompatible or invalid data make estimates unavailable, not zero-percent availability or zero-cost travel.

## Shared Asteroid Approximation

- Planet-to-belt profiles use inner, middle and outer representative radii with the actual belt's shared angular speed. They are numerical geometries, not registered bodies. Recomputing Keplerian speed per radius models a different belt.
- Query or interpolate candidate/phase costs at the asteroid's actual radius and angular offset before deriving affordability or statistics. Do not interpolate final percentages or longest waits.
- In a complete single-phase cycle, initial angle changes next-window timing but not full-cycle availability or longest gap. Equal speeds require the actual fixed phase.
- Edge samples do not bound interior cost: solver branches, invalid trajectories and candidate changes can produce interior extrema. Midpoints improve estimates without proving conservative bounds. Compare margins with denser references.
- Same-belt data use representative source radius, target radius and fixed separation. Add cross-belt families only when a second generated belt is used.
- Hierarchical asteroid routes need extra phase axes. A planet-belt phase shift does not preserve an independent moon phase. Follow the selected target's actual phase path through baked data without gameplay profile generation.
- Keep A-to-B and B-to-A directional. Equivalent station body geometry may share the orbital component, not local maneuvers or endpoint compatibility. Runtime body references remain CelestialObjectKey values.

## Prebaked Data And Builds

Generate forecasts before release and package them with the mod. Runtime queries phases and tables and validates departure exactly. It does not generate, extend or repair geometry profiles, and discovery or map visibility triggers no bulk calculation. Cached geometry does not prove a target still exists.

Ordinary builds compare canonical inputs with the baked output fingerprint in a tracked, Gradle configuration-cache-compatible task. Deterministically encode and order celestial geometry, attractor gravity, clearance, physics, units, sampling and solver/generator identity.

- Unchanged inputs reuse current data without sampling. Changed or missing data warn in the build console and offer a yes/no regeneration choice.
- An explicit build answer overrides prompting. Pre-decline skips generation and prompting, not freshness checking. A declined development build may continue with stale or missing forecasts disabled and exact validation available. Current data remain usable. Never fingerprint stale output as new.
- A noninteractive stale development build without an explicit answer fails with actionable yes/no-argument guidance, rather than hanging or silently approving generation.
- Every GitHub release noninteractively generates, verifies and packages fresh data. Decline cannot bypass this. Failed generation or verification blocks publication.
- Arbitrary server epochs use phase-dependent data, not a file valid only at bake time. There is no runtime-generation fallback or legacy reader.
- Share a headless numerical definition source or incremental export with the game-owned catalog. Do not initialize the game on every build, parse arbitrary Java expressions with regex, or maintain a manually copied second catalog.

Direct circular pairs and sibling moons need one phase, Overworld-to-Callisto two, and moons of different planets generally three. Multidimensional cell percentages are not time availability. Follow the actual route's phase evolution over a stated interval. Interpolation must not merge unrelated solver branches into fictitious candidates or turn invalid samples into free flights.

## Open Numerical Work

Sampling density, bounded coverage, candidate retention, compression, accuracy margins, work quotas, data size and build-argument spelling remain open. Measure costs and compare representative families with denser references, especially narrow windows, interior radii, branch transitions and invalid regions. Do not generate every asteroid pair or add a dense uniform grid without measured need.

Numerical checks need to preserve rotation and cycle behavior, signed/equal speeds, censored and wraparound gaps, both belt directions, feasible slower or individual-burn alternatives, exact cap enforcement, changed propulsion state, partial servicing, loop closure and active-flight persistence.

## Implementation Evidence And Provenance

At commit `a9128e9e` on 2026-10-07, `OrbitalTransferPlanner.computeRoute` evaluated 64 durations and two Lambert branches, selecting before vehicle evaluation. It did not implement vehicle-aware budgets or window guarantees. The Rocket prototype used nominal fuel capacity and hardcoded Isp. The generated SOL field's resolver used world-origin phase and velocity, so its rigid simplification does not establish support for an offset star.

The budget, forecast and release-data decisions date to 2026-10-07. Later decisions require noninteractive stale builds to fail without an explicit answer. Earlier liter controls, fastest-only selection and runtime-generation proposals are superseded.

## Gameplay Flow

The player connects places in a Rocket mission, sets a delta-v allowance for each route and chooses fuel efficiency or speed. Forecasts help them judge availability and waiting, while departure checks the actual vehicle, resources and target. If no feasible route fits the allowance, the Rocket waits.

The player supplies enough propulsion resources for the remaining allowances through the next replenishment or mission end. Unused propellant stays aboard, and an occupied arrival pad makes the Rocket wait rather than discard it.
