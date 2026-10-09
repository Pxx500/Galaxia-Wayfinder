---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Celestial Capability Rules

## Question

Which authored celestial, environmental, surface, atmosphere, gravity, and orbital properties should grant or constrain reusable object-native capabilities such as gas extraction, mining, solar generation, outposts, stations, and transport endpoints?

## Resolution

Object-native capability rules are established by the accepted requirements below. Environmental facts determine eligibility, and asteroid Outposts do not require a Station orbit. Numerical orbit eligibility, solar calibration, and physical implementation remain content and tuning work. They do not reopen the agreed capability model or block the asteroid-specific contract.

Consolidated on 2026-09-12 from existing owner decisions, without approving new numerical rules or certifying implementation.

## Accepted Requirements

- Celestial Objects author physical and domain facts rather than arbitrary per-machine capability flags. Gameplay systems derive their eligibility and behavior from those facts.
- Gas Siphon and ordinary atmospheric gas collection are separate extraction systems.
- Gas Siphon is exclusive to Gas Giants and uses their authored atmospheric gas data. It remains a separate machine and access method from ordinary surface collection.
- A rocky or otherwise solid planet with an atmosphere does not become Gas Siphon-compatible merely because its atmosphere contains useful gases. Any ordinary atmospheric collection uses a separate capability and machine contract.
- A Gas Siphon is an orbital module of a Celestial Asset associated with the Gas Giant. It is not placed on a fictional gas-giant surface.
- The capability may be provided by a module on a physical Station or by a module in an Automated Facility. Both reuse the Gas Giant's ordinary authored atmosphere composition and pressure data, while energy, inventory, and logistics follow the owning asset's normal model.
- Gas Siphon does not introduce a separate deep-resource profile. Its distinction from ordinary atmospheric collection is the eligible object and access method, not a duplicated source of gas composition data.
- `Solid Surface` is one shared authored property for gameplay that requires accessible stable terrain.
- A Celestial Object without a Solid Surface cannot support Unprepared Landing, a Silo or Rocket Pad, a physical surface Transport Endpoint, a surface Automated Outpost, ordinary surface mining, or construction that requires terrain.
- A Celestial Object without a Solid Surface may still support capabilities provided by another valid Body Environment or Eligible Orbit. Gas Giants support orbital Gas Siphon, while minor asteroids support zero-gravity Automated Outposts.
- Systems use Solid Surface instead of maintaining parallel flags such as `canLand`, `canMine`, `canBuildOutpost`, or `canPlaceSilo`.
- Baseline solar availability derives from the system's light source and the Celestial Object's position rather than a `goodForSolar` capability flag.
- Each Celestial Object may also author one general Solar Resource Modifier for balance and exceptional local conditions. The final object-level solar modifier is visible in the Star Map.
- Asset placement then applies the relevant surface or space environment behavior. Surface generation may experience atmosphere and illumination cycles, while space-based generation avoids ordinary atmospheric loss.
- Solar presentation separates Daylight Solar Intensity from Average Solar Yield. Overworld daylight intensity is the `1.0x` instantaneous reference, while the complete Overworld day-night cycle is the `1.0x` long-term yield reference.
- The Star Map presents Average Solar Yield as the primary comparison. Its breakdown includes daylight intensity, light and dark duration, atmosphere, and the authored Solar Resource Modifier.
- Actual surface production follows local illumination. Day and night duration remain separately visible because equal average yield can create different energy-storage requirements.
- A Celestial Object's gravitational orbit and a Celestial Asset's Space Environment are separate concepts.
- A Station requires an Eligible Orbit. Major planets, moons, Gas Giants, and other bodies with sufficient authored orbital facts may host one.
- Minor asteroids and other bodies with insufficient gravity do not have an Eligible Orbit and cannot host an Automated Station.
- A minor asteroid instead hosts a body-anchored Automated Outpost. The Outpost operates in zero gravity, may provide a Dock for Spaceships, and combines local extraction with the space-logistics capabilities needed at that body.
- Allowing a Dock on an asteroid Outpost does not turn the Outpost into a Station and does not claim that the asteroid has an orbit.
- Direct `canCreateStation` and `canCreateOutpost` flags are not part of the target capability model. Placement derives from reusable Asset Environments and the associated Celestial Object's facts.
- A Body Environment represents an asset anchored directly to a Celestial Object. A Surface Environment is the Solid Surface form of that environment. A Space Environment represents vacuum and zero-gravity operating conditions and may apply to an orbital Station or to a body-anchored asteroid Outpost.
- Automated Outposts use a valid Body Environment. Automated Stations require an Eligible Orbit and use a Space Environment.
- Ordinary atmospheric gas collection requires a physical dimension, positive authored surface pressure, and at least one authored atmosphere ingredient.
- Ordinary atmospheric collection and Gas Siphon use the same atmosphere composition and pressure facts. Pressure may affect collection throughput or compression cost.
- Authored planetary and Gas Giant atmospheres are inexhaustible gameplay sources. Collection does not decrease a global atmosphere reservoir or require atmosphere regeneration.
- Atmosphere extraction is limited by machine throughput, energy, infrastructure, gas concentration, and pressure rather than a finite planetary stock counter.
- Every Celestial Asset derives one shared set of Environmental Properties from the associated Celestial Object, its Asset Environments, and its own modules or protections.
- Systems such as Gas Siphon, Solar Generator, Miner, and transport infrastructure read the Environmental Properties they need instead of copying celestial facts or defining machine-specific location flags.
- `CelestialBodyProperties` is the canonical authored source for environmental facts. Playable-dimension hazards and other runtime environment views derive from it instead of separately authoring the same temperature, pressure, radiation, or atmosphere values.
- Celestial icon textures, observer-relative sky-body rendering, cubemap skyboxes, and decorative enhanced-sky layers are distinct presentation concerns. A body icon is not automatically a usable sky texture.
- Every dimension actually registered by Galaxia must resolve to one registered `CelestialObject`. This is a hard registry invariant even when the dimension's gameplay profile is incomplete.
- Register Tenebrae as a Celestial Object records the completed minimal registration decision. Tenebrae remains a non-playable scaffold until its separate gameplay contract is designed.
- Minecraft biome temperature such as Mars `0.4F` remains unchanged until its independent vanilla climate behavior is understood. It is not treated as the canonical celestial hazard temperature.
- Existing skybox, sky-body, and enhanced-sky rendering remain outside the current cleanup because another contributor owns that visual work. The ownership model may be documented without changing their assets or rendering behavior.

## Production Environment Requirements

On 2026-09-17 the owner explicitly separated microgravity from absence of atmosphere. These are recipe environment conditions, not a generic must-be-on-a-Station or must-be-in-orbit flag.

- Silicon-germanium crystal growth and specialty fluoride optical-fiber production require microgravity in the intended Galaxia gameplay. Orbit is one way to provide those conditions, not the exclusive allowed location.
- Space-Grade Alloy requires absence of atmosphere and has no microgravity requirement. Luna is an accepted location because it is airless despite having surface gravity.
- Other production chains may use either condition, both when justified, or neither. Do not impose either requirement on every Galaxia material.
- The existing distinction between physical Station inventories and abstract Automated Facility capabilities remains. A suitable environment does not by itself supply an absent machine or module.
- Exact thresholds remain tuning. The NASA research motivates the microgravity benefit, while the recipe restriction is an explicit gameplay choice rather than a claim that terrestrial manufacture is physically impossible.

### Accepted Environment Tags

On 2026-10-08 the owner selected checkable tags for every environment. Tags describe environmental conditions such as Microgravity and No Atmosphere, not team membership or Technology Knowledge. An environment may have several tags at once, and recipes declare the environmental tags they require. A recipe may require either example independently or both where justified.

Galaxia owns the environmental facts and the tags exposed from them. GT5 uses those tags to enforce recipe requirements before consuming ingredients. Keep this classification on the Galaxia side when staged items and recipes move to GT5. Tags must remain coherent with the accepted physical-property model rather than becoming independent per-recipe planet whitelists.

On 2026-10-10 the owner explicitly concentrated environment definitions and evaluation in Galaxia. Do not create a competing environment catalog or an open collection of environment providers in GT. If extensions add tags, they do so through Galaxia's API and remain under its environment model. GT only needs neutral requirement references and the integration needed to check and display them without a reverse runtime dependency.

On 2026-10-10 the owner selected a new optional recipe environment requirement in GT, independent of `mSpecialValue`. A recipe without this requirement has no environmental restriction from this system. A recipe with the requirement must have all of its required tags satisfied at the execution location, subject to the explicitly accepted absent-Galaxia development behavior below. Existing voltage, heat, cleanroom and other recipe requirements remain independent. Do not encode these extra tags through the old special-value sentinels.

The owner requires a readable fluent method on the GT recipe builder to declare this optional requirement, rather than making recipe authors manipulate raw metadata or special values. On 2026-10-10 they delegated technical representation and naming to the developer, with convenient handwritten recipes as the acceptance criterion. The selected authoring direction is `requiresEnvironment(...)` with named, typed tag values exposed as constants. Several supplied tags mean that all are required. A closed Java enum is not required. This preserves enum-like IDE completion without preventing tag registration through Galaxia's API. Neutral references must be usable by GT recipe authors without loading Galaxia classes, while Galaxia owns tag definitions, classification and evaluation. Developers adding an ordinary recipe should only choose the constants, not wire an evaluator or understand room lookup. Exact internal types and wiring are implementation details to derive when execution begins. This records the authoring contract, not an implemented builder method or tag type.

On 2026-10-10 the owner accepted an Alpha room atmosphere state that distinguishes Vacuum from Atmosphere without a full simulation of pressure or gas composition. Galaxia derives No Atmosphere from the actual absence of atmosphere, not from sealing alone or lack of oxygen. Use the Station's existing room membership and local state rather than rescanning geometry for each recipe. The precise transitions that fill or empty a room remain to be defined.

### Deferred On-Demand Vacuum

On 2026-10-10 the owner excluded deliberate room evacuation and vacuum-on-demand mechanics from the current Alpha scope. The idea is interesting future work, not an implementation prerequisite. Alpha may use natural vacuum and local atmosphere states, but sealing a room on an atmospheric world must not itself create vacuum. Do not add a pump, evacuation mode or alternative vacuum-creation mechanic for this recipe integration.

### Evaluation And Integration Boundaries

This establishes the contract, not an implemented API. Tag representation, cross-mod access and exact enforcement points remain implementation work. Local conditions affect the effective environment tags where applicable. The simplified room atmosphere state is not a complete pressure model.

On 2026-10-10 the owner accepted suspending a running recipe when its required environmental conditions cease to hold. Retain its committed ingredients and progress, and resume when the requirements are met again. This is a gameplay contract, not evidence that current GT processing already supports this behavior.

The owner also requested an explicit GT-only development behavior: when Galaxia is absent, hide and silently ignore the additional environmental requirements supplied by Galaxia. This optional-integration behavior is authorized for development convenience. It is not a request to bypass unrelated existing GT requirements such as cleanroom. An unavailable room or unresolved local condition while Galaxia is loaded is a different case, not automatically covered by the absent-mod rule.

On 2026-10-10 the owner selected the multiblock controller's position as the observation point for Alpha recipe environment checks. Do not require matching conditions across the whole structure. This deliberately defines the result for a machine crossing a room boundary by its controller's environment. A broader spatial rule can be considered later but is not an Alpha prerequisite.

Bounded source inspection on 2026-10-08 at Galaxia `a9128e9ef21ff05254648190b4f79f94bdc9669d` found `GalaxiaAPI.getStationAround(World, int, int, int, int):403-422`, `TileStationBase.isInside():182-199` and `ArbitraryShapeDefinition.isInsideStructure():197-204`. The lookup visits Station assets and their controllers, while the arbitrary room membership check reads stored validation data. `TileStation:113-119` exposes oxygenation and oxygen level. `HazardPressure:38-41` treats a sealed room as pressure-safe but does not expose its actual pressure. These are usable inputs, not a complete environment-tag query. Connected rooms and lookup cost still need attention when integrating the query.

## Implementation and Tuning Follow-ups

- Station placement requires a usable orbit. The numerical orbit criterion is not yet established and must be checked against authored bodies during implementation.
- The existing facts already distinguish body-anchored asteroid Outposts from orbital Stations. `Body Anchor` was proposed in an unanswered question and is not an accepted additional property.
- Dock access follows vehicle and local environmental conditions. Asteroid Outpost docking is accepted. A new blanket rule requiring a named `Space Environment` flag is not separately approved.
- Environment names in these notes describe gameplay relationships. Their existence does not require an enum, registry, class hierarchy, or copied property store.
- Physical surface availability, physical visitability, and a persistent asteroid's abstract body anchor are distinct. Absence of a playable dimension does not mean absence of material to extract.
- Solar comparison labels are accepted. Surface day/night durations and numerical calibration remain tuning questions. For the current Station-orbit model, the owner assumes a geostationary orbit with continuous full sunlight. Planet-shadow interruptions and an orbital light/dark cycle are not part of the current scope.
- Continuous sunlight is an explicit gameplay simplification, not a physical consequence guaranteed by a geostationary orbit. It does not set solar output to the same value around every body or remove distance and authored solar modifiers.

## Current Implementation Boundary

Source inspection on 2026-09-12, under `src/main/java/com/gtnewhorizons/galaxia/`:

- `registry/celestial/CelestialBodyProperties.java:20` still exposes direct visitability and Station/Outpost flags, consumed by `core/network/AssetCreateRequestPacket.java:148`. The accepted derived eligibility model is not implemented by those flags.
- `registry/celestial/asteroid/AsteroidCelestialMaterializer.java:104` marks generated asteroids Station-ineligible and Outpost-eligible. That result agrees with the accepted asteroid facility distinction, without establishing a numerical orbit criterion.
- `CelestialBodyProperties` owns pressure and atmosphere ingredients but has no accepted Solar Resource Modifier field in the inspected property model. Existing render brightness is not evidence of solar-production implementation.
- `registry/celestial/CelestialRegistry.java:240` and `:248` still author Mars temperature separately in body properties and dimension effects. The shared environment authority remains an implementation requirement.

These findings do not reopen the resolved gameplay model or certify all placement and extraction paths.
