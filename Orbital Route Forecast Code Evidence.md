---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Orbital Route Forecast Code Evidence

Source: Read-only investigations of Galaxia commit a9128e9ef21ff05254648190b4f79f94bdc9669d during the owner's route-forecast planning request
Imported: 2026-10-07

## Source Snapshot

Graph indexing returned aborted_previous_preserved and several graph source ranges were stale. Findings were checked against the actual checkout. These are source observations and derived counts, not approval of a design or proof of completed implementation.

### Orbital Motion

OrbitalMechanics adds parent and child motion and supports eccentricity. Effective speed derives from positive attractor gravity and radius. Authored orbitSpeed supplies direction rather than an independent speed magnitude.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/orbital/OrbitalMechanics.java:56`, `:109`, `:155`, `:170`, `:181`, `:226`.

The registry has 38 circularOrbit authoring calls and no eccentric-orbit authoring call found by this inspection. Callisto is registered under Jupiter, so its world state contains both motions.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/CelestialRegistry.java:788`.

### Asteroid Field

GeneratedAsteroids uses sizeCounts(40, 80, 200), totaling 320 generated bodies, and a radial band from 2.15 to 2.45 AU in the authored scale.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/asteroid/content/GeneratedAsteroids.java:21`.

AsteroidFieldOrbitResolver explicitly supplies the belt's angular velocity to each asteroid with its own fixed radius and angle. It uses the supplied world-space belt state and returns positions around the world origin.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/asteroid/AsteroidFieldOrbitResolver.java:34`, `:65`.

SOL is at absolutePosition(0.0, 0.0). FROZEN_BELT is circular, directly under SOL, and has the only current asteroidFieldProfile attachment. BARNARDA is at (5800, -2600), but its authored belt has no generated minor-body profile. The current generated field supports rigid SOL-centered rotation. Extending that resolver to an offset star requires checking its reference frame.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/CelestialRegistry.java:112`, `:126`, `:1492`, `:1529`, `:1626`.

### Trajectories And Existing Sharing

OrbitalTransferPlanner scans 64 time-of-flight candidates between 0.1 and 3.0 times the Hohmann scale. Each candidate evaluates both Lambert directions. It selects a preferred duration and branch before receiving vehicle fuel, thrust or a route fuel cap. TransferRoute retains separate departure and capture delta-v plus duration.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/orbital/OrbitalTransferPlanner.java:67`, `:124`, `:147`, `:174`, `:226`, `:289`.

HammerDispatchPlanner shares ordered source/destination/priority calculations inside one fixed-time inspection pass. ModuleHammer throttles failed probes. These are not multitime Rocket forecasts.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/outpost/logistics/HammerDispatchPlanner.java:52`, `:82`, and `src/main/java/com/gtnewhorizons/galaxia/registry/outpost/module/types/ModuleHammer.java:192`.

### Rocket Prototype

RocketStage accumulates nominal capacities, subtracts that scalar from mass, and uses Isp 300. EnginePartDef has thrust but no complete propulsion recipe. FuelTankPartDef has scalar capacity. RocketPartInstance records definition and placement without actual fuel inventory.

Evidence: `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/analysis/RocketStage.java:33`, `:38`, `:40`, `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/modules/EnginePartDef.java:3`, `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/modules/FuelTankPartDef.java:3`, and `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/blueprint/RocketPartInstance.java:7`.

### Derived Workload Counts

At 64 departure samples, one profile has 4096 duration candidates and up to 8192 Lambert branch evaluations. Three radius profiles have up to 24576 branch evaluations. Separate profiles for 320 targets would have up to 2621440 branch evaluations for one source.

The 320 generated bodies have 102080 directed within-field pairs. Applying full sampling to every pair produces 836239360 branch evaluations. These counts do not include all solver iteration or state-resolution cost and are not measured execution times.

No builds, game runs or runtime benchmarks were performed.

Return to [[Sources]].
