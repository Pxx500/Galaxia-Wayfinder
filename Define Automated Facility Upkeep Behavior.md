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

Define Player Presence and Automation Tradeoffs delegates the accepted work-based upkeep and local starvation contract to this decision. These rules are common to Automated Facilities, not an asteroid-only maintenance system.

## Resolution

Missing upkeep resources temporarily stop only the affected module and produce its warning. Other modules are unaffected except through real operating dependencies. Resource upkeep is charged for actual work, not mere existence.

## Accepted Requirements

- A module without its required upkeep resources temporarily stops. Supply starvation does not itself destroy the module.
- The affected module exposes a warning through the normal operational warning system. There is no facility-wide shutdown solely because one module lacks its own upkeep resources.
- An idle module does not consume resource upkeep for elapsed time alone. This includes a Miner that cannot produce because output storage is full.
- A module supplying a continuous effect is doing work while that effect is provided. Work-based upkeep is not limited to discrete item recipes.
- Exact resource inputs, amounts, accounting cadence, and balance remain module-specific implementation and tuning work. This decision does not prescribe per-tick accounting.

## Implementation Evidence

Source inspection on 2026-09-12 found per-module shortage blocking, but upkeep accounting still counted enabled modules rather than actual work. The inspected owners were `AutomatedFacility` and `UpkeepLedger`. Recheck their current behavior when implementing work-based upkeep, including idle Miners blocked by full output.
