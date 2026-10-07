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

## Question

How should per-route delta-v limits make multi-leg Rocket missions predictable despite changing orbital geometry, and what cost and departure-window guidance can the planner honestly provide?

## Owner Direction

On 2026-10-07 the owner established a mission composed of place, action and route tiles. Connecting two place tiles automatically generates the route tile between them. Their subsequent resolution uses universal orbital delta-v requirements and a delta-v allowance on each route. The Rocket stores real fuel, which its current propulsion and mass model converts into usable delta-v. Summed remaining allowances are compared with that capability. The player chooses fuel-efficiency or speed priority for the flight.

This extends the existing Vehicle Schedule, Travel Block and Visit Block concepts in [[Define Space Transport Dispatch Model]]. It does not introduce a separate Flight Plan artifact. The owner accepted the forecast model below, including shared belt approximations and the distinction between estimates and authoritative departure checks.

## Accepted Availability Guidance

On 2026-10-07 the owner clarified that guidance responds to the selected route allowance, finalized as delta-v. The intended player-facing metrics are approximately what percentage of time the route is available at that allowance, or approximately the maximum wait in seconds for a qualifying departure window. A fixed 25-percent delta-v threshold is not the desired player-facing control.

Availability means a feasible departure fits the selected delta-v allowance and the route's other applicable constraints. The percentage describes the share of forecast time that qualifies, not the number of separate windows. Maximum forecast waiting describes the longest continuous interval without a qualifying departure. It is distinct from the wait until the next window from the current time.

These values are estimates based on the available forecast. Sparse samples do not establish a global maximum wait or prove permanent impossibility. A forecast that ends before a qualifying window cannot supply a finite maximum for that unfinished interval. Exact presentation, forecast coverage and sampling resolution remain implementation-time work.

## Accepted Contract

- A limit caps the route's complete propulsive delta-v expenditure. If no currently feasible route fits, the vehicle waits rather than exceeding the player's limit.
- Budget totals are checked against delta-v derived from actual usable propulsion supplies. Recompute after refueling or a propulsion-state change. Surface ascent, transfer burns and landing must all be covered when present in the scheduled route.
- Sufficient total fuel does not prove that departure windows exist or that all vehicle and endpoint requirements are satisfied.
- Cached orbital candidates store universal delta-v requirements and transfer durations. The actual Rocket supplies usable delta-v and maneuver feasibility. Vehicle-dependent local maneuvers and gravity losses are evaluated for that Rocket rather than baked into a universal orbital profile.
- Cached estimates can guide the player. The authoritative departure calculation still verifies the chosen route against current conditions, actual fuel and the configured cap.
- A sampled time interval supports estimated costs and departure windows within that interval. No sampled route is not proof that the route will never be possible.

## Resolution

The owner resolved this contract on 2026-10-07 by choosing delta-v accounting, player-selectable flight priorities and the investigated forecast model. The following records the accepted behavior and ownership boundaries. Sampling accuracy, work quotas and numerical details remain implementation-time validation work.

### Planning Progress

- [x] Capture route-tile, fuel-limit and availability requirements.
- [x] Inspect current orbital motion, generated asteroid fields and Rocket capability assumptions.
- [x] Compare build-time catalogs with planner-owned on-demand forecasts.
- [x] Classify constant, periodic and multi-phase connections.
- [x] Evaluate the owner's representative belt-radius approximation.
- [x] Define safety invariants and numerical validation scenarios.
- [x] Resolve delta-v accounting, flight-priority choice and forecast scope with the owner.
- [x] Finalize runtime versus prebaked delivery in favor of fully prebaked forecast generation.
- [x] Record the owner's selection of fully prebaked forecasts and change-triggered regeneration.
- [x] Review delegated findings and record their implications below.
- [x] Resolve developer decline, noninteractive builds and compulsory fresh GitHub-release data.

### Budget Safety And Route Selection

A cap is an upper propulsive delta-v allowance, not fuel burned in advance or a separate tank. Unused fuel remains aboard and retains its usable delta-v. Later caps do not automatically increase.

For unchanged propulsion and structural mass without replenishment, usable delta-v is effective exhaust velocity multiplied by log(current mass / terminal mass after usable propellant is exhausted). Successive propulsive burns subtract their actual delta-v from that capability. If available delta-v covers summed route allowances and each leg stays within its allowance, remaining capability covers remaining allowances. The propulsion model must account consistently for the actual consumable mixture. This does not prove a usable departure window, adequate thrust, acceptable burn or transfer duration, companion supplies or receiving compatibility.

Check the whole remaining delta-v interval before departure, up to the next replenishment or mission end. Tank capacity alone is not enough. Actual servicing must provide the planned resources. Refueling, engine or propellant changes, structural changes or capability loss require a fresh usable-delta-v calculation and budget assessment. Previous coverage cannot be carried across a changed propulsion state. For Loop schedules, include the closing leg and evaluate across the last-to-first boundary. A loop without replenishment can execute only finite covered laps and must not be described as indefinitely sustainable.

Ascent, transfer departure, capture and landing participate whenever the selected leg includes them. There is no unbudgeted extra landing charge. Companion oxidizer and provisional coolant are checked independently under their eventual propulsion rules. Freight fluids do not count as propulsion supplies.

Each Travel Block has the player's flight-priority choice. Fuel-efficiency priority minimizes required delta-v among currently eligible candidates. Speed priority minimizes transfer time among those candidates. Both obey the delta-v cap, actual vehicle feasibility and existing vehicle-class duration policy. Apply eligibility before choosing the candidate. The priority ranks routes for the current departure opportunity, while the cap controls whether to wait for another window. This does not add a player-configured duration limit.

An earlier leg using less delta-v retains extra capability. Under unchanged propulsion, it does not invalidate a later universal orbital delta-v threshold. The extra propellant mass can still lengthen finite burns or affect thrust-to-weight feasibility. Guidance states its assumed vehicle condition and refreshes when that condition changes. Actual departure uses actual state and converts the accepted burns into real resource consumption. There is no fixed liters-per-delta-v coefficient.

### Motion Classification

Use the actual motion relative to the transfer attractor, not just the object's type label. The current mechanics calculate a planar x/y state and do not apply inclination. The single-relative-phase rules below rely on that rotation-invariant planar model. Future inclination support requires reclassification, not automatic reuse of the same proof.

| Connection | Forecast treatment |
| --- | --- |
| Local transitions on one celestial body | Assess applicable ascent, landing and docking maneuvers. A same-body interplanetary-planner rejection must not become a blanket ban on local movement. |
| Planar circular planets around one star | One complete relative-phase cycle for each directed geometry under the current rotation-invariant model. |
| Planar circular sibling moons around one planet | One relative-phase cycle after accounting for their common parent under that same model. |
| Equal signed angular speeds | Constant relative geometry. Assess the actual fixed phase, not hypothetical windows across other phases. |
| Opposite directions | Use signed relative angular speeds. |
| Two selected asteroids in the current rigid SOL belt | Query a shared baked source-radius, target-radius and separation table. Relative geometry is constant, so no evolving time axis is needed. |
| Circular planet and supported asteroid belt | A shared representative-radius family, described below. |
| Two supported circular belts | If needed, a small family covering both source and destination radii, including mixed inner/outer combinations. Do not generate all asteroid pairs. |
| Planet to another planet's moon, such as Overworld to Callisto | Multiple phases. Keep direct travel and forecast the actual route over a bounded period. |
| Hierarchical moon to a specific asteroid | A bounded requested-target forecast. A planet-belt phase shift does not preserve the independent moon phase. |
| Eccentric, nested or unsupported motion | A bounded actual-model forecast or explicit unavailable forecast data. Do not claim a one-phase cycle. |
| Different star systems | First require a supported route/attractor model. Do not apply the planet-pair cycle formula automatically. |

For circular motions, signed angular speeds omega_A and omega_B give relative phase phi(t) = phi_0 + (omega_B - omega_A) * t. Unequal speeds repeat after 2*pi / abs(omega_B - omega_A). Equal speeds have constant relative phase. Obtain effective speeds from OrbitalMechanics. With positive attractor gravity, authored orbitSpeed magnitude is not an independent orbital speed.

A full hierarchical route repeats only if every relevant phase repeats in the same frame. Do not search for a floating-point least common multiple or call a near alignment an exact cycle. Do not substitute Jupiter for Callisto or require an extra parent-orbit stop merely to simplify forecasting.

### Shared Belt Approximation

The owner suggested inner- and outer-edge virtual asteroid samples and accepted the expanded forecast model including midpoint coverage. These are numerical target geometries, not registered phantom asteroids or new celestial identities.

For a direct circular planet-to-belt connection, generate shared phase profiles for representative inner, middle and outer radii. Every representative uses the actual belt's shared angular speed. Ordinary Keplerian speeds recalculated at each representative radius would model a different system.

A selected asteroid supplies its real radius and angular offset. Query or interpolate the shared family at that radius, before classifying affordability. For a complete single-phase cycle, the initial angle shifts the next-window time but does not change the full-cycle availability percentage or longest gap. At equal angular speeds, only the actual fixed phase matters.

Do not interpolate final percentages or maximum waits between representative radii. Those summaries lose the arrangement of windows. Approximate phase costs or eligible candidate data first, then derive the statistics.

Inner and outer costs do not mathematically bound all interior costs. Solver branches, invalid trajectories and candidate changes can create interior extrema. The midpoint is useful additional coverage, not a proof. A maximum over representatives is pessimistic only for those representatives. Label family results as estimates. An empirically cautious margin can be selected after comparison with denser reference calculations, without advertising guaranteed conservative bounds.

Same-belt selected pairs use the baked radius-pair and fixed-separation family. A second used generated belt would justify a source-radius and target-radius family with relative phase. There is only one current generated field, so do not add unused cross-belt datasets before they are needed.

Hierarchy can defeat family phase shifting. For moon-to-asteroid routes, follow the selected target's actual phases through the corresponding baked family to derive bounded guidance. No gameplay solver generates a profile for that target. No bulk calculations are triggered by discovery or map visibility.

### Statistics And Coverage

For a proven periodic profile, time availability is the fraction of the full cycle with an eligible route. Longest waiting is the largest nonqualifying interval, including a gap crossing the cycle boundary. Time to the next window from now is a separate value.

For bounded forecasts, show the covered period and the longest observed gap there. Do not join the first and last samples. A trailing unavailable interval may continue beyond coverage, so it does not establish a finite maximum. No qualifying samples means no window found in the sampled coverage, not permanent impossibility.

Orbital availability excludes loading, replenishment, maintenance and docking occupancy. A busy pad does not suppress departure. The vehicle arrives and waits there under the existing no-consumption rule.

Show unavailable estimates when baked data are missing, stale or incompatible rather than inventing a zero-percent result. Invalid numerical samples are unavailable or uncertain data, never zero-cost flights. Forecast accuracy must be checked around narrow windows and invalid/branch-changing regions.

### Ownership And Prebaked Data

Keep motion with OrbitalMechanics, trajectory candidates and forecasts with the shared orbital planner, and actual resources, propulsion, allowances and schedule execution with the vehicle. The Star Map reads authoritative results and must not implement a second evaluator.

| Generation option | Assessment |
| --- | --- |
| Build-time catalog | Useful for a finite fixed set of geometries, but must match runtime physics. A min/max-only catalog cannot answer window distribution or varied vehicle constraints. |
| All-pairs startup generation | Rejected. It delays startup and scales badly with generated bodies. |
| Player-requested background simulation | Superseded by the owner's fully prebaked selection. |

Ship generated forecast data with the mod and use inexpensive runtime table queries. No gameplay job generates or repairs geometric profiles. Generator work and packaged data size remain bounded and measured. The fully prebaked dataset needs no legacy reader or runtime-generation fallback.

Changing a cap queries existing data. Changing actual Rocket state refreshes its affordability projection. Geometry, attractor gravity, clearance or solver-rule changes require a matching new bake. They do not trigger runtime regeneration. Pad occupancy and servicing state do not belong in the baked data. Cached geometry does not prove a target still exists.

Keep A-to-B and B-to-A directional. Station endpoints tied to equivalent body geometry can share the orbital component while local maneuvers and endpoint compatibility remain distinct. Asteroid references remain CelestialObjectKey references, with minor-body details resolved inside their owner.

A build-generated dataset is the selected source of forecast information. Actual flight feasibility remains a separate authoritative check. Exact stored layout and sample counts are execution choices to settle with numerical and size measurements.

### Accepted Prebaked Build Direction

The owner selected 100-percent prebaked forecast data. Ordinary compilation performs a cheap comparison of canonical calculation inputs against the inputs recorded for the existing bake. Include the celestial catalog and every property that affects routes. Physics, unit and sampling rules must also participate in validity, rather than accepting an unchanged planet hash after the solver changes.

When data are unchanged, reuse the existing bake without sampling. When they change, show a build-console warning and request a yes/no regeneration decision. The owner requested a build argument that automatically declines regeneration without prompting. The exact argument and behavior in terminal, IDE and CI remain part of the delegated build-contract investigation.

The owner accepted continuing a development build after declining regeneration, with missing or stale estimates unavailable. Exact flight validation remains operational. An explicit decline skips the expensive generator and prompt, not the cheap freshness check. If the existing data are current, they remain usable. Never record a new fingerprint as if old data had been regenerated.

GitHub releases always generate and include a fresh baked dataset. The release workflow is noninteractive and approves generation automatically. A decline argument cannot bypass this requirement. Generation or verification failure prevents publication. Iterative developer compilations retain the cheap check and optional regeneration behavior.

Coverage at arbitrary server epochs uses prebaked motion-phase data and inexpensive runtime queries, not a file valid only for one bake-time epoch. No stale or missing dataset causes generation in gameplay.

### Fully Prebaked Coverage Requirements

The generator produces reusable phase-dependent orbital candidate data. Runtime derives current phase coordinates and follows their actual future evolution through table lookups. These queries and the actual departure check remain allowed. Runtime does not solve trajectories to generate, extend or repair forecast tables.

Direct circular planet pairs and sibling moons need one relative phase. Overworld-to-Callisto needs two phases, and moons belonging to different planets generally need three. A uniform percentage over multidimensional cells is not necessarily time availability for the actual route. Follow its real phase path over a stated finite future interval to estimate availability and waiting. A trailing gap cannot establish a finite global maximum.

Asteroid families remain shared. Planet-to-belt data use relative phase and representative radius. Fully prebaked same-belt forecasts use representative source radius, target radius and fixed angular separation, rather than solving a requested pair in gameplay. Hierarchical asteroid forecasts add the relevant phase axes. No catalog enumerates every generated asteroid pair.

Retain or approximate candidate alternatives consistently with the accepted dV cap and both priorities. Interpolation must not turn invalid samples into zero-cost flights or combine unrelated solver branches into a fictitious candidate. Numerical accuracy and candidate retention need comparison with denser references.

Rich data are not automatically small. At 32 samples per phase axis, 64 durations, two branches and three float values per candidate, raw two-phase values are about 1.5 MiB per directed route and three-phase values about 48 MiB, before metadata. These are illustrative counts, not selected resolutions or measured sizes. Choose data density and compression from actual error and memory measurements rather than applying one dense grid everywhere.

The ordinary hash check belongs in a tracked build task, not only the configuration phase, because this project enables Gradle configuration cache. Canonical inputs need deterministic ordering and encoding. Their fingerprint is compared with the one stored for the actual baked output, not with the last ordinary build. Include relevant solver/generator identity rather than hashing the entire repository or only planetary values.

The current registry is coupled to Minecraft, Forge and GT initialization. A cheap checker needs one shared headless numerical definition source or an incremental numerical export. Do not launch full game initialization on every build, parse arbitrary Java expressions with regex, or maintain a second manually copied planet list.

Explicit build answers take priority over prompting. Interactive input cannot be assumed in IDE or CI. Missing input must not hang the build or count as regeneration approval. The exact argument spelling is still a proposal, not an implemented option.

### Accepted Noninteractive Build Behavior

For a noninteractive development build with stale or missing data and no explicit answer, fail with an actionable message requesting a yes/no argument. Never wait for unavailable input or silently approve expensive regeneration. The caller can explicitly pre-decline. GitHub releases instead automatically generate and verify the dataset under their separate accepted rule.

Development decline, noninteractive behavior and compulsory fresh GitHub-release data are resolved. Exact argument spelling and frontend wiring are implementation details. No new public-save compatibility or runtime-generation path is implied.

### Candidate Correctness

A single minimum-total-delta-v sample can lose a candidate whose separate burns or time of flight fit a particular vehicle. Forecasting and dispatch must use consistent eligibility and selection policy. Preserve or recompute relevant alternatives, including departure and capture costs.

The existing planner currently selects one duration and one Lambert branch before vehicle evaluation. Rejecting that result afterward is insufficient for cap-aware planning. Do not assume that Pareto compression on total delta-v and duration is safe. Every applicable cost and feasibility condition must be monotonic in the compared dimensions before dominated candidates can be discarded without loss.

The belt approximation may be numerically imperfect, but exact dispatch must evaluate the actual selected target and actual Rocket. If the real candidate exceeds its cap, keep waiting. Never spend beyond the allowance because a shared family estimated a cheaper route.

After departure, the selected trajectory and maneuver obligations remain attached to that active flight. An occupied receiving pad does not rerun the interplanetary transfer. Reloading must not reroll the trip or charge fuel twice. Temporary waiting must not trigger the intentional-loss contract.

### Scale And Verification

Current code checks 64 transfer durations and two Lambert branches. At 64 departure samples, one profile means 4096 duration candidates and up to 8192 branch evaluations. Three radial curves mean up to 24576 branch evaluations for one planet-belt family, rather than about 2.62 million for separate profiles of all 320 generated asteroids.

Those 320 bodies have 102080 directed same-field pairs. Naive full-cycle sampling for all pairs would involve about 836 million branch evaluations. That is a rejected workload. Current same-belt geometry additionally eliminates the time dimension for requested pairs.

These are operation counts, not measured runtime. Candidate-rich profiles use more memory than a min/max table. Work quotas and retained-memory limits must be chosen from measurements.

Required acceptance and numerical comparison cases:

- Circular rotation invariance, full relative-cycle repetition, equal speeds and opposite directions.
- A periodic unavailable interval crossing the sample boundary and a censored bounded interval.
- Belt approximation compared with exact interior radii, both directions and multiple phase resolutions. Measure delta-v error, optimistic affordability mistakes, availability percentage-point error and longest-wait error. Treat radial and temporal error separately.
- Source geometry close to or inside a belt's radial range, branch transitions, invalid candidates and narrow windows.
- No gameplay generation for visible or newly discovered asteroids. Shared baked family queries and bounded runtime lookup cost.
- Unchanged-input builds skip generation. Explicit developer decline disables only missing or stale estimates, and noninteractive stale builds without an answer fail clearly. Every GitHub release generates, verifies and packages fresh data.
- A slower feasible candidate when the fastest is over budget, and a candidate needed because individual burn limits differ.
- Usable delta-v below remaining delta-v caps despite enough tank capacity. Retained capability after a cheaper leg. Missing companion fluids and partial replenishment.
- Loop closing-leg coverage, full local maneuvers, arrival-side docking waits, changed vehicle state, target loss and active-flight reload.
- Planned payload deployment followed by intentional loss, without confusing a waiting vehicle with that terminal state.

Compare representative families with a denser reference grid during numerical verification, not at every server startup. Refine only the families whose measured errors warrant more radial or phase samples. Extra samples remain shared family data.

## Resolved Owner Choices

1. Delta-v is the universal planning unit. Store orbital demands as delta-v and convert the Rocket's actual fuel into usable delta-v. Physical fuel storage and consumption remain real resources.
2. The player selects fuel-efficiency or speed priority. Both choose only eligible candidates within the allowance. The earlier fastest-only recommendation is superseded.
3. The forecast model is accepted: complete cycles where valid, shared representative belt-radius approximations and bounded actual-target forecasts for multi-phase cases. Estimates never bypass the actual departure check.
4. Forecast generation is fully prebaked. Ordinary developer builds check calculation-input freshness and request regeneration only when needed. A pre-decline argument skips regeneration and leaves stale estimates unavailable. Exact mission validation continues.
5. GitHub releases automatically generate and package current forecast data. Failed generation or invalid data block publication.
6. A noninteractive development build with stale or missing data and no explicit answer fails with instructions to pass a yes/no argument.

The design contract is resolved. Numerical accuracy, propulsion formulas, generator cost and data size require implementation-time measurement. Accepted planning does not certify an implemented or benchmarked feature.

## Existing Code Boundary

Read-only inspection at Galaxia commit `a9128e9e` on 2026-10-07 found that `OrbitalTransferPlanner.computeRoute` accepts a departure time, evaluates 64 transfer-duration candidates and returns route delta-v and duration. It does not accept vehicle propulsion or a fuel-volume cap. This supplies a starting calculation, not an implemented budget or departure-window guarantee.

The current generated field is attached to SOL at the world origin. AsteroidFieldOrbitResolver uses world-origin phase and velocity. The rigid circular simplifications are supported for this current field, not automatically for a field around an offset star. Its coordinate-frame assumption requires validation before expanding that support.

The Rocket prototype derives fuel from nominal capacity, uses hardcoded Isp, and lacks the complete actual-resource/propulsion model. Reliable usable-delta-v conversion requires that capability on the existing vehicle owner. The planning analysis does not establish implemented vehicle-aware route feasibility.

## Provenance

Direct owner discussion of changing outbound and return costs on 2026-10-07, followed by explicit resolution of delta-v accounting, selectable priorities and the forecast model.

The owner's later clarification on the same date selects route availability as a percentage of time and approximate maximum waiting in seconds as the intended guidance for a selected fuel allowance.

The owner subsequently requested a complete investigation with subagents and proposed representative inner/outer belt targets as an acceptable approximation candidate. The consolidated proposal adds midpoint coverage and separates approximate forecasting from exact cap enforcement.

The final owner answer supersedes the proposed primary-fuel-liter control and mandatory speed priority. The owner retained real fuel in the Rocket while choosing delta-v for mission accounting.

The owner's generation follow-up selected two explicit simulation actions and a background worker that returns results to the server. This supersedes automatic forecast generation merely upon route selection.

The owner then rejected progressive profile publication in favor of a single complete transfer and requested an estimated connection count plus completed-work chat updates. This supersedes the proposed priority queue and partial-result streaming.

The later fully prebaked selection supersedes the runtime-generation candidate. The owner accepted runnable development builds with stale estimates disabled after decline and required generated data in every GitHub release.

The owner then accepted failing noninteractive stale development builds that provide no explicit answer. Superseded runtime-generation details were removed from the active contract.
