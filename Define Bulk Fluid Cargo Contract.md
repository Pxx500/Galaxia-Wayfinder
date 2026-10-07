---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Bulk Fluid Cargo Contract

## Question

Does Alpha provide direct bulk-fluid cargo for Rockets and Spaceships, or require fluids to travel packaged as item cargo?

## Established Input

[[Require Explicit Interplanetary Logistics]] includes fluids, while [[Define Space Transport Dispatch Model]] currently describes item-based cargo instructions. Fluid-storage modules in historical sources are not independently accepted design.

## Resolution

On 2026-09-17 the owner accepted fluid freight separately from item cargo. Rockets and Spaceships use the ordinary visit, loading and unloading model for bulk fluids, distinct from propulsion supplies. This does not grant Hammer bulk-fluid capability.

Rocket fluid freight uses a general fluid-capacity module. Reuse an existing suitable module if present, otherwise add that capability. Do not divide freight modules into gas tanks and liquid tanks. Both use the same fluid cargo system. This does not deny that a fluid may have gaseous properties, nor specify how many fluid types a module stores simultaneously.

The owner's intended Rocket cargo policy rejects container items rather than using item cargo to bypass dedicated storage. Ordinary non-container items remain cargo, including manufactured items. If a broad container restriction proves too limiting, evaluate a blacklist and then an explicit whitelist. The exact item coverage and policy mechanism are deferred until representative cargo items can be assessed. These are possible later refinements, not three simultaneous modes to implement now.

## Provenance

Surfaced during the owner-requested whole-vault reconciliation on 2026-09-17.

## Current Implementation Boundary

Bounded source inspection on 2026-09-17 at Galaxia `b1e42710a1d78b10ca35fde0c44a3cfdc293974b` found no general Rocket fluid-freight capacity. Under `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/rocket/`, `blueprint/RocketPartRegistry.java:95` registers Basic Storage as `modules/FunctionalPartDef.java:3`, whose fields do not include cargo capacity. `modules/FuelTankPartDef.java:3` instead defines scalar propulsion fuel capacity, consumed by `analysis/RocketStage.java:28`. This is not a general freight tank.

The accepted fluid-cargo capability therefore remains implementation work. No code was changed or runtime behavior tested in this planning check. The unrelated local AirlockGuiGameTests modification was preserved.
