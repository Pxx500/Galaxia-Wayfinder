---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Module Settings Editing Contract

## Question

Which module values are copyable settings rather than physical properties or runtime state?

## Established Input

- Recipe editing remains a document model. The user edits a local draft and explicitly saves it.
- A complete submitted settings value may be rejected and logged when malformed. Pre-release compatibility and partial recovery are not required.
- Validation must protect authority and unsafe boundaries without duplicating speculative recovery logic throughout the codebase.
- Each settings-capable module should have one explicit immutable settings definition rather than scattered field-level packet verbs.
- Settings remain private or shared. Membership follows stable module identity rather than its location.
- Physical build properties are not ordinary settings. In particular, Miner Focus Tier is a paid physical property of the module.
- Runtime progress and operation state are not settings.
- Settings editors use a document model with an explicit Save action rather than sending each field change live.
- Internal settings code may assume constructed values are valid. Validation remains concentrated at untrusted packet and persistence boundaries.
- A malformed client submission is rejected and logged without changing authoritative settings. Corrupt pre-release persisted settings may reset the complete settings value to the module default instead of adding field-level recovery or migration logic.

The following accepted behavior was retained from the completed August architecture decisions during the 2026-09-11 cleanup. The remaining settings-classification questions below are still open.

## Accepted Shared Settings and Recipe Editing Rules

- Every settings-capable module has one effective settings owner, either private or a shared group.
- Creating a group copies the module's effective settings into that group and joins the module to it. Joining an existing compatible group shares subsequent changes. Leaving a group retains its current settings as a private copy.
- Copying settings gives each target an independent private copy and removes the target from any shared group. Copying never silently joins the source's group.
- Removing a module removes its membership. An empty group is removed automatically.
- Shared recipe configuration does not share execution progress. Each executing module keeps its own progress, and copying settings never copies another module's runtime progress.
- Recipe editing uses a local draft and an explicit save of the complete recipe configuration. Saving does not predictively change authoritative client state.
- An accepted complete recipe replacement resets affected recipe schedule progress. Joining or leaving a recipe group resets the affected module's recipe progress.
- Copying changed recipe settings resets the target's own recipe schedule. An identical copy to an already-private target preserves its schedule. Copying to a shared target makes it private and resets its schedule, even if the effective values match. Source progress is never copied. The owner accepted this existing behavior on 2026-09-12.
- Changes are validated against current server state. Concurrent valid saves are applied in server order, with the last accepted complete value winning.
- A removed target is rejected rather than redirecting the change to a replacement at the same position. Invalid changes have no partial effects. A batch copy validates all targets before changing any.

## Current Implementation Evidence

Source inspection on 2026-09-12 under `src/main/java/com/gtnewhorizons/galaxia/`:

- `registry/outpost/AutomatedFacility.java:437` applies copied settings, and `finishModuleSettingsCommand` at line 456 resets recipe schedules on changed targets through `resetRecipeSchedules` at line 1236. The source's progress is not copied.
- `registry/outpost/FacilityModuleSettings.java:196` treats an identical private target as unchanged, preserving its schedule. Copying onto a shared target changes ownership to private and resets its recipe schedule even when the effective values match. This resets recipe schedule state, not the separate powered cooldown counter.
- Complete Recipe Book and Miner settings replacements already use the module-targeted path at `AutomatedFacility.java:387`. `FacilityModuleSettings.java:260` resolves its current private or shared owner. Choosing a new command name is not a required product question.
- Shared settings support currently covers Miner and recipe settings. `ModuleMiner.java:211` and `:221` copy focus ore through a component hook, while `MinerSettings.java:9` stores blacklist keys. Focus ore is not the paid Focus Tier.
- Recipe Save is implemented, but Miner blacklist still sends immediate field edits. Unify Module Configuration Window Lifecycle owns the accepted explicit-Save target and this implementation gap.

## Remaining Decisions

- Which current Hammer, Miner, Debug, and Logistics values are copyable settings versus physical properties or runtime state.
- Switching modules discards the local draft as decided in Unify Module Configuration Window Lifecycle. Save semantics and internal command naming are not additional open gameplay questions.

## Related Topics

- [[Unify Module Configuration Window Lifecycle]]
- [[Area - Automation and Infrastructure]]
