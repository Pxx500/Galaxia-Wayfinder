---
type: implementation-issue
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
source_decision: "[[Define Alpha Observation Opening]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Prospecting Satellite Range Feedback

## Durable Requirement

Expose the existing visibility and scanning ranges in the normal Star Map through a global, localized `Show satellite ranges` checkbox. This is a non-blocking implementation follow-up, not a new sensor tier or a gameplay range rebalance.

- The outer range shows where eligible objects become visible. The inner range shows where visible objects can be scanned.
- Satellites are properties of their host bodies, not independently selectable Star Map objects. The global control does not depend on selecting or hovering a satellite.
- Enabling the overlay shows both ranges for every relevant satellite.
- Visibility coverage merges into one field and scanning coverage into another. Same-type overlaps must not darken, form internal seams, or duplicate outlines.
- Scan coverage takes precedence over visibility-only coverage, including overlaps between different satellites.
- Both meanings must be understandable without relying on color alone.
- Rendering consumes authoritative gameplay ranges rather than maintaining its own range values.

## Performance Requirement

When disabled, the overlay performs no coverage preparation or rendering. When enabled, coverage handling must have bounded practical cost with representative satellite counts and overlaps. Do not unconditionally rebuild expensive coverage geometry every frame or tick. Choose and profile the technique during implementation rather than preserving an untested cache or rendering design here.

## Deferred Choices

- Default enabled or disabled state.
- Colors, opacity, legend, and exact presentation.
- Rendering technique, supported runtime primitives, and any measured need for caching.
- The authoritative outer visibility range and integration with the existing renderer.

## Evidence and Provenance

Inspection on 2026-09-12 identified the inner scan radius in `registry/satellite/SatelliteDiscoveryWorkerSource.java:21` (`PROSPECTING_SCAN_RADIUS`) and its use by `prospectingScope` at line 57. Eligible Prospecting Satellites contribute through `prospectingWorkers` at line 26. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. The outer visibility radius was not established by this bounded audit. Existing scan authority does not prove that the normal-map overlay is implemented.

## Gameplay Flow

The deferred overlay would let the player enable satellite visibility and scanning coverage on the Star Map. Scanning coverage would take precedence where the fields overlap, with the two meanings distinguishable without color alone.
