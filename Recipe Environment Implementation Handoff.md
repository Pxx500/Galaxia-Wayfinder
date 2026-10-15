---
type: execution-tracker
status: blocked-room-data
date: 2026-10-10
tags:
  - galaxia/alpha
  - galaxia/execution
---

# Recipe Environment Implementation Handoff

## Current Status

The 2026-10-10 checkpoint proved a bounded GT singleblock pause hook in development and a built development JAR. Full environment integration remains blocked by ambiguity between unresolved room data and verified exterior exposure.

The recorded checkpoint changed only disposable game-test instrumentation. It did not deliver the production authoring helper, tag enforcement, EBF integration, Room Pressure Level or controller bar. This is the last recorded status, not a fresh code audit.

## Decision Owners

- [[Define Celestial Capability Rules]] owns tags, optional integration, observation position, room pressure and retained-work pause
- [[Design Early Orbital Production Recipe Chain]] owns GT-bound staging and production content
- [[CONTEXT]] owns domain vocabulary
- [[Consolidate Physical Station Architecture]] owns the boundary that defers room-detection and side-classification redesign

## Agreed Delivery Scope

Deliver recipe environment requirements from Galaxia without GT source changes. Galaxia remains the environment authority. Use existing GT metadata, a small helper returning the normal builder and bounded temporary late mixins, not a provider framework or copied builder.

The temporary authoring entry is `requiresEnvironment(MICROGRAVITY, NO_ATMOSPHERE)`, followed by GT's normal builder operators. Multiple tags are conjunctive and independent of `mSpecialValue`. The future native GT builder method requires separate maintainer alignment.

Acceptance covers EBF, ordinary Fluid Solidifier and ordinary Extruder, with:

- A pre-consumption environment check that preserves existing requirements, including EBF heat, caching, locking and parallel processing
- One committed operation retained through environmental pause and resume, without repeated consumption, output rerolls or process-energy drain while paused
- Save/reload retention of the operation's requirement, progress and pending outputs
- Normal housekeeping and exact passthrough for unrestricted recipes, including one following a tagged operation
- Translated NEI requirements and client-visible rejected or paused status, retaining EBF heat information
- Actual containing-room conditions, including connected secondary rooms. Multiblocks observe only the controller
- Development and built-JAR runtime verification of the instrumentation, not just unit tests or successful injection counts

GT-bound requirement infrastructure is temporarily staged under Galaxia's `gt5` package. Environment definitions, celestial classification, room lookup and pressure remain Galaxia responsibilities. Temporary mixins are removed after equivalent native GT hooks exist.

When Galaxia is absent, this delivery's hooks and tagged additions are absent. Existing GT requirements remain intact. Direct tagged authoring and hidden-and-ignored behavior in GT without Galaxia belong to the later API transfer. With Galaxia loaded, unresolved conditions never count as satisfied or as the absent-mod case.

## Demonstrated Blocker

`RoomPressureDataCheckpoint.unresolvedRoomDoesNotProveExteriorExposure` formed two sealed rooms and registered both with an airlock, then replaced the far room's controller with a normal wall. The shell remained closed, but that room became unresolved. The airlock reported `isExternalConnection() == true` because fewer than two tracked controllers are classified as exterior.

The test reached its final exposure assertion after both rooms had validated and the unchanged boundary had been checked. The same signal therefore represents either real exterior access or missing room/controller data. Existing seal and vacuum queries consume it as breach evidence.

Using this signal to empty pressure violates the accepted unknown-versus-exterior distinction. Treating all unresolved sides as sealed would instead miss real exterior vacuum. Continuing requires an agreed distinction from the existing room/airlock owner. Do not invent a second geometry engine or rescan per recipe to bypass that boundary.

The owner-selected pressure policy remains in [[Define Celestial Capability Rules]]. The blocker does not reopen it or authorize a room redesign.

## Exclusions And Open Boundaries

This task excludes full production chains, technology blueprints, team-knowledge gates, vacuum pumps, vacuum-on-demand, connectivity redesign and global replacement of GT cleanroom or LOW_GRAVITY behavior.

The numerical microgravity cutoff remains tuning. Zero gravity is a positive fixture, while Luna at `0.25` and Overworld at `1.0` are negative fixtures. A reachable early orbital workshop is separate gameplay work, not proven by using Frozen Belt or Luna as fixtures.

## Dated Checkpoint Evidence

The 2026-10-10 checkpoint reports retained progress and outputs, no process-energy drain during pause, automatic resume with one completion, unrestricted passthrough and auto-output housekeeping. The test-owned condition was deliberately independent of real room pressure.

These results establish the narrow pause checkpoint, not completion of production integration. Current code, dependencies and runtime hooks need checking when work resumes.
