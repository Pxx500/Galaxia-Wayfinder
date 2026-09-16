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

# Define Automated Facility Upkeep Behavior

## Question

How do recurring module upkeep requirements affect an Automated Facility when supplies are missing, and when does an idle module incur upkeep?

## Established Input

Define Player Presence and Automation Tradeoffs preserves recurring authored module resources and shutdown on missing supply as a candidate automation cost. Detailed starvation, consumption, and recovery behavior is not yet accepted there. These rules are common to Automated Facilities, not an asteroid-only maintenance system.

## Resolution

Missing upkeep resources temporarily stop only the affected module and produce its warning. Other modules are unaffected except through real operating dependencies. Resource upkeep is charged for actual work, not mere existence.

## Accepted Requirements

- A module without its required upkeep resources temporarily stops. Supply starvation does not itself destroy the module.
- The affected module exposes a warning through the normal operational warning system. There is no facility-wide shutdown solely because one module lacks its own upkeep resources.
- An idle module does not consume resource upkeep for elapsed time alone. This includes a Miner that cannot produce because output storage is full.
- A module supplying a continuous effect is doing work while that effect is provided. Work-based upkeep is not limited to discrete item recipes.
- Exact resource inputs, amounts, accounting cadence, and balance remain module-specific implementation and tuning work. This decision does not prescribe per-tick accounting.

## Implementation Evidence and Provenance

The owner accepted both rules in the Wayfinder conversation on 2026-09-10.

Read-only source inspection on 2026-09-12 confirms per-module shortage blocking and recovery in `registry/outpost/AutomatedFacility.java:1032`, `:1068`, and `:1075`, under `src/main/java/com/gtnewhorizons/galaxia/`.

Work-based accounting is not implemented by the inspected path. `AutomatedFacility.java:1445` settles upkeep every 1200 ticks, and `registry/outpost/upkeep/UpkeepLedger.java:42` counts enabled, structurally operational modules without checking actual work. A Miner unable to insert output still meets that predicate. This is an implementation gap against the resolved rule, not a reason to ask again whether idle modules should pay upkeep.
