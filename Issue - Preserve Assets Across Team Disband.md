---
type: implementation-issue
status: planned
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
source_decision: "[[Audit Galaxia Concept Map]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Issue - Preserve Assets Across Team Disband

## Goal

Prevent Galaxia assets from remaining attached to a removed GTNH team identity.

## Accepted Behavior

- Normal owner-initiated disband transfers all Galaxia assets to the initiating owner's replacement singleton team.
- Administrator-forced disband requires either an explicit successor owner or explicit authorization to delete the assets.
- Assets are never implicitly deleted or duplicated among former members.
- Singleton teams remain protected by GTNHLib's existing no-disband behavior.
- GTNHLib must expose enough disband context for Galaxia to identify the removed team, initiating owner, and replacement team.

## Verified Current Constraint

- GTNHLib creates replacement singleton teams for members during disband but emits neither `TeamMergeEvent` nor a dedicated disband event.
- Without an additional hook or explicit integration change, Galaxia assets remain assigned to the removed team UUID.

## Related Topics

- Audit Galaxia Concept Map
- Area - Automation and Infrastructure
- Galaxia Alpha Wayfinder

## Gameplay Flow

When an owner disbands a team normally, its Galaxia assets transfer to that owner's replacement singleton team. An administrator-forced disband instead needs a successor owner or explicit authorization to delete the assets.
