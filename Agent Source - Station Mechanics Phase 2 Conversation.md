---
type: source
status: unreviewed
tags:
  - wayfinder/source
---

# Agent Source - Station Mechanics Phase 2 Conversation

Source status: unreviewed planning capture
Captured: 2026-07-31
Scope: Station Mechanics Phase 2, automated stations, and thermal-management planning
Review disposition: source-only capture. This note is intentionally not linked to Wayfinder maps, areas, tickets, or implementation modules until reviewed by the project owner.

## Scope

This 2026-07-31 conversation captures a thermal-management direction and possible Station Mechanics Phase 2 work. It is review material, not an accepted specification or implementation plan. Older documents and the code observations below may no longer describe the current project.

Historical project references: `AI/StationMechanicsArchitecture.md`, `AI/Current/ModuleRegistryArchitecture.md` and `docs/station-module-operations-design.md`. These identify the architecture context at capture time, not current file locations or instructions.

## Code Shape Observed in 2026

The captured station system had the following implementation surface:

- `AutomatedFacility` is the facility runtime owner for automated stations and outposts.
- `StationLayout` owns the station grid and placed module footprints.
- `ModuleInstance` is the universal per-placement module state.
- `ModuleComponent` / `IModuleComponent` own per-kind behavior/config state.
- `FacilityModuleKind` is the stable module identity enum.
- `FacilityModuleRegistry` already owns part of the registry-driven module definition model.
- `ModuleOperationPlan`, `ModuleOperationState`, `ModuleOperationPhase`, `IModuleOperation`, `ModuleTierOperation`, `HammerModuleOperation`, and `MinerFocusOperation` already exist as the seed of physical module operations.
- Persistence and sync paths already know about module operations in places such as `FacilityPersistenceManager`, `AssetSyncPacket`, and `AssetModuleUpdatePacket`.

Important design pressure: the registry is partially implemented but not yet the full source of truth for all UI, persistence, sync, and build surfaces.

## Station Mechanics Direction

The conversation returned to Station Mechanics Phase 2, previously treated as deferred. The owner explicitly reframed it as active: deferred until now.

The first recommended vertical slice was heat / thermal management. Reasoning:

- Heat naturally extends existing facility modules, upkeep, area effects, module registry data, and station-grid concepts.
- It does not require immediately building full internal logistics, pathfinding, expeditions, docking, or a global station job system.
- It gives orbital stations a strong gameplay identity: vacuum makes heat dissipation a real design constraint.

## Heat Scope Decision

The owner selected the option where heat is not universal. Heat should apply where the environment makes it interesting:

- orbital stations, because they operate in vacuum;
- outposts on vacuum or airless bodies;
- outposts on hot planets or bodies;
- ordinary temperate planets should not require full heat management by default.

The owner then clarified the implication: there should be a per-planet or per-celestial-body flag/profile.

## Thermal Environment Model

The working model is a small environment profile rather than a single boolean. A possible first enum shape:

```java
CoolingEnvironment {
    TEMPERATE,
    VACUUM,
    HOT,
    CRYOGENIC
}
```

First implementation should probably handle only:

- `TEMPERATE`: no active heat pressure for ordinary outposts;
- `VACUUM`: active heat pressure and weak passive cooling;
- `HOT`: active heat pressure even on planetary outposts.

`CRYOGENIC` is attractive as a future modifier but should not drive the first implementation unless the owner explicitly chooses it.

## Outpost Cooling Idea

For vacuum or hot outposts, the owner floated underground cooling loops: infrastructure that dumps heat into the ground rather than radiating into space.

Current interpretation:

- Orbital stations should rely primarily on radiators or thermal-management modules.
- Airless outposts can have an alternative cooling route: underground cooling loops, regolith heat sinks, or body-specific thermal sink features.
- Hot planets may make cooling harder, or may require stronger infrastructure even if an atmosphere exists.

This is an idea, not yet an accepted mechanic.

## First Slice Candidate

A conservative first implementation slice would be:

1. Add a thermal environment profile to authored celestial body data.
2. Let `AutomatedFacility` ask its body or station context whether heat mechanics are active.
3. Aggregate simple facility-level thermal values: heat generated, heat dissipated, thermal pressure.
4. Give a small set of existing modules heat generation or cooling values through existing owners, preferably module definitions or tier data rather than feature-local registries.
5. Expose enough state for debugging or player feedback, but avoid designing a full final UI before the simulation contract is stable.
6. Apply a simple, reversible gameplay effect when thermal pressure exceeds safe capacity: likely throttling or blocking selected modules rather than destructive failures.

The first slice should avoid full tile-by-tile heat simulation unless the owner chooses a more physical design. Facility-level or cluster-level aggregation is probably enough to learn whether the mechanic is fun.

## Proposed Ownership

The proposed approach puts celestial environment data on the celestial model and module thermal behavior on existing module definitions, tiers or components, rather than separate feature-local registries. This is a design direction, not an implementation decision.

## Open Questions To Review Later

- What exact name should the thermal environment concept use: `CoolingEnvironment`, `ThermalEnvironment`, or something more domain-specific?
- Is the profile attached to every celestial object, or derived from atmosphere, temperature, and orbital context?
- Should orbital stations always count as `VACUUM` regardless of parent body?
- Should hot planets and vacuum planets be separate profiles or composable traits?
- Should the first model be facility-level aggregation, cluster-level aggregation, or station-grid local heat?
- Which modules generate heat first: recipe machines, miners, hammers, shipyard, batteries, power generation, or only high-power modules?
- Which modules dissipate heat first: radiator, maintenance bay modifier, underground cooling loop, connector network, or existing area effects?
- What happens when overheated: pause module, throttle throughput, increase upkeep, damage operation progress, or create alerts only?
- How should thermal state be shown in the current station GUI without making the UI too noisy?
- Should heat be a blocker for Alpha, or an optional Phase 2 system that can be abandoned if it adds more micromanagement than gameplay?

## Non-Decisions

The conversation did not decide to implement:

- full internal station logistics;
- docking or orbital shipyard behavior;
- expeditions;
- satellite-station integration;
- tile-by-tile thermal conduction;
- destructive overheating failures;
- a final player-facing heat UI;
- migrations or save compatibility shims.

## Scope Still Open

Whether to continue the broader Phase 2 remains open. The recorded heat direction is narrower: environmental behavior, mainly driven by vacuum and hot bodies, with a per-body thermal profile.
