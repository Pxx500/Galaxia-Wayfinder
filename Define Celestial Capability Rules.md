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

Which authored celestial and environmental facts grant or constrain extraction, power, facilities and transport capabilities?

## Resolution

Derive eligibility from physical and domain facts, not per-machine location flags. The model is accepted. Numerical orbit eligibility, solar calibration and implementation remain separate work.

## Shared Environmental Authority

`CelestialBodyProperties` is the canonical authored source for temperature, pressure, radiation, atmosphere and related facts. Playable-dimension hazards and runtime views derive from it rather than reauthoring values.

Every Celestial Asset derives Environmental Properties from its associated object, Asset Environments and modules or protections. Machines and transport read the properties they need rather than copying facts or adding location flags.

Every dimension registered by Galaxia must resolve to one registered `CelestialObject`, even with an incomplete gameplay profile. Tenebrae's minimal registration does not make it playable. Vanilla biome temperature, such as Mars `0.4F`, is separate from celestial hazard temperature and remains unchanged until its climate behavior is understood.

Body icons, observer-relative sky-body rendering, cubemap skyboxes and decorative enhanced-sky layers are different presentation concerns. An icon is not automatically a sky texture. Existing sky rendering and assets remain outside this cleanup.

## Surface, Orbit and Facility Eligibility

- Solid Surface is the shared fact for accessible stable terrain. Without it, no Unprepared Landing, Silo, Rocket Pad, physical surface Transport Endpoint, surface Automated Outpost, ordinary surface mining or terrain-dependent construction is available.
- Do not maintain parallel `canLand`, `canMine`, `canBuildOutpost` or `canPlaceSilo` flags.
- A Body Environment anchors an asset directly to an object. A Surface Environment is its Solid Surface form.
- A Space Environment describes vacuum and zero gravity, not gravitational orbit. It may apply to an orbital Station or a body-anchored asteroid Outpost.
- Stations need an Eligible Orbit. Major planets, moons, Gas Giants and other sufficiently authored bodies may qualify. The numerical criterion remains open.
- Minor asteroids lack Eligible Orbits. They may host zero-gravity, body-anchored Automated Outposts with extraction and Docks, not Automated Stations.
- Dock capability does not turn an asteroid Outpost into a Station. Vehicle and local conditions govern docking, without a separately approved blanket Space Environment flag.
- Placement derives from the associated object's facts and valid environments, not direct `canCreateStation` or `canCreateOutpost` flags.
- Physical surface availability, visitability and an abstract persistent asteroid anchor are distinct. No playable dimension does not mean no extractable material.
- Body Anchor was an unanswered proposal, not an additional accepted property. Environment names do not require an enum, registry or class hierarchy.

## Gas Extraction

Gas Siphon is exclusive to Gas Giants and operates as an orbital Celestial Asset module, on a physical Station or Automated Facility. It does not use a fictional surface. A solid planet's useful atmosphere does not make it Siphon-compatible.

Ordinary atmospheric collection is a separate machine/capability and requires a physical dimension, positive authored surface pressure and at least one atmosphere ingredient. Both systems reuse ordinary composition and pressure facts, not a separate deep-resource profile. Pressure may affect throughput or compression cost. Energy, inventory and logistics follow the owning asset.

Planetary and Gas Giant atmospheres are inexhaustible gameplay sources. Throughput, energy, infrastructure, gas concentration and pressure limit collection, not a global stock or regeneration counter.

## Solar Resources

Baseline availability follows the system's light source and the object's position. Each object may add one authored Solar Resource Modifier for balance or exceptional conditions, visible in the Star Map.

Distinguish Daylight Solar Intensity from Average Solar Yield. Overworld daylight is the instantaneous `1.0x` reference, while its full day-night cycle is the long-term `1.0x` yield reference. Average yield is the primary Star Map comparison, with daylight intensity, light/dark duration, atmosphere and authored modifier in its breakdown.

Surface generation follows actual illumination and atmospheric effects. Separate day/night durations expose storage needs even at equal average yield. Space avoids ordinary atmospheric loss.

The current Station-orbit model assumes geostationary placement with continuous full sunlight. Planet shadows and orbital light/dark cycles are out of scope. This gameplay simplification does not equalize output across bodies or remove distance and authored modifiers.

## Recipe Environment Contract

Microgravity and No Atmosphere are independent requirements, not generic Station or orbit flags:

- SiGe crystal growth and specialty fluoride optical-fiber production require microgravity.
- Space-Grade Alloy processing and recycling require No Atmosphere, including generated material recipes. Luna qualifies despite surface gravity.
- Other processes may need either, both or neither. A suitable environment does not supply missing machinery or Automated Facility modules.

These are gameplay choices motivated by research, not claims that terrestrial manufacture is physically impossible. Thresholds remain tuning.

Galaxia owns tag definitions, classification and evaluation. Extensions register through Galaxia's API, not a competing GT catalog or open provider collection. Tags describe conditions, not team membership or Technology Knowledge.

Recipes may declare an optional requirement independent of `mSpecialValue`. All supplied tags must hold at execution. Recipes without it gain no restriction from this system. Voltage, heat, cleanroom and other requirements remain independent.

The accepted authoring target is a readable `requiresEnvironment(...)` fluent method with named typed constants and IDE completion. A closed enum is not required. GT authors should use neutral references without loading Galaxia classes or wiring evaluators. Exact types and wiring remain implementation choices.

For Alpha, observe the multiblock controller's position, not every block of its structure. If conditions fail during a recipe, suspend it with committed ingredients and progress retained, then resume when conditions return.

## Room Pressure

A physical Room owns one bounded Room Pressure Level shared by all its controllers. Zero is Vacuum and full is full atmosphere. The controller shows a progress bar. Storage scale is an implementation choice, not a physical-units or gas-composition simulation.

Use existing membership and local state rather than rescan geometry for every recipe. No Atmosphere means actual absence of atmosphere, not sealing or merely lack of breathable oxygen.

- Without an operating oxygenator, a room surrounded by vacuum slowly loses pressure. It does not become Vacuum immediately or retain atmosphere indefinitely. Loss rate remains tuning.
- A room on an atmospheric world does not become Vacuum merely because oxygenation stops. Sealing does not create Vacuum.
- Filling may be immediate but still requires ordinary oxygenator resources and power.
- Opening an airlock between sealed rooms or removing their shared partition immediately equalizes pressure, conserving existing atmosphere with volume-weighted redistribution.
- An actual opening to exterior vacuum immediately empties rooms connected through that airflow route.
- Infrastructure connectivity through walls is not airflow connectivity.

Only passive loss is gradual. There is no timed equalization or breach simulation. Missing room data is not evidence of a leak. [[Define Airlock Space Classification]] retains unresolved-side questions. Geometry optimization remains deferred.

Deliberate evacuation and vacuum-on-demand are out of current Alpha scope. Do not add a pump, evacuation mode or Overworld artificial-vacuum workaround for this integration.

## Combustion Generation in Space

Combustion generation is prohibited in the current space-factory scope, including oxygenated Station rooms. Exhaust and occupant safety motivate the restriction. Oxygenation, ventilation, exhaust treatment or direct oxygen inputs do not provide an exception.

Standard GT non-combustion machinery remains the baseline. Steam and nuclear generation are not combustion merely because they produce EU. Space Grade Solar Panels are recipe components, not generators.

Exact GT family coverage and an early power route need verification. This is a separate generation constraint, not an expansion of recipe-environment implementation or a complete planetary power policy.

## Integration Scope and Absent-Galaxia Development

The immediate implementation scope is Galaxia-only. Do not edit GT5 production sources or initiate upstream work. Prefer local authoring helpers and narrowly scoped Galaxia-hosted instrumentation without copying the whole GT builder. Separate transferable logic from temporary integration that later GT adoption must replace. Local source ownership does not eliminate runtime integration risk.

Native GT recipe metadata, fluent authoring and environment-dependent Recipe Families are the eventual direction, not implemented APIs established by these notes. [[Design Lunar Crater Processing Recipe Chain]] owns family-level locks and generated-recipe coverage.

Integrated gameplay includes Galaxia. GT-only execution is a development convenience with two explicitly accepted rules:

- Hide and silently ignore ordinary additional environmental requirements when Galaxia is absent. Existing requirements such as cleanroom still apply.
- Omit Galaxia-dependent environmental family variants. A family with no remaining variants is neither registered nor shown in NEI. Do not pick an arbitrary outcome or retain a disabled family.

Unavailable room data while Galaxia is loaded is not covered by the absent-mod exception.

## Implementation Evidence and Provenance

The capability model was consolidated from owner decisions on 2026-09-12. Independent production conditions were selected on 2026-09-17. Environment tags, pressure and integration boundaries were refined on 2026-10-08 through 2026-10-11.

Dated source findings under `src/main/java/com/gtnewhorizons/galaxia/`:

- On 2026-09-12, `CelestialBodyProperties` still held direct Station/Outpost flags used by `AssetCreateRequestPacket`, lacked the accepted solar modifier and duplicated Mars temperature with dimension effects. `AsteroidCelestialMaterializer` already marked asteroids Station-ineligible and Outpost-eligible.
- At `a9128e9ef21ff05254648190b4f79f94bdc9669d` on 2026-10-08, `GalaxiaAPI.getStationAround` traversed assets/controllers, `TileStationBase.isInside` used stored validation membership, and `TileStation` exposed oxygenation and level. `HazardPressure` treated sealing as pressure-safe rather than exposing actual pressure. These were inputs, not a completed environment query.

[[Recipe Environment Implementation Handoff]] records separate implementation coordination. Neither that handoff nor this resolved ticket certifies completed APIs, generator enforcement or current placement behavior.
