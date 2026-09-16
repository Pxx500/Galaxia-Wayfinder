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

# Unify Module Configuration Window Lifecycle

## Question

What shared draft, Save, Cancel, and target-switch behavior should module settings windows provide?

## Resolution

Settings editing uses a local draft and an explicit Save. Switching to another module closes the previous configuration and opens the selected module's editor, discarding unsaved changes. No per-module draft retention or additional discard-confirmation flow is required. Typed settings editors retain their own validation and values. Physical operations remain distinct from editing settings.

These are existing accepted rules, consolidated on 2026-09-12. The internal editor interface is implementation work, not another player-facing decision. Remaining copyable-value classification belongs to [[Define Module Settings Editing Contract]].

## Current Implementation Boundary

Source inspection on 2026-09-12 under `src/main/java/com/gtnewhorizons/galaxia/`:

- `client/gui/station/RecipeConfigModalWidget.java:613` submits a complete recipe draft and closes. `ModuleConfigModalController.java:351` closes and rebuilds that editor when retargeting.
- `MinerBlacklistConfigModalWidget.java:199` still sends a blacklist change immediately.
- `ModuleConfigModalController.java:341` and `:361` retarget Miner and Debug widgets in place.

The Recipe Book path provides partial alignment, not proof that every editor meets the contract. The Miner immediate-edit path and differing retarget behavior remain implementation work. No current internal class layout is prescribed by this decision.
