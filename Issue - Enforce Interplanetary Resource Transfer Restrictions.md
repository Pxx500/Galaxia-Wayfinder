---
type: implementation-issue
status: planned
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Issue - Enforce Interplanetary Resource Transfer Restrictions

## Required Outcome

Enforce [[Require Explicit Interplanetary Logistics]] for the supported modpack. Shared storage and remote networks must not move items or fluids between celestial destinations in place of Galaxia logistics.

The policy also prohibits wireless EU transfer between planets. Include the supported wireless-energy paths in enforcement and verification, while preserving local power distribution.

Ender Chests, EnderStorage item and fluid channels, AE2 Quantum Ring connections and equivalent supported remote-access paths are relevant surfaces. Ordinary same-destination AE2 storage, crafting and automation remain available. Both biological players and androids obey the same material-transfer boundary.

## Completion Boundary

[[Define Late Interplanetary Network Access]] owns the newly surfaced late-access and surface-to-orbit boundary questions. Check that decision before finalizing integration coverage. The existing fixed-bandwidth Quantum Ring implementation is not proof of compliance with the physical-logistics policy.

Identify and verify the actual resource paths, including automatic transfers and portable access to shared inventories. Blocking only an android GUI does not meet the requirement. Preserve accepted Galaxia transport roles and avoid disabling all local AE2 use.

This is cross-system integration work, not an android-only inventory patch. Keep enforcement with the appropriate resource or network owner rather than replicating mod storage in body state. The final supported integrations and technical changes must be derived from the code during execution.

The android delivery's scoped denial of ordinary Ender Chest access does not complete this issue. Later implementation feedback explicitly leaves global EnderStorage and other transfer integrations to separate work. Per-destination EnderStorage channels are an owner preference to evaluate against actual channel behavior, not a verified integration design.

## Verification Boundary

Demonstrate blocked cross-destination item, fluid and wireless-EU transfers through the supported paths, allowed local networks, and normal Rocket cargo supply and receipt. Record the actual dependency or modpack versions tested. No enforcement is certified by this planning note.
