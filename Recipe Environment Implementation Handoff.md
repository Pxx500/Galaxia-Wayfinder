---
type: execution-tracker
status: delivered-local
date: 2026-10-23
tags:
  - galaxia/alpha
  - galaxia/execution
---

# Recipe Environment Implementation Handoff

## Current Status

On 2026-10-23 the owner explicitly replaced retained-work pause with the existing GT process failure semantics. Loss of a required environment must follow the machine's ordinary power-failure behavior. Singleblocks restart progress through GT's existing path, while multiblocks cancel the operation and discard pending outputs. Do not add a separate pause/resume engine or new operation-retention guarantees.

The owner also accepts the current controller-backed room model. Removing a room controller removes that room and its local atmosphere data from the model, even if the physical shell remains closed. The controller-to-wall scenario is accepted behavior for now, not a bug to fix or a blocker. Do not broaden this delivery to preserve controllerless rooms or redesign room detection and airlock side classification.

The 2026-10-10 checkpoint proved a bounded GT singleblock pause hook in development and a built development JAR. That mechanism is now a superseded experiment and must not be introduced into the production integration. The previous room-data blocker is withdrawn under the owner's clarified contract.

Production implementation now exists on the local `recipe-environments` branch in `~/Documents/GitHub/Galaxia/worktrees/recipe-environments`. It provides the authoring helper, metadata and NEI rendering, enforcement before consumption, native GT runtime failure, active-requirement NBT, Room Pressure Level and the controller bar. The changes remain local and uncommitted. A complete patch, checked against base 092ad1800bbbaa96dc8f2bac6d6ccfa45e32e852, is available at `~/.agents/docs/Galaxia/worktrees/recipe-environments/docs/integration/recipe-environments.patch`.

The final 2026-10-23 Horizon-QA run `build/horizonqa/environment-copy` passed all three selected scenarios and exited normally. They exercise ordinary Extruder and Fluid Solidifier rejection and power-failure reset, EBF's inherited ProcessingLogic and heat validation, EBF native shutdown with discarded pending outputs, physical pressure decay and airlock equalization, a real oxygenator supplied with oxygen and energy, breach venting, the actual controller GUI, and ordinary/shallow recipe copies retaining the environment requirement. The copy constructor needed a fourth narrow mixin because this GT version deliberately drops metadata in native copies.

The complete ordinary build passed with 961 JUnit tests, zero failures and zero errors, plus Spotless and Checkstyle. `agentVerify` is absent in this checkout, so its documented components were run directly. PMD completed. IntelliJ exported findings but reported internal inspection errors, so the combined audit is not clean or complete. Full evidence and finding dispositions are in `~/.agents/docs/Galaxia/worktrees/recipe-environments/docs/reviews/recipe-environments-verification.md`.

The public authoring imports are `com.gtnewhorizons.galaxia.api.RecipeEnvironments.requiresEnvironment`, `MICROGRAVITY` and `NO_ATMOSPHERE`. `requiresEnvironment(Tag...)` returns the normal `GTRecipeBuilder`. Extensions use `RecipeEnvironments.register(...)`. Initial tags read gravity and actual local pressure rather than generic station membership.

## Decision Owners

- [[Define Celestial Capability Rules]] owns tags, optional integration, observation position and controller-backed room pressure
- [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]] owns the shared failure contract, superseding retained-work requirements
- [[Design Early Orbital Production Recipe Chain]] owns GT-bound staging and production content
- [[CONTEXT]] owns domain vocabulary
- [[Consolidate Physical Station Architecture]] owns the boundary that defers room-detection and side-classification redesign

## Agreed Delivery Scope

Deliver recipe environment requirements from Galaxia without GT source changes. Galaxia remains the environment authority. Use existing GT metadata, a small helper returning the normal builder and bounded temporary late mixins, not a provider framework or copied builder.

The temporary authoring entry is `requiresEnvironment(MICROGRAVITY, NO_ATMOSPHERE)`, followed by GT's normal builder operators. Multiple tags are conjunctive and independent of `mSpecialValue`. The future native GT builder method requires separate maintainer alignment.

Acceptance covers EBF, ordinary Fluid Solidifier and ordinary Extruder, with:

- A pre-consumption environment check that preserves existing requirements, including EBF heat, caching, locking and parallel processing
- Loss of a required environment uses the existing GT power-failure path and its normal machine-specific consequences, rather than a separate retained-work pause
- No new progress/output preservation or save/reload guarantees beyond the native GT operation lifecycle
- Normal housekeeping and exact passthrough for unrestricted recipes, including one following a tagged operation
- Translated NEI requirements and appropriate existing machine failure/status reporting, retaining EBF heat information
- Actual containing-room conditions, including connected secondary rooms. Multiblocks observe only the controller
- Development and built-JAR runtime verification of the instrumentation, not just unit tests or successful injection counts

The authoring and requirement owner is `com.gtnewhorizons.galaxia.api.RecipeEnvironments`. Temporary GT integration is under `com.gtnewhorizons.galaxia.mixin.gt`, loaded by a dedicated late loader. Environment definitions, celestial classification, room lookup and pressure remain Galaxia responsibilities. Temporary mixins are removed after equivalent native GT hooks exist.

When Galaxia is absent, this delivery's hooks and tagged additions are absent. Existing GT requirements remain intact. Direct tagged authoring and hidden-and-ignored behavior in GT without Galaxia belong to the later API transfer. With Galaxia loaded, unresolved conditions never count as satisfied or as the absent-mod case.

## Superseded Room-Data Finding

`RoomPressureDataCheckpoint.unresolvedRoomDoesNotProveExteriorExposure` formed two sealed rooms and registered both with an airlock, then replaced the far room's controller with a normal wall. The shell remained closed, but that room became unresolved. The airlock reported `isExternalConnection() == true` because fewer than two tracked controllers are classified as exterior.

The test reached its final exposure assertion after both rooms had validated and the unchanged boundary had been checked. The same signal therefore represents either real exterior access or missing room/controller data. Existing seal and vacuum queries consume it as breach evidence.

The owner has clarified that rooms require controllers. Losing the controller and associated atmosphere data is an accepted consequence. The diagnostic's expectation that a controllerless enclosure remain a modeled room is no longer a required contract. Do not retain it as a failing acceptance test or use it to block implementation. No new exterior-versus-controllerless distinction is required for this delivery.

The current pressure policy, including controller-backed room ownership, lives in [[Define Celestial Capability Rules]]. This finding does not authorize a room redesign.

## Exclusions And Open Boundaries

This task excludes full production chains, technology blueprints, team-knowledge gates, vacuum pumps, vacuum-on-demand, connectivity redesign and global replacement of GT cleanroom or LOW_GRAVITY behavior.

The numerical microgravity cutoff remains tuning. Zero gravity is a positive fixture, while Luna at `0.25` and Overworld at `1.0` are negative fixtures. A reachable early orbital workshop is separate gameplay work, not proven by using Frozen Belt or Luna as fixtures.

## Dated Checkpoint Evidence

The 2026-10-10 checkpoint reports retained progress and outputs, no process-energy drain during pause, automatic resume with one completion, unrestricted passthrough and auto-output housekeeping. The test-owned condition was deliberately independent of real room pressure.

These results establish only the superseded pause experiment, not completion of production integration. They must not be presented as acceptance evidence for the newly selected GT failure semantics. Current code, dependencies and runtime hooks need checking when implementation resumes.
