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

## Purpose

This file preserves the current agent conversation and decisions about expanding Galaxia station mechanics. It is not an accepted specification, implementation plan, or ticket map. Use it later as a source note when deciding whether to continue, reshape, or abandon this direction.

## Active Branch And Workspace Context

- A dedicated worktree was created for this direction at `C:/Users/Pxx500/Documents/GitHub/Galaxia/.worktrees/expand-automatedStations`.
- The branch name is `expand-automatedStations`.
- The original requested branch name was `expand automatedStations`, but Git does not allow spaces in branch names, so the branch was created with a hyphen.
- The main checkout later showed `master`; future implementation work should happen in the dedicated worktree unless the owner decides otherwise.

## Verification And Workflow Decisions

- Gradle commands must always run through context-mode wrappers with explicit timeouts; never run Gradle through direct shell/CMD because it can hang.
- At the end of coding tasks, run `./gradlew agentVerify` through context-mode.
- A global Gradle init script was created at `C:/Users/Pxx500/.gradle/init.d/agent-verify.gradle` so new repositories and worktrees get an `agentVerify` task even when the repo-local helper is missing.
- That global task mirrors the repo helper intent: run `spotlessApply`, `test`, and `build` where those tasks exist.
- `mustRunAfter` does not cause `spotlessApply` to run on every build. It only orders tasks when both are already in the Gradle task graph.
- Because the owner does not have direct visibility into the worktree, after every gameplay-code change the agent must run `runClient25` so the owner can verify the game manually.

## Existing Project Context Reviewed

The agent reviewed the repo instructions and station-related documents before the long pause. Important source documents included:

- `AI/StationMechanicsArchitecture.md`
- `AI/Current/StationMechanicsImplementationPlan.md`
- `AI/Current/StationMechanicsIdea.md`
- `AI/Current/stationmechanicsphase2.md`
- `AI/Current/StationMechanicsFollowups.md`
- `AI/Current/ModuleRegistryArchitecture.md`
- `AI/Current/ModuleRegistryRefactorImplementationPlan.md`
- `docs/station-module-operations-design.md`
- `docs/station-module-operations-next-pr-handoff.md`
- `docs/generic-module-upgrade-system-proposal.md`
- `AI/Glossary.md`
- `AI/LocalizationRules.md`
- `AI/Current/Rules.md`

Important interpretation: older station mechanics documents contain historical or deferred design material. Current code is allowed to supersede old plan text when they disagree. Do not force code backward to match stale class names, packet tables, or phase notes.

## Current Code Shape Observed

The station system already has a substantial implementation surface:

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

## Important Architecture Constraints

- Deepen existing domain owners before creating feature-local stores or callback SPIs.
- Put celestial environment data on the celestial/domain model, not in a station-only side table unless proven necessary.
- Put module thermal behavior on module definitions, tier data, or module components, not in scattered switch statements.
- Do not add migration or compatibility shims by default. Galaxia is pre-alpha/pre-beta and developer saves are scratch data unless the owner declares a supported public contract.
- Use `CelestialObjectKey` for runtime references and `CelestialObjectId` for developer-authored fixed registrations.
- If any visible UI text or translation key is added, consult `AI/LocalizationRules.md` first.
- If gameplay behavior, persistence, networking, ownership, or cross-module contracts change, default back to TDD through a stable public seam.

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

## Possible Decision Path

1. Decide whether the destination is a spec only, a Wayfinder map, or a first implementation slice.
2. If continuing, choose the thermal environment vocabulary and ownership location.
3. Choose the first simulation resolution: facility-level, cluster-level, or grid-local.
4. Choose initial heat producers and cooling modules.
5. Choose the overheat consequence.
6. Only then produce implementation tickets or a detailed implementation plan.

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

## Owner Sentiment

The owner is considering whether to continue this direction or abandon it. This note should be treated as review material, not momentum pressure. The valuable decision already made is narrower than the whole Phase 2: heat should be environmental, mainly vacuum and hot-body driven, with a per-body thermal profile.