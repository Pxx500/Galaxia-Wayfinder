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

# Bulk Fluid Cargo Contract

## Fluid Freight

[[Require Explicit Interplanetary Logistics]] includes fluids, while [[Define Space Transport Dispatch Model]] currently describes item-based cargo instructions. Fluid-storage modules in historical sources are not independently accepted design.

Rockets and Spaceships support fluid freight separately from item cargo. Bulk fluids use the ordinary visit, loading and unloading model and are distinct from propulsion supplies. This does not grant Hammer bulk-fluid capability.

Rocket fluid freight uses a general fluid-capacity module. Reuse an existing suitable module if present, otherwise add that capability. Do not divide freight modules into gas tanks and liquid tanks. Both use the same fluid cargo system. This does not deny that a fluid may have gaseous properties, nor specify how many fluid types a module stores simultaneously.

The intended Rocket cargo policy rejects container items so they cannot bypass dedicated storage. Ordinary non-container items remain cargo, including manufactured items. If a broad container restriction proves too limiting, evaluate a blacklist and then an explicit whitelist. The exact item coverage and policy mechanism are deferred until representative cargo items can be assessed. These are possible later refinements, not three simultaneous modes to implement now.

## Current Implementation Boundary

Source inspection at Galaxia `b1e42710` found propulsion capacity but no general Rocket fluid-freight capacity. The propulsion tank is not a freight tank. Recheck the current module model before implementing freight storage.

## Gameplay Flow

A player loads fluids as freight on a Rocket or Spaceship visit and unloads them at the destination. Rocket freight uses general fluid capacity for gases and liquids, separate from propulsion supplies. The intended Rocket item policy accepts ordinary items but rejects containers that could bypass dedicated storage.
