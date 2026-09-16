---
type: source
status: deferred
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Agent Source - Patched Conics Transfer Rework

## Purpose

This node preserves the complete Patched Conics investigation, implementation experiment, planning decisions, and review outcome as a deferred Wayfinder source. It is linked from [[Deferred]] and is not part of the active Galaxia Alpha planning frontier.

The work attempted to replace the old Lambert-only interplanetary transfer model and synthetic local-loop visualization with one authoritative three-phase mission:

1. departure from the source gravity well;
2. Lambert cruise between moving bodies;
3. arrival into the destination gravity well.

## Deferred Status

The owner deferred this work because it became a substantially larger cross-system rework than expected and its gameplay value is uncertain.

The implementation cost was not limited to adding gravity-well terms to delta-v. A physically coherent result required coordinated changes to numerical solving, astronomical data, time-of-flight search, vehicle cost models, server dispatch authority, networking, persistence, planner state, and rendering.

Local departure and arrival "spirals" were a particular source of implementation difficulty. Their direction, shape, timing, moving-planet frame, and position/velocity continuity at the cruise patch boundaries repeatedly exposed edge cases. The current rebuild replaces synthetic spirals with finite local two-body conic arcs, while true low-thrust spirals remain future work.

The visible payoff is doubtful. At Star Map scale the local gravity-well phases are small compared with the interplanetary cruise, and the player will probably not notice their detailed geometry during normal play. Their main observable effects are higher delta-v, a slightly different total time of flight, and a short line segment near each body. A simpler gameplay cost model may deliver almost the same player-facing decisions at far lower implementation and maintenance cost.

This is therefore preserved as a reviewed experiment and design source, not accepted integration work. Do not resume or merge it merely because the implementation exists.

## Current Implementation State

- Branch/worktree: `PatchedConics-rebuild` at `C:/Users/Pxx500/Documents/GitHub/Galaxia/.worktrees/PatchedConics-rebuild`.
- State: implemented and verified in an isolated worktree, but uncommitted, unpushed, and not integrated with `master`.
- Tracked delta at the last audit: 19 files, approximately 1,152 insertions and 1,592 deletions, plus new untracked transfer-domain and test packages.
- The implementation is a clean forward cut. It intentionally contains no format versioning, migration path, compatibility shim, or legacy transfer fallback.
- `TransferScanner` and the old raw `TransferRoute` model are removed from the rebuilt flow.

### Implemented Physics And Search

- Explicit SI conversion through `OrbitalUnitScale`, with a stylized simulation scale rather than literal real-world travel times.
- Complete transfer physics data only for Vael, Mars, and Overworld; fictional or incomplete bodies fail with typed incomplete-data results rather than guessed placeholders.
- A composed `PatchedConicMission` containing departure local arc, Lambert cruise, arrival local arc, and total TOF.
- Finite hyperbolic/parabolic local conics around moving source and destination bodies.
- Position and velocity continuity checks at both patch boundaries.
- Universal-variable cruise propagation and analytical phase sampling.
- Explicit Lambert branch identity and regression coverage around 180 degrees.
- Adaptive TOF search across both Lambert branches, with departure fixed to now rather than waiting for launch windows.
- `maximumTotalDv` filtering against the selected evaluation's total delta-v.

### Implemented Transfer Modes

- Railgun and spaceship are separate immutable evaluations and separate missions.
- Railgun is modeled surface-to-surface. Its paid total delta-v is launch speed derived from specific orbital energy, so it pays the departure gravity well. Arrival impact speed is reported but is not a paid braking cost because no catcher is required.
- Spaceship pays surface access where applicable plus impulsive parking-orbit escape and capture costs.
- True continuous low-thrust spiral dynamics are not implemented and remain a future possibility.
- The planner can simulate Railgun, Spaceship, or Compare. Compare retains both independent missions rather than combining mode fields into one route.

### Implemented Gameplay Integration

- HAMMER route feasibility, launch capability, energy, ticks, delivery state, packet payload, persistence, and client rendering consume the same railgun mission.
- `WHEN_DV_UNDER` compares total delta-v.
- Dispatch performs a fresh solve at the current epoch; preview recalculation is throttled and invalidated by input changes.
- Destination storage capacity, queues, and docking throughput remain outside trajectory planning.
- Runtime celestial references use `CelestialObjectKey`.
- The planner renderer samples departure, cruise, and arrival separately around body positions at each sample epoch.

## Accepted Decisions Preserved By The Experiment

- Keep an explicit abstraction layer even when astronomical calculations use SI units; literal real-world distances and times are not a gameplay requirement.
- A body's sprite size is presentation-only and must never influence trajectory physics.
- Depart immediately. Do not add launch-window waiting as part of this system.
- Railgun and spaceship are distinct transfer products with distinct cost semantics.
- Total delta-v is the authoritative value for limits, HAMMER energy, and `WHEN_DV_UNDER`.
- Railgun pays to leave the source gravity well but does not pay to stop at the destination without a catcher requirement.
- Spaceship uses surface access plus impulsive escape/capture. A dock may queue ships, but destination throughput is irrelevant to trajectory planning.
- Missing astronomical data must produce an explicit unavailable result, not guessed physics.
- No migration, versioning, dual codec, or legacy compatibility path is wanted for this pre-release feature.

## Why The Rework Expanded

The original problem looked like a transfer-price correction. In practice, adding gravity wells changed the ownership and shape of the entire route result:

- Lambert alone only supplies the heliocentric cruise boundary velocities.
- Gravity-well entry and exit require body radius, gravitational parameter, sphere of influence, endpoint altitude, and relative boundary states.
- Local phase duration changes the Lambert departure and arrival epochs, so local arcs and cruise cannot be solved as unrelated visual decorations.
- Railgun surface launch and spaceship parking-orbit maneuvers do not share one total-delta-v formula or necessarily one geometry.
- A mission used for billing must also be the mission used for server timing, persistence, synchronization, preview, and active-flight rendering.
- Near-180-degree Lambert geometry, branch selection, TOF minima, and phase sampling each introduced separate numerical edge cases.
- The historical branch could not be transplanted safely because current celestial identity, GUI, registry, logistics, and planner APIs had diverged.

The result is closer to a replacement of the transfer domain than a localized cost fix.

## Review And Verification State

The rebuilt working tree completed focused transfer, planner, simulator, HAMMER, networking, persistence, and celestial-data tests. A full `agentVerify` run passed Spotless, tests, and build. Two independent final reviews found no reachable defect in the reviewed physics or end-to-end authority flow.

Remaining uncertainty:

- no manual in-game visual verification was completed;
- active-flight rendering uses a sampled polyline and may undersample very short local phases;
- package motion interpolates between precomputed points rather than analytically evaluating the mission every frame;
- there is no dedicated persistence test that round-trips an active `LogisticsDelivery` containing a full `RailgunTransferEvaluation`;
- the larger product question remains unanswered: whether this realism creates useful choices that justify its complexity.

The pre-rebuild review findings preserved below explain why the rebuild was necessary; they must not be read as confirmed defects in the final isolated rebuild.

## Reactivation Gates

Before this source becomes active work again, decide:

1. What player-facing decision or progression constraint requires full three-phase patched conics rather than a simpler gravity-well cost policy?
2. Are the local arcs expected to be visible and legible gameplay, or only internal cost/TOF accounting?
3. Is comparison between railgun and spaceship intended to drive player choices, or are the modes already separated by progression and infrastructure?
4. What balance ranges should total delta-v and TOF satisfy under Galaxia's stylized scale?
5. Which celestial bodies need authored transfer physics data for the next playable slice?
6. Is the maintenance cost of coupled local-arc/Lambert solving acceptable for the value exposed in the Star Map?

If these answers favor a simpler model, retain the authoritative mode separation and gravity-well cost semantics without reviving the full local-arc visualization.

## Implementation Surfaces

The deferred working tree touches these principal owners:

- `registry/orbital/transfer/` - mission, local conics, mode evaluations, unit scale, and search policy.
- `registry/orbital/OrbitalTransferPlanner.java` - Lambert geometry and planner entry point.
- `registry/celestial/CelestialRegistry.java` - authored transfer physics data.
- `client/gui/orbitalGUI/InterplanetaryTransferSystem.java` and `OrbitalView.java` - simulation modes, preview, and active-flight rendering.
- `registry/outpost/logistics/HammerDispatchPlanner.java`, `AllowShootingConfig.java`, and `LogisticsDelivery.java` - HAMMER authority and delivery state.
- `registry/outpost/module/types/ModuleHammer.java` - launch capability ownership.
- `core/network/LogisticsSyncPacket.java` - forward-only mission codec.
- `core/persistence/FacilityPersistenceManager.java` - forward-only mission persistence.
- focused tests under `registry/orbital/transfer/`, orbital GUI, celestial data, networking, and outpost logistics.

## Integrated Design Record

This section incorporates the durable information from the temporary repository planning, review, architecture, and AI notes so those files can be removed without breaking this handoff.

### Pre-Rebuild Failure Classes

The reviewed implementation that preceded the isolated rebuild had these material problems:

- cost calculation and preview could describe different trajectories;
- local departure and arrival loops were synthetic animation rather than solved dynamics;
- server TOF covered Lambert cruise but omitted local phases;
- renderer properties, including sprite scale, leaked into physical periapsis choices;
- railgun gravity-well cost could be counted incorrectly and launch constraints were not authoritative;
- spaceship surface ascent/descent was represented as a flat term without a coherent flight contract;
- behavior around a 180-degree Lambert transfer was not protected by an explicit regression contract;
- a fixed TOF grid could skip minima and produce discontinuous route choices;
- the renderer numerically reconstructed conics separately and could drift away from the billed mission;
- silent defaults and placeholder celestial values made incomplete physics appear valid;
- raw Lambert geometry, vehicle evaluation, validity, and active-mode state were mixed into one route object;
- catcher capability was assigned to the destination body rather than endpoint infrastructure or transfer policy;
- tests preserved synthetic visual geometry and volatile balance values instead of domain invariants;
- user-facing simulator text bypassed localization;
- astronomical units and the provenance of the Izzo implementation were not explicit;
- the historical branch had diverged from current celestial identity, GUI, registry, logistics, and planner ownership.

The isolated rebuild was a replacement architecture intended to remove these failure classes rather than patch them individually.

### Rebuild Plan And Execution Order

The accepted rebuild sequence was:

1. Preserve the historical work and isolate a clean rebuild based on current `master`.
2. Audit the old feature delta without transplanting stale APIs or compatibility overloads.
3. Establish dimensional, identity, endpoint, failure, and total-TOF contracts through stable public tests.
4. Separate Lambert geometry from railgun and spaceship evaluation.
5. Solve finite local conics and couple both patch boundaries to moving-body epochs.
6. Correct mode-specific gravity-well costs and HAMMER capability limits.
7. Stabilize Lambert branch selection, near-180-degree behavior, TOF search, and analytical sampling.
8. Integrate one mission through server authority, networking, persistence, simulator modes, comparison, and rendering.
9. Run focused verification, full project verification, one consolidated review, and no more than one fix/re-review cycle.

That sequence reached an implemented and verified state in the isolated worktree. Integration, commits, and PR publication did not happen before the effort was deferred.

### Unit And Time Abstraction

The rebuild uses SI-backed calculations without requiring literal Solar System travel times. The explicit simulation scale is:

```text
L0 = 6,371,000 m
T0 = 1,000 s
V0 = L0 / T0
MU0 = L0^3 / T0^2

r_si = r_game * L0
t_si = t_game * T0
v_si = v_game * V0
mu_si = mu_game * MU0
```

This keeps equations dimensionally consistent while preserving a stylized Galaxia system. Strategic-map screen coordinates, sprite dimensions, and dimension-space blocks are presentation or navigation representations, never literal astronomical distance inputs.

### Core Mission Equations

Total mission time is the sum of independently solved phases:

```text
TOF_total = TOF_departure_local + TOF_Lambert_cruise + TOF_arrival_local
```

At a body-centered radius `r`, the speed on an unbound local conic is derived from hyperbolic excess speed:

```text
v(r) = sqrt(v_infinity^2 + 2 * mu / r)
```

Railgun launch cost from a surface radius `r_surface` is therefore:

```text
delta_v_railgun_total = sqrt(v_infinity_departure^2 + 2 * mu_source / r_surface)
```

Arrival impact speed is reported from the equivalent destination expression but is not added to paid railgun delta-v when no catcher or braking requirement exists.

For an impulsive spaceship departing a circular parking orbit at radius `r_parking`:

```text
delta_v_escape = sqrt(v_infinity_departure^2 + 2 * mu_source / r_parking)
                 - sqrt(mu_source / r_parking)
```

Capture uses the corresponding destination expression, and the spaceship total is:

```text
delta_v_spaceship_total = surface_access_departure
                          + delta_v_escape
                          + delta_v_capture
                          + surface_access_arrival
```

Surface access is an explicit endpoint/gameplay policy. It must not be disguised as part of Lambert geometry. True finite-burn atmospheric ascent, descent, and low-thrust spirals are outside the implemented model.

### Required Celestial Inputs

Each body participating in a full transfer needs authored or legitimately derived values for:

- gravitational parameter `mu`;
- physical radius;
- sphere-of-influence radius, or sufficient parent/orbit data to derive it;
- orbital state or elements needed to evaluate position and velocity at arbitrary epochs;
- parking-orbit altitude where spaceship endpoints use orbit access;
- endpoint location policy such as surface or orbit;
- optional rotation and atmosphere data only if a future model explicitly consumes them.

The rebuild intentionally provided complete transfer data only for Vael, Mars, and Overworld. Other bodies remain unavailable until real design data is authored.

### Gameplay And Progression Context

The broader design distinguished transport methods rather than treating them as interchangeable:

- automated outposts depend on ships or railgun logistics instead of ordinary inventory links;
- conventional HAMMER transport is suitable for shorter or intra-system routes;
- an advanced interplanetary railcannon can be a later progression capability;
- spaceships support controlled arrival, docking, and movement where payload or crew survival matters;
- receiver storage, docking queues, throughput, and downstream surface delivery are logistics concerns outside trajectory solving;
- physical feasibility must not automatically become a progression bypass;
- the strategic Star Map is an abstraction and must not promise a literal AU-to-screen or block-to-orbit scale.

These distinctions are the strongest potential gameplay reason to retain separate railgun and spaceship evaluations. They do not, by themselves, prove that local conic arcs need to be visibly rendered.

### Licensing And Clean-Room Record

The implementation policy was to derive mathematics from primary literature and use permissively licensed projects only as validation references:

- Dario Izzo's *Revisiting Lambert's Problem* is the primary mathematical reference for Lambert formulation and branch behavior.
- ESA PyKEP is BSD-3-Clause and was treated as a reference implementation, not copied into Galaxia.
- poliastro is MIT-licensed and was treated as additional reference material.
- Orekit and Tudat were useful for conceptual or numerical validation but were not selected as code sources under the preferred project licensing constraints.
- no third-party Lambert implementation or runtime dependency was copied into the rebuild;
- any future continuation should preserve a short provenance note and validate independently derived equations against published cases.

## External Technical Sources

- Dario Izzo, *Revisiting Lambert's Problem*, arXiv:1403.2705.
- ESA PyKEP documentation and source were used as a BSD-3-Clause reference point, not copied as an implementation dependency.
- poliastro documentation and source were treated as MIT-licensed reference material.
- Orekit and Tudat documentation were useful validation references but unsuitable as code sources under the preferred licensing constraints.

## Related Topics

- Deferred
