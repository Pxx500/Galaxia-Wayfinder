---
type: wayfinder-ticket
ticket_type: grilling
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
  - wayfinder/grilling
---

# Decide Gantry Maintenance Machine Ownership

## Module Repair

Use the existing Module Assembler for material-consuming repair of concrete Rocket modules. The Landing Pad dispatches worn modules through Gantry to available, supplied Assemblers. Healthy modules may bypass repair and travel to the Silo. Several Assemblers may service modules concurrently and return them to the same Silo for reassembly.

This resolves the machine owner, not the implementation or numerical repair costs.

## Established Constraints

- The Silo is the closest existing owner of physical Rocket turnaround and holds the assembled Rocket before launch.
- The Module Assembler currently produces and receives module definitions through a placeholder stock model.
- Gantry owns physical transport rather than Rocket or module lifecycle state.
- The chosen machine must consume supplied materials and energy, restore concrete module durability, and return the module through Gantry without creating a parallel transport path.
- `Perform maintenance` remains a dummy Vehicle Schedule declaration and does not depend on which physical machine performs repair.
- Concrete module durability, durable Gantry transit, and confirmed handoff are prerequisites for safely transporting worn module instances.

## Current Readiness Evidence

Read-only inspection on 2026-09-12 found definition and placement data but no per-instance wear in `registry/rocketmodules/rocket/blueprint/RocketPartInstance.java:7`. `registry/rocketmodules/tileentities/TileEntityModuleAssembler.java:119` still handles definition-based stock and assembly timing. `registry/rocketmodules/tileentities/gantry/GantryAPI.java:80` supports returning transport but does not return a delivery acknowledgement. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

This historical inspection predates the selected workflow and does not describe the current Rocket branch. It explains why concrete module state and confirmed handoff must be verified during implementation.

## Provenance

Source: Rocket implementation feedback, 2026-10-18. Demonstration speed and laboratory layout are not gameplay requirements.

## Related Topics

- [[Research Current Gantry System]]
- [[Define Automated Rocket Turnaround and Module Wear]]

## Gameplay Flow

After a Rocket lands, the Landing Pad sends worn modules through Gantry to supplied Module Assemblers for repair. Healthy modules can bypass repair. Multiple Assemblers can work concurrently and return modules to the same Silo for reassembly.
