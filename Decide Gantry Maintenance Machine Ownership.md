---
type: wayfinder-ticket
ticket_type: grilling
status: blocked
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
  - wayfinder/grilling
---

# Decide Gantry Maintenance Machine Ownership

## Question

Should automatic Rocket module repair deepen the existing Module Assembler, use a specialized subtype, or belong to a separate Gantry-connected maintenance machine?

## Requires

Agreement with the developers responsible for the existing Gantry, Silo, and Module Assembler systems.

This is an external design dependency. The current code audit does not supply that agreement.

## Established Constraints

- The Silo is the closest existing owner of physical Rocket turnaround and holds the assembled Rocket before launch.
- The Module Assembler currently produces and receives module definitions through a placeholder stock model.
- Gantry owns physical transport rather than Rocket or module lifecycle state.
- The chosen machine must consume supplied materials and energy, restore concrete module durability, and return the module through Gantry without creating a parallel transport path.
- `Perform maintenance` remains a dummy Vehicle Schedule declaration and does not depend on which physical machine performs repair.
- Concrete module durability, durable Gantry transit, and confirmed handoff are prerequisites for safely transporting worn module instances.

## Current Readiness Evidence

Read-only inspection on 2026-09-12 found definition and placement data but no per-instance wear in `registry/rocketmodules/rocket/blueprint/RocketPartInstance.java:7`. `registry/rocketmodules/tileentities/TileEntityModuleAssembler.java:119` still handles definition-based stock and assembly timing. `registry/rocketmodules/tileentities/gantry/GantryAPI.java:80` supports returning transport but does not return a delivery acknowledgement. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

Neither an existing assembler nor a returning Gantry direction establishes a finished repair owner. Developer reconciliation remains genuinely necessary.

## Options to Discuss

- Extend the existing Module Assembler with repair behavior.
- Add a specialized Module Assembler subtype.
- Add a separate Gantry-connected maintenance machine.

## Related Topics

- [[Research Current Gantry System]]
- [[Define Automated Rocket Turnaround and Module Wear]]
