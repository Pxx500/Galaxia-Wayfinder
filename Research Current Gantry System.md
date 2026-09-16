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

## Question

What physical machines, ownership boundaries, and module flows currently form Galaxia's Gantry System, and where can automatic Rocket module maintenance integrate without creating a parallel module lifecycle?

## Known Context

- The Gantry System uses physical rail-like infrastructure to move Rocket modules between machines.
- Known examples include a Silo and a Module Assembler, though their exact current names and implementation state require verification.
- Automatic maintenance may deepen an existing machine or use a separate Gantry-connected machine.

## Resolution

- The implemented physical system consists of the Silo, Module Assembler, Gantry segments, and Gantry Terminals. `GantryAPI` coordinates routing but does not own persistent lifecycle state.
- The Silo owns the Rocket build order, delivered parts, assembled blueprint, and assembly status until it creates the `EntityRocket`. It is the closest existing owner of physical Rocket turnaround.
- The Module Assembler is currently a production service with a queued but placeholder stock model. It does not own the assembled Rocket.
- Gantry transports `RocketPartInstance` values between connected endpoints. Returning modules to the Assembler collapses them back into a count by module definition rather than preserving a concrete module instance.
- `RocketPartInstance` currently contains definition, placement, orientation, and serialization data, but no durability, wear, serial identity, or repair state.
- No maintenance machine currently exists.
- The Gantry transport prototype has persistence and acknowledgement gaps. Active transit state is not durable across unload, and some rejection or return paths clear source state without confirmed delivery.
- Automatic maintenance should extend the existing Silo and Gantry module lifecycle. The Silo is the natural turnaround coordinator, Gantry remains transport, and a physical production or maintenance machine performs the actual module work.
- Before Gantry can safely carry valuable worn module instances, its transport needs durable state and confirmed handoff semantics.

## Blocks

- [[Define Automated Rocket Turnaround and Module Wear]]
