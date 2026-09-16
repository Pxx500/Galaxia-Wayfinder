---
type: wayfinder-research
status: complete
source: "[[Discord Source - Galaxia Dev Notes]]"
parent: Review Galaxia Dev Notes
tags:
  - galaxia/alpha
  - wayfinder/research
---

# Galaxia Dev Notes Research

> Historical or reference record. Read dated outcomes and later corrections before using earlier proposals. This record is not an active instruction to execute its plan, and its code or verification claims have not been revalidated by the 2026-09-10 vault consolidation.

## Provenance and Review Rule

Source: [[Discord Source - Galaxia Dev Notes]]  
Original: https://docs.google.com/document/d/1kyRDNYa4DpgGRy6Sq5Y77DPSezG7nJh97so4hAIrfco/edit?tab=t.62cu26l6xf9d

The source is a historical collection of proposals by several developers, not an accepted specification. Its `Alpha Release Must-have List` records an earlier implementation checklist and does not define the current Wayfinder Alpha scope. Ore placement and ore-generation claims were excluded in favor of the maintained Ore Sheet.

## Classification Summary

| Source concept | Classification | Current interpretation or route |
|---|---|---|
| Galaxia uses modular Rockets assembled from cores and modules | Corroborated / routed | Modular vehicles remain accepted direction. Exact module contracts belong with Define Vehicle Capability and Route Requirements and the eventual Galaxia-specific Alpha capability floor. |
| Rocket Core controls shape, slots, and a hardcoded destination tier | Partly superseded | Shape and slot ownership remain plausible. A direct `core tier -> destination whitelist` is replaced by the accepted multi-variable vehicle and route capability model. |
| Enforced, passive, active, structural, and functional module categories | Genuine open question | Useful design vocabulary, but no current Wayfinder decision accepts this taxonomy or its slot rules. |
| Functional modules for thrust, onboard processing, fluid storage, and item storage | Genuine open question | Candidate vehicle capabilities. Their Alpha necessity and trade-offs remain undefined. Route to Define Alpha Transport Roles and Define Alpha Galaxia-Specific Capability Floor. |
| Fixed Tier 1 and Tier 2 Rocket slot layouts | Superseded / provenance only | Historical examples, not product contracts. They also use retired destination names. |
| Higher Rocket tiers unlocked with Research Notes or a research tree | Superseded as a global rule | Current Alpha defaults to material and capability gating. Research may support a concrete activity, but is not assumed as the universal Rocket progression system. |
| Module Assembler as the common construction owner for cores and modules | Genuine open question | Consistent with physical spacecraft construction, but its exact ownership and Alpha contract have not been accepted by Wayfinder. |
| Silo or Launch Pad links to the assembler, assembles, launches, lands, and starts a minigame | Genuine open question | The exact responsibilities and boundaries of construction, launch, landing, and flight planning remain unclassified. |
| Arcade flight game with Radiation, Fuel, Energy, Mass, and Speed | Genuine open question | No accepted Wayfinder decision commits to this minigame or these five state variables. Route to Define Flight Progression Balance Invariants and Define Vehicle Capability and Route Requirements. |
| Gantry doors, spline points, line-clearance validation, linked-list traversal, and inertial animation | Provenance only | Implementation and presentation proposal. Do not preserve it as deferred Wayfinder specification; derive implementation detail if Gantries enter an execution task. |
| Physical Stations as decentralized orbital logistics hubs | Corroborated / routed | Consistent with explicit interplanetary logistics and the requirement for at least one mandatory Physical Station. Exact capability remains open in Define First Physical Station Contract. |
| Physical Station protects players and machines from environmental hazards | Genuine open question | Candidate Station role and construction constraint. Route to Define First Physical Station Contract and Define Celestial Capability Rules. |
| Arbitrarily shaped Station rooms controlled as modules | Genuine open question | Neither the geometry model nor controller ownership is accepted. It is not required by the current definition of Physical Station. |
| Station rooms, docks, power room, hydroponics, centralized power plugs, and voltage-tier hatches | Genuine open question | Candidate Station capabilities. Their Alpha subset belongs in Define First Physical Station Contract and Define Alpha Research and Production Floor. |
| Mufflers consume extra oxygen or fail inside Station rooms | Genuine open question | Specific environmental-production rule without an accepted Station atmosphere contract. |
| HAMMER targets and cannons attach to Station docks | Partly corroborated / open | HAMMER is an accepted explicit cargo method; requiring a Physical Station dock and the exact send/receive multiblocks remain open in Define Alpha Transport Roles. |
| Station shells use environment-specific protection materials | Genuine open question | Consistent with object-native capability rules, but exact hazards, materials, and failure behavior remain undefined. |
| Cold, zero-gravity, or radioactive locations enable improved processing | Corroborated direction / routed | Strong example of Destination-Dependent Production. Specific recipes and bonuses belong in Define Alpha Research and Production Floor and Define Celestial Capability Rules. |
| Station observatory performs research because of its orbital view | Genuine open question | Direct candidate for the first mandatory Physical Station, but the owner explicitly left its exact output uncertain. Route to Define First Physical Station Contract. |
| Satellites spread an AE2 network | Genuine conflict / clarification needed | A data or control network may be valid. Direct interplanetary AE2 item or fluid transfer would violate Require Explicit Interplanetary Logistics. The source does not distinguish these meanings. |
| Automated Outposts represent non-visitable bodies and are operated through the Star Map | Corroborated | Matches Automated Facility terminology, non-dimensional Star Map Objects, and the accepted persistent-asteroid representation. |
| Minor asteroids have generated properties that govern available operations and resources | Corroborated direction / routed | Object-native properties are accepted; exact generation, resource rules, and balance remain open in Define Celestial Capability Rules and Define Asteroid Automation Contract. |
| Automated Facility power, resource, production, and logistics modules | Genuine open question | Candidate capability families. No complete Alpha module portfolio is accepted. |
| Automated Facility modules require recurring upkeep and stop without supplies | Corroborated candidate / routed | Matches Define Player Presence and Automation Tradeoffs. Exact inputs, cadence, buffers, shutdown, and restart behavior remain deliberately open. |
| Automated Outposts cannot use direct inventory transfer and rely on ships or railguns | Corroborated | Matches explicit interplanetary logistics and the distinction between remote automation and local inventory access. |
| Standard HAMMER is intra-system and a larger Railcannon is inter-system | Genuine open question | The accepted route model avoids arbitrary categorical boundaries. Range, endpoint, and vehicle capability rules must be derived before this split is accepted. |
| Cargo must reach an orbital Station before descending to a planetary surface | Genuine open question | A possible logistics topology, but it must emerge from endpoint and transport capabilities rather than an unconditional destination rule. |
| Progression order: manual Rockets, Physical Stations, low-thrust Spaceships, Automated Outposts, then interplanetary Railcannons | Partly corroborated / open | Early manual travel and later automation fit current direction; a pre-Mars Physical Station remains provisional. Exact tiers, engines, and the final Railcannon step remain unaccepted. Route to Define Alpha Transport Roles and Define Player Presence and Automation Tradeoffs. |
| Automated Outposts trade flexibility for fast standardized construction and large-scale automation | Corroborated direction | Fits the accepted automation trade-off: player time is replaced by capital, logistics, constraints, and possible upkeep rather than removed for free. |
| Automated Facilities are managed through integrated Star Map interfaces | Corroborated | This is part of the accepted Automated Facility definition. Exact UX is implementation work. |
| Local AE2 feeds endpoint logistics multiblocks | Genuine open question | Compatible with explicit transport if AE2 only supplies or receives local endpoint inventories. It must not become direct interplanetary teleportation. |

## Superseded Material

- `Theia`, `Hemateria`, the Vael System, and their fixed Rocket-tier destination assignments are retired working names and progression plans. Current design starts from the GTNH destination baseline; the inactive destination designer's concepts remain deferred until owner review.
- Hardcoded `Rocket Core tier -> allowed dimensions` is superseded by route eligibility derived from vehicle, endpoint, environment, and payload variables.
- A mandatory research tree culminating in a Mars unlock is not accepted. Research may become part of a concrete pre-Mars capability, but Define First Physical Station Contract intentionally leaves that decision open.
- Any direct interplanetary AE2 transport conflicts with the accepted ban on teleporting players, items, or fluids between celestial destinations.
- Ore-generation placement, Moon ore lists, and resource-tier judgments in the checklist are non-authoritative.

## Deferred or Outside the Current Alpha Decision Floor

- Full custom Gantry routing and inertial animation.
- Final models, textures, GUI layouts, multiblock shapes, sky overlays, and visual asset inventories.
- Hydroponics and bee optimization aboard Stations unless selected by the later Alpha research and production floor.
- A unified late-game high-speed Railcannon network until the Alpha transport roles and route model are resolved.
- Grappling hook, visible wearable tanks, player gear rendering, dynamic plumes, dismount timing, and similar isolated presentation or quality-of-life tasks.
- Returnable Rocket parts and combined orbital fuel-tank/engine units until their gameplay contracts are specified.

## Historical Alpha Checklist: Provenance Only

The checklist remains useful as evidence of previously anticipated work, but not as accepted scope. This includes:

- recipe, casing, machine, module, fuel-line, Moon-processing, and GTNH integration tasks;
- airlock and Gantry rewrites, Rocket automation, satellite handling, Research Outpost implementation, fuel consumption, and Rocket-part behavior;
- Star Map help, mechanic documentation, and dismount behavior;
- model, multiblock, GUI, texture, and sky-art inventories.

Promote an item from this checklist only when an accepted Alpha capability or active implementation issue requires it.

## Highest-Value Inputs for Later Tickets

1. Use the Station proposal as source material for Define First Physical Station Contract, especially the observatory, environmental protection, docks, and destination-dependent processing candidates.
2. Use the Automated Facility proposal in Define Celestial Capability Rules and Define Asteroid Automation Contract, preserving the accepted Star Map abstraction and explicit-logistics constraints.
3. Use the flight and module proposals only after Define Vehicle Capability and Route Requirements establishes the stable route and vehicle vocabulary.
4. Treat the source's research tree, retired planet names, Alpha checklist, and implementation mechanics as historical provenance unless independently re-approved.
