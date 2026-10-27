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

Use Overworld surface daylight as the common solar-output reference of `1.0x` or 100%, with zero solar output at night. Daylight Solar Intensity is instantaneous available output. Average Solar Yield averages output over the local light/dark cycle using that same reference, not a second normalization that makes a full Overworld cycle equal to 100%. Keep daylight intensity, light/dark duration, atmosphere and authored modifier visible in the comparison. This single-reference clarification supersedes the earlier dual-reference presentation.

Surface generation follows actual illumination and atmospheric effects. Separate day/night durations expose storage needs even at equal average yield. Space avoids ordinary atmospheric loss.

Derive solar output from source distance, atmospheric transmission and illumination through the shared environmental model, not a hardcoded dimension-to-percentage table. Suitable orbital generation should be substantially more productive than Overworld daylight, in addition to avoiding nighttime downtime. The discussed 200% or 300% for Overworld orbit are illustrative calibration targets, not selected constants. Any retained authored Solar Resource Modifier is an explicit adjustment to the derived model, not its replacement.

The accepted Alpha orbital convention places the parent planet below the player and the Sun in a fixed horizontal direction. Orbital dimensions retain microgravity and continuous sunlight, without periodic planetary eclipses. Down identifies the planet-facing world direction, not a gravity force. This is a gameplay and rendering convention, not a claim of geostationary orbital mechanics. It does not equalize output across bodies or remove distance and authored modifiers.

[[Define Space Factory Power Supply]] develops directional solar walls and radiator exposure using the same fixed horizontal light direction as the rendered Sun. Local construction shading is distinct from the excluded planet-shadow orbital cycle, and its exact checks remain open.

## Recipe Environment Contract

Microgravity and No Atmosphere are independent requirements, not generic Station or orbit flags:

- SiGe crystal growth and specialty fluoride optical-fiber production require microgravity.
- Space-Grade Alloy alloying, melting, casting and material recovery require No Atmosphere, including generated recipes for those operations. Assembly of cast parts does not automatically inherit that requirement. The lunar recipe owner defines the melt-and-cast route. Luna qualifies despite surface gravity.
- Other processes may need either, both or neither. A suitable environment does not supply missing machinery or Automated Facility modules.

These are gameplay choices motivated by research, not claims that terrestrial manufacture is physically impossible. Thresholds remain tuning.

The current player-facing progression assumes the required microgravity is available in orbital dimensions. This is content availability, not permission to add an orbit whitelist to recipes. Earlier zero-gravity asteroid Outpost concepts do not by themselves establish an accessible physical production alternative. Validate belt and Outpost content against this assumption when implementing their production capabilities. If another accessible environment truly meets the conditions, the same recipe rule must accept it.

An environment restriction may naturally leave only one accessible choice. Do not invent alternatives to meet a quota, or choose a unique pressure or temperature value merely to encode a planet ID.

Galaxia owns tag definitions, classification and evaluation. Extensions register through Galaxia's API, not a competing GT catalog or open provider collection. Tags describe conditions, not team membership or Technology Knowledge.

Recipes may declare an optional requirement independent of `mSpecialValue`. All supplied tags must hold at execution. Recipes without it gain no restriction from this system. Voltage, heat, cleanroom and other requirements remain independent.

The accepted authoring target is a readable `requiresEnvironment(...)` fluent method with named typed constants and IDE completion. A closed enum is not required. GT authors should use neutral references without loading Galaxia classes or wiring evaluators. Exact types and wiring remain implementation choices.

For Alpha, observe the multiblock controller's position, not every block of its structure. If a required environment fails during a recipe, use the machine's native GT failure path and its ordinary consequences. Do not retain work in a custom environment-pause state or resume a canceled operation when conditions return. [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]] owns this shared rule.

## Room Pressure

A physical Room owns one bounded Room Pressure Level shared by all its controllers. Zero is Vacuum and full is full atmosphere. The controller shows a progress bar. Storage scale is an implementation choice, not a physical-units or gas-composition simulation.

Use existing membership and local state rather than rescan geometry for every recipe. No Atmosphere means actual absence of atmosphere, not sealing or merely lack of breathable oxygen.

- Without an operating oxygenator, a room surrounded by vacuum slowly loses pressure. It does not become Vacuum immediately or retain atmosphere indefinitely. Loss rate remains tuning.
- A room on an atmospheric world does not become Vacuum merely because oxygenation stops. Sealing does not create Vacuum.
- Filling may be immediate but still requires ordinary oxygenator resources and power.
- Opening an airlock between sealed rooms or removing their shared partition immediately equalizes pressure, conserving existing atmosphere with volume-weighted redistribution.
- An actual opening to exterior vacuum immediately empties rooms connected through that airflow route.
- Infrastructure connectivity through walls is not airflow connectivity.

Only passive loss is gradual. There is no timed equalization or breach simulation. Rooms require controllers under the accepted current room model. Removing a room's controller removes its modeled room and atmosphere data, even if the shell remains closed. Preserving a controllerless room is not required for environment integration. This does not turn arbitrary unavailable runtime data into a valid environment result. [[Define Airlock Space Classification]] retains other unresolved-side questions. Geometry optimization remains deferred.

Deliberate evacuation and vacuum-on-demand are out of current Alpha scope. Do not add a pump, evacuation mode or Overworld artificial-vacuum workaround for this integration.

## Combustion Generation in Space

Combustion generation is prohibited in the current space-factory scope, including oxygenated Station rooms. Exhaust and occupant safety motivate the restriction. Oxygenation, ventilation, exhaust treatment or direct oxygen inputs do not provide an exception.

Standard GT non-combustion machinery remains the baseline. Steam and nuclear generation are not combustion merely because they produce EU. Space Grade Solar Panels are recipe components, not generators.

Exact GT family coverage and an early power route need verification. This is a separate generation constraint, not an expansion of recipe-environment implementation or a complete planetary power policy.

## Integration Scope and Absent-Galaxia Development

The initial Galaxia-only prototype is no longer the exclusive implementation target. On 2026-10-23 the owner authorized native GT recipe-environment API work, with cleanroom as a native GT use case and unchanged cleanroom gameplay. Prioritize compatibility with MaterialLib-backed GT material unification for material-generated requirements. Galaxia retains its celestial and room-condition definitions. This scoped authorization belongs to the environment integration delivery, not permission for every content task to independently modify GT infrastructure. Existing prototype evidence does not certify the new API or material integration.

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
