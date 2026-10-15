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

# Define Rocket Route Fuel Budgets

## Accepted Decision

Rocket missions use place, action and route tiles. Connecting two places creates the route tile. Each route has a player-set delta-v allowance and a fuel-efficiency or speed priority. This extends Vehicle Schedules in [[Define Space Transport Dispatch Model]], not a separate Flight Plan.

The Rocket stores actual propulsion resources. Its current mass and propulsion convert those supplies into usable delta-v. Forecasts guide planning, while authoritative departure checks enforce the allowance against the real target and vehicle. Accepted design is not implemented or benchmarked behavior.

## Budget And Candidate Selection

- Each allowance caps the route's complete propulsive delta-v, including applicable ascent, departure, capture and landing. There is no extra unbudgeted landing charge. If no feasible candidate fits, wait.
- Before departure, usable delta-v must cover all remaining allowances through the next replenishment or mission end. Tank capacity is not available fuel. Actual servicing must supply the planned resources. Check companion oxidizer and provisional coolant independently. Freight fluids are not propulsion supplies.
- Recalculate after replenishment, engine or propellant changes, structural changes or capability loss. For loops include the closing leg and last-to-first boundary. Without replenishment only finitely many covered laps are possible.
- An allowance is neither a separate tank nor fuel burned in advance. Unused propellant remains aboard. Later allowances do not automatically increase.
- For unchanged propulsion and structural mass, usable delta-v is effective exhaust velocity multiplied by `log(current mass / terminal mass after usable propellant is exhausted)`. Actual successive burns subtract their delta-v, using a consistent consumable-mixture model. Covering summed allowances preserves coverage of remaining allowances, but does not prove adequate thrust, maneuver time, departure windows or endpoint compatibility.
- Fuel-efficiency priority minimizes delta-v among currently eligible candidates. Speed priority minimizes transfer time among them. Apply the cap, vehicle feasibility and vehicle-class duration rule before ranking. The cap controls waiting for a later window. No player-configured duration limit is added.
- Retain candidate alternatives needed by individual burns, duration and vehicle feasibility. A minimum-total-delta-v sample can lose the only feasible candidate. Compressing candidates on total delta-v and duration alone is valid only if every relevant constraint is monotonic in those dimensions.
- Extra fuel retained after a cheap leg preserves usable delta-v but can lengthen finite burns or alter thrust-to-weight feasibility. Guidance states its assumed vehicle condition and refreshes when it changes. Actual burns consume real resources, not a fixed liters-per-delta-v coefficient.
- Once launched, the chosen trajectory and maneuver obligations stay with the active flight. Reloading does not reroll travel or charge fuel twice. An occupied pad does not recalculate interplanetary travel. The Rocket arrives and waits there with remaining maneuver fuel intact. Waiting is not intentional disposal.

## Forecast Contract

Forecast data contain universal orbital delta-v candidates and transfer durations. Vehicle-dependent local maneuvers and gravity losses are evaluated for the actual Rocket. The Star Map consumes the shared planner's results rather than implementing another evaluator. Motion belongs to OrbitalMechanics. Resources, allowances and execution belong to the vehicle.

Guidance responds to the selected allowance with estimated percentage of time available and/or approximate maximum waiting in seconds. Availability is qualifying time, not a count of windows. Time until the next window is a separate metric. Loading, replenishment, maintenance and pad occupancy are excluded from orbital availability.

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

For a proven periodic profile, availability covers the full cycle and longest waiting includes a gap crossing its boundary. For bounded forecasts, state coverage and longest observed gap, do not join the ends, and do not present an unfinished trailing gap as a finite maximum. No qualifying samples means no window found in that coverage, not permanent impossibility. Missing, stale, incompatible or invalid data mean unavailable estimates, never zero-percent availability or zero-cost travel.

## Shared Asteroid Approximation

- Planet-to-belt profiles use inner, middle and outer representative radii with the actual belt's shared angular speed. These are numerical geometries, not registered phantom bodies. Keplerian speeds recomputed per radius would model a different belt.
- Query or interpolate candidate/phase costs at the selected asteroid's real radius and angular offset before deriving affordability or statistics. Do not interpolate final percentages or longest waits.
- In a complete single-phase cycle, initial angle changes next-window timing but not full-cycle availability or longest gap. Equal speeds require the actual fixed phase.
- Edge samples do not bound interior cost. Solver branches, invalid trajectories and candidate changes can produce interior extrema. Midpoint coverage improves estimates without proving conservative bounds. Any margin needs comparison with denser reference calculations.
- Same-belt data use representative source radius, target radius and fixed separation. Add cross-belt families only when a second generated belt is used.
- Hierarchical asteroid routes require their extra phase axes. A simple planet-belt phase shift does not preserve an independent moon phase. Follow the actual selected target's phase path through baked data without gameplay profile generation.
- Keep A-to-B and B-to-A directional. Equivalent station body geometry may share the orbital component, not local maneuvers or endpoint compatibility. Runtime body references remain CelestialObjectKey values.

## Prebaked Data And Builds

All forecast generation is prebaked and packaged with the mod. Runtime performs inexpensive phase/table queries and exact departure validation, not geometric-profile generation, extension or repair. Discovery and map visibility trigger no bulk calculations. Cached geometry does not prove that a target still exists.

Ordinary builds cheaply compare canonical route-calculation inputs with the fingerprint stored for the actual baked output. Include celestial geometry, attractor gravity, clearance, physics, units, sampling and solver/generator identity with deterministic encoding and ordering. Run this check in a tracked task compatible with Gradle configuration cache, not configuration alone.

- Unchanged inputs reuse current data without sampling.
- Changed or missing data produce a build-console warning and a yes/no regeneration choice.
- An explicit build answer overrides prompting. A pre-decline argument skips generation and prompting, not freshness checking.
- A declined development build may continue. Missing or stale forecasts are disabled, but exact flight validation remains available. Current data remain usable. Never fingerprint stale output as newly generated.
- A noninteractive stale development build without an explicit answer fails with actionable yes/no-argument guidance. It must not hang or silently approve expensive work.
- Every GitHub release noninteractively generates, verifies and packages fresh data. Decline cannot bypass this. Failed generation or verification blocks publication.
- Arbitrary server epochs use phase-dependent data, not a file valid only at bake time. There is no runtime-generation fallback or legacy reader.
- Share a headless numerical definition source or incremental export with the game-owned catalog. Do not initialize the game on every build, parse arbitrary Java expressions with regex, or maintain a manually copied second catalog.

Direct circular pairs and sibling moons need one phase, Overworld-to-Callisto two, and moons of different planets generally three. Multidimensional cell percentages are not time availability. Follow the actual route's phase evolution over a stated interval. Interpolation must not merge unrelated solver branches into fictitious candidates or turn invalid samples into free flights.

## Open Numerical Work

Sampling density, bounded coverage, candidate retention, compression, accuracy margins, work quotas, data size and exact build-argument spelling remain implementation choices. Measure costs and compare representative families with denser references, especially narrow windows, interior radii, branch transitions and invalid regions. Do not generate every asteroid pair or add a dense uniform grid without measured need.

Numerical checks need to preserve rotation and cycle behavior, signed/equal speeds, censored and wraparound gaps, both belt directions, feasible slower or individual-burn alternatives, exact cap enforcement, changed propulsion state, partial servicing, loop closure and active-flight persistence.

## Implementation Evidence And Provenance

At commit `a9128e9e` on 2026-10-07, `OrbitalTransferPlanner.computeRoute` evaluated 64 durations and two Lambert branches, selecting before vehicle evaluation. It did not implement vehicle-aware budgets or window guarantees. The Rocket prototype used nominal fuel capacity and hardcoded Isp. The generated SOL field's resolver used world-origin phase and velocity, so its rigid simplification does not establish support for an offset star.

Direct owner decisions on 2026-10-07 establish delta-v allowances, selectable priorities, estimated availability/waiting, representative belt families, fully prebaked generation, optional developer decline and compulsory fresh release data. Noninteractive stale builds without an explicit answer were subsequently resolved to fail. Earlier liter controls, fastest-only selection and runtime-generation proposals are superseded.
