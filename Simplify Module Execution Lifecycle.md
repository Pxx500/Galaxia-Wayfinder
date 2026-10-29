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

# Simplify Module Execution Lifecycle

## Accepted Requirements

- Resource-affecting module changes are server-authoritative and use stable module identity.
- Validate the complete change before effects. Rejected changes preserve inventory, layout, and operation state. Multi-target operations are all-or-nothing.
- Miner Focus Tier is a paid physical property, not ordinary copyable settings.
- Upkeep follows the resolved work-based rules in [[Define Automated Facility Upkeep Behavior]].

## Current Behavior

Source inspection on 2026-09-12 under `src/main/java/com/gtnewhorizons/galaxia/`:

- An operation waiting for enough materials does not by itself stop the module's normal work.
- Once building begins, ordinary runtime is blocked. Refunding also blocks it.
- Completion or cancellation releases the operation gate.
- Normal runtime has powered-tick and cooldown-cycle cadences.

Evidence: `registry/outpost/AutomatedFacility.java:1445`, `:1462`, and `:1487`, plus `registry/outpost/module/ModuleInstance.java:52` and `:58`.

## Operation Lifecycle

Waiting for upgrade materials does not itself stop normal module work. Active building or refunding blocks normal work until completion or cancellation and the associated settlement release the operation gate. This behavior was accepted on 2026-09-12.

Feature-cache sharing, callback removal, internal status representation, and code naming are implementation-time choices. They no longer appear as gameplay blockers in this ticket.

## Gameplay Flow

The player can request a module upgrade while it continues normal work as materials accumulate. Once building begins, or while a refund is active, normal work stops until the operation completes or is cancelled and settled.
