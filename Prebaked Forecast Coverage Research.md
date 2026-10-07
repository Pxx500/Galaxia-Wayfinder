---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Prebaked Forecast Coverage Research

Source: Owner discussion and read-only Galaxia source inspection at commit `a9128e9e` by the prebaked coverage investigation subagent

Imported: 2026-10-07

## Source Snapshot

The owner selected fully prebaked orbital forecasts, generated explicitly rather than during every compilation. A cheap build check should detect changed calculation inputs or model rules and offer regeneration, with an argument that declines automatically. This investigation describes the coverage implications. It does not approve additional gameplay changes or prescribe an implementation plan.

### Main Finding

A baked time series for one arbitrary epoch cannot serve every future epoch of a route with several independent orbital phases. Reusable phase tables can. Runtime evaluates the current phase coordinates, reads the table and derives allowance-dependent statistics. It does not solve transfer trajectories or generate new geometric profiles.

The exact departure calculation remains authoritative under the accepted contract. Running that calculation when actually dispatching is compatible with fully prebaked forecasts. Running it repeatedly to repair, extend or create forecast data in gameplay would be runtime forecast generation.

### Code Evidence

Paths are relative to the Galaxia checkout at the inspected commit. The knowledge graph found the owners, but full reindexing failed twice with `aborted_previous_preserved`. Current source was read directly to verify the findings and line numbers.

| Owner | Observed behavior |
| --- | --- |
| `registry/orbital/OrbitalMechanics.java:56` | Ordinary child world state adds its local orbital position and velocity to its parent's state. Nested moons therefore introduce additional motions. |
| `registry/orbital/OrbitalMechanics.java:109` | State is planar. Eccentricity is supported, but inclination is not applied. Circular motion is the current authored baseline. |
| `registry/orbital/OrbitalMechanics.java:155` and `:226` | Positive parent gravitational parameter determines mean motion through `sqrt(mu / a^3)`. Authored orbit-speed magnitude is not independently authoritative in that case. Its sign still determines direction. |
| `registry/orbital/OrbitalTransferPlanner.java:124` | One departure call evaluates 64 durations, from 0.1 to 3.0 times the phase-dependent Hohmann estimate, then returns one priority-selected candidate. |
| `registry/orbital/OrbitalTransferPlanner.java:134` | Attractor sprite size currently affects minimum transfer periapsis. A field that appears visual can therefore be a mathematical input. |
| `registry/orbital/OrbitalTransferPlanner.java:226` | Each duration evaluates both Lambert directions, but currently retains only the lower-total-dV branch. |
| `registry/celestial/CelestialObject.java:62` | Hohmann duration uses actual source and target distances from the attractor at the supplied epoch. Nested route duration ranges can vary with phase. |
| `registry/celestial/asteroid/AsteroidFieldOrbitResolver.java:35` | Asteroids share the belt's angular speed and receive individual radius and angular offsets. Their states are currently built around the world origin. |
| `registry/celestial/asteroid/content/GeneratedAsteroids.java:22` | Current generated field has 320 nodes and spans 2.15 to 2.45 Earth-relative AU units. |
| `registry/celestial/CelestialRegistry.java:511`, `:666`, `:788` | Overworld orbits Sol, Jupiter orbits Sol, and Callisto orbits Jupiter. A direct Overworld-to-Callisto route has three circular components. |
| `registry/celestial/CelestialRegistry.java:98` | Default registration also initializes GT materials, dimension and block content. Offline numeric input acquisition is additional work and must not introduce a separately maintained duplicate planet list. |

### Reusable Geometry Coverage

For planar circular motion, globally rotating the entire geometry leaves scalar transfer costs unchanged. With `m` distinct relevant circular components, at most `m - 1` independent relative angles remain. Shared components can cancel when source and target share a moving parent. The number of distinct components, not the celestial class label, determines the table shape.

| Route | Baked coordinates |
| --- | --- |
| Two planets around one star | One relative phase |
| Sibling moons around one planet | One relative phase after shared-parent motion cancels |
| Overworld to Callisto | Jupiter phase relative to Overworld and Callisto's local phase relative to Overworld |
| Moons around two different planets | Typically three relative phases |
| Planet to selected belt asteroid | Relative phase plus representative target radius |
| Moon to selected belt asteroid | Typically two relative phases plus representative target radius |
| Two asteroids in one rigid belt | Source radius, target radius and angular separation. No evolving time axis |
| Different rigid belts | Source radius, target radius and relative belt phase |

The current three representative radii can be shared across all nodes in a belt. A chosen node supplies its actual radius and phase offset for lookup. No per-node all-pairs dataset is needed. A rigid-belt pair still needs the shared radius-pair/separation family. Computing a fresh pair profile on demand would contradict fully prebaked forecasts, even though that earlier runtime candidate required only one nonperiodic evaluation.

A parent-body endpoint also needs care. If the transfer attractor and source are the same body, the current body-center source radius is zero and the Lambert planner rejects the geometry. Local ascent or parking-orbit state must provide the actual nonzero orbital endpoint where that transfer model needs one. Baking a body-center failure as permanent impossibility would be incorrect. This is an existing endpoint-model limitation, not a reason to invent an extra required gameplay stop.

The world-origin asteroid resolver must not be assumed valid for a field around an offset star. Expanding that support needs a correct common-frame motion model before its forecasts can be baked.

### Statistics At Arbitrary Epochs

For a direct pair, relative angular speed gives a full synodic cycle. The baked phase curve supports estimated percentage availability and the longest unavailable gap, including wraparound. Equal angular speeds use the actual fixed relative phase. Sampling all hypothetical phases would invent windows the real pair never reaches.

For several phases, runtime follows the real phase trajectory through the baked table. Given current epoch `t`, each coordinate advances as `phi_i(t + dt) = phi_i(t) + relativeOmega_i * dt`, modulo one turn. Table reads at future times support a bounded forecast with a stated coverage period. This is cheap projection of stored data, not Lambert sampling.

A uniform count over every multidimensional phase cell is not generally the percentage of time for the actual route. Rationally dependent frequencies may follow only a subset of those cells. It also cannot establish the longest waiting interval. Do not claim an exact common period by taking a floating-point least common multiple of periods.

For such bounded projections, report availability during the covered interval and the longest observed gap. If an unavailable gap continues beyond the forecast horizon, its finite maximum is unknown. No sampled qualifying lookup means no window found within coverage, not permanently impossible travel.

### What Each Sample Must Preserve

A min/max-only dataset cannot support variable dV allowances, both flight priorities and vehicle feasibility. Retain eligible alternatives with duration, departure dV, capture dV and numerical validity. Transfer branch identity is needed if directional burn or trajectory constraints participate in eligibility. Do not treat an invalid solver result as zero dV.

The 64 duration choices are candidate alternatives within each phase cell, not 64 independently usable flight windows. Candidate selection happens after the chosen allowance and applicable vehicle constraints have filtered alternatives. Speed priority chooses the shortest eligible flight, while efficiency priority chooses the least eligible dV.

Two separate burns can have different feasibility even when total dV is identical. Keeping only the fastest or cheapest current result can remove the only feasible candidate for a particular engine. Total-dV/time dominance is insufficient until every eligibility constraint is known to be monotonic in those dimensions.

Universal tables store orbital requirements. Runtime resource-to-dV conversion, local ascent and landing costs, finite-burn checks and actual servicing remain vehicle computations. Forecast percentages must state their vehicle assumptions if they include those constraints. Geometry alone cannot promise that a weak engine can execute a short flight.

### Approximation And Cost

Inner, midpoint and outer radii are numerical representatives. Neither extrema over the two edges nor extrema over all three prove bounds on every interior radius. Solver branches and validity regions can change inside the band. Interpolating across a valid/invalid or branch boundary can fabricate a cheap candidate. Keep candidates associated consistently or use nearby-cell estimates with explicit uncertainty until numerical validation supports stronger interpolation.

First approximate phase-dependent candidate data, then apply the allowance and derive statistics. Interpolating final percentages or maximum waiting values loses the arrangement of windows.

For `P` samples on each independent phase axis and `K` retained duration candidates, generation scale is approximately `P^d * K * 2` Lambert branch evaluations per directed route family, where `d` is the phase dimension. With `P = 32` and `K = 64`, this is 4,096 evaluations for one phase, 131,072 for two and 4,194,304 for three. These are counts, not measured durations. Increasing every axis to 64 multiplies three-axis work by eight.

Candidate storage also grows. At 32 samples per axis, 64 durations, two branches and three 32-bit scalar values per branch, raw two-phase candidate values occupy approximately 1.5 MiB per directed route. Three-phase values occupy approximately 48 MiB. Validity and metadata are extra. Compression or candidate reduction may help, but the claim that all forecast data is automatically tiny applies only to min/max summaries.

A same-belt family with three source radii, three target radii and 64 angular-separation samples has 576 geometric cells. It scales with the family's sample resolution rather than the 102,080 directed pairs of 320 actual nodes.

### Comparison Of Coverage Directions

**Phase tables** preserve actual nested motion and support arbitrary epochs. They keep runtime geometric solving out of forecasts. Their offline work and storage grow with the number of phases, so direct pair curves and multidimensional moon routes should not blindly use the same resolution. Accuracy must be measured against denser exact reference calculations, especially narrow windows and branch changes.

**A narrower family approximation** could model a planet-centered transfer plus a separately estimated local moon correction. This uses smaller data. It does not preserve the existing direct moon route or prove its dV/time tradeoff. A worst-case correction may erase useful windows, while an optimistic correction can misstate availability. Using it is a gameplay approximation requiring owner approval, not merely an implementation optimization. Adding mandatory parent stops to make the decomposition exact would change the accepted route model.

The simplest coherent recommendation is shared phase tables for the supported current planar circular hierarchy, with belt-radius families. Use full cycles only where proven. For several phases derive a bounded future forecast through table lookups. Measure resolutions and retained alternatives in the offline generator. Explicitly mark motion families not covered by the shipped data. Do not silently create runtime profiles to fill holes.

### Fingerprint And Dataset Validity

Fingerprint a canonical numeric input catalog with stable celestial keys and parent relationships, orbital elements or effective rates, gravitational parameters, attractor clearance, field radial ranges and motion-family rules. Include hierarchy transforms and every value that affects the candidate duration range. Retain a model fingerprint covering the numerical solver, motion resolution, candidate policy, validity tolerances, units and dataset schema. Hashing only planet values would miss solver changes.

Sort records by stable keys, use a fixed encoding and exact finite numeric representation, and exclude timestamps or registration iteration order. A whole repository commit hash is too broad because unrelated UI and recipe work would mark forecasts stale. A conservative source-content fingerprint over the mathematical/input-owning sources can detect changes before a pure numeric extraction seam exists, but may produce extra regeneration warnings for unrelated edits in those files. A manually incremented version alone does not establish that every relevant code change was captured.

Family datasets need not fingerprint generated individual positions or world seeds when they cover the whole supported radius/phase domain. Runtime selected targets still must satisfy those domain limits. An exception with different motion, radius or an unbaked field needs explicit unavailable guidance. Discovery state, texture pixels, ore profiles, team knowledge and pad occupancy are not mathematical forecast inputs.

Stored metadata should identify input and model fingerprints, units, coordinate axes and bounds, candidate coverage, periodicity proof or bounded-statistic rule, resolution and measured approximation limits. A dataset checksum can detect corruption independently of freshness.

Missing, incompatible or stale data must be visible as unavailable estimates unless the owner explicitly approves using stale estimates. A declined regeneration can permit iterative compilation under the requested policy, but it must not turn old data into certified current forecasts. Authoritative current departure checks can still function. There is no gameplay regeneration fallback.

### Material Choices Still Needed

1. Confirm that fully prebaked means geometric candidates are baked while runtime derives future availability by table lookup, including bounded projections for multi-phase routes. Otherwise epoch-independent maximum-wait guidance cannot be provided cheaply for the full hierarchy.
2. Decide what declining regeneration means for runtime guidance. The safe recommendation is that mismatched data has unavailable estimates while exact departure remains usable. Using marked stale estimates is a different explicit choice.
3. Decide whether a missing initial dataset can be bypassed for developer builds under the same unavailable-guidance rule. Generation must never claim a successful ready dataset before one exists.

The recommended phase-table direction does not require reopening the accepted dV unit, priority choice or asteroid approximation contract. Numerical density, candidate compression and work limits should be chosen from measurements rather than additional gameplay questions.

[[Sources]]
