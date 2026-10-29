---
type: wayfinder-ticket
ticket_type: research
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Travel and Logistics
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/research
---

# Research Current Gantry System

## System and Ownership

Source inspection on 2026-09-12 established the following integration boundaries. Recheck the current code before implementation.

- The implemented physical system consists of the Silo, Module Assembler, Gantry segments, and Gantry Terminals. `GantryAPI` coordinates routing but does not own persistent lifecycle state.
- The Silo owns the Rocket build order, delivered parts, assembled blueprint, and assembly status until it creates the `EntityRocket`. It is the closest existing owner of physical Rocket turnaround.
- The Module Assembler is currently a production service with a queued but placeholder stock model. It does not own the assembled Rocket.
- Gantry transports `RocketPartInstance` values between connected endpoints. Returning modules to the Assembler collapses them back into a count by module definition rather than preserving a concrete module instance.
- `RocketPartInstance` currently contains definition, placement, orientation, and serialization data, but no durability, wear, serial identity, or repair state.
- No maintenance machine currently exists.
- Active transit is not durable across unload, and some rejection or return paths clear source state without confirmed delivery. Safe transport of worn modules needs durable state and confirmed handoff.
- Automatic maintenance should extend this lifecycle: the Silo coordinates turnaround, Gantry transports modules, and a physical machine performs the work.

## Follow-Up

- [[Decide Gantry Maintenance Machine Ownership]] selects the repair machine.
- [[Define Automated Rocket Turnaround and Module Wear]] owns the gameplay lifecycle.
