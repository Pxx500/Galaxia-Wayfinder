---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
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

# Module Settings Editing Contract


## Settings Model

Each settings-capable module has one explicit immutable settings value and one effective owner, private or shared. Membership follows stable module identity, not location. Physical build properties and runtime progress are not settings.

Editors use a local document draft and explicitly Save the complete value. Saving does not predict authoritative client state. Switching modules discards the draft under [[Unify Module Configuration Window Lifecycle]].

Validate untrusted packet and persistence boundaries rather than duplicating recovery throughout internal code. Reject and log malformed submissions without authoritative changes. Corrupt pre-release persisted settings may reset the complete value to defaults. No field-level recovery or migration is required.

## Copying and Shared Groups

- Creating a group copies effective settings into it and joins the source. Joining a compatible group shares future changes. Leaving keeps the current value as a private copy.
- Copying creates an independent private value at each target and removes its group membership. It never joins the source's group.
- Removing a module removes membership. Empty groups disappear.
- Shared recipe configuration never shares execution progress.
- Accepted complete recipe replacements and recipe-group joins or departures reset affected recipe schedules.
- A changed recipe copy resets the target schedule. An identical copy to an already-private target preserves it. Copying to a shared target makes it private and resets its schedule even if values match. Source progress is never copied.
- Concurrent valid saves apply in server order. The last accepted complete value wins.
- Removed targets are rejected, not redirected to replacements at the same position. Invalid operations have no partial effects, and batch copy validates every target before applying any.

## Module Classification

| Module or value | Copyable and shareable settings | Physical or runtime state |
| --- | --- | --- |
| Miner | Selected focus ore and ore blacklist in one value | Paid Focus Tier is physical. Alignment stays local |
| Hammer | Shooting mode, numeric threshold and route priority in one value | Tier and variant are physical. Stored energy and cooldowns are runtime |
| Recipe execution | Recipe configuration | Execution progress remains local |

Hammer modes allow unrestricted firing or a delta-v or flight-time limit. Route priority chooses delta-v or flight time.

Facility reserve, package-size and import/export policies are asset-level configuration, not extra Hammer fields. Stock, actual dispatch destinations and in-flight cargo are not copied settings. Whole-facility logistics copying or groups are not selected.

Debug Data Generator job parameters are configuration and job progress and consumed totals are runtime state. Copy/group tooling for this debug surface is not required. Its current debug-only status is not a permanent product restriction.

## Implementation Boundary

Inspection on 2026-09-12 and master `b1e42710` on 2026-09-16 found:

- Recipe Save and complete module-targeted replacement existed. `AutomatedFacility` and `FacilityModuleSettings` implemented copy ownership and schedule-reset behavior, not copying source progress or the separate powered cooldown.
- Miner blacklist was copied and shared through `MinerSettings`. `ModuleMiner.copySettings` copied focus ore separately, but focus ore was not shared. Changing it reset local alignment. Blacklist editing still sent immediate changes.
- `HammerConfigModalWidget` exposed the accepted fields, but Hammer had no settings-group support.
- `HammerDispatchPlanner` selected destination, cargo and quantity from `LogisticsResourceConfig`, not per-Hammer settings.
- Debug Data Generator had no settings groups.

Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. These findings establish gaps at inspection time, not current verification. Unified Miner and Hammer settings were accepted on 2026-09-16. Shared editing rules came from the August decisions, with identical-copy semantics confirmed on 2026-09-12.

## Related Topics

- [[Unify Module Configuration Window Lifecycle]]
- [[Area - Automation and Infrastructure]]

## Gameplay Flow

The player edits a module's settings in a local draft and saves the complete value. Switching modules discards an unsaved draft. A player can copy settings as independent values or join compatible modules to a shared group, while physical properties and execution progress remain local.
