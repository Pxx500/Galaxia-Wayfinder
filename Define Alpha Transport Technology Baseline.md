---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Progression]]"
secondary_areas:
  - Area - Travel and Logistics
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Alpha Transport Technology Baseline

## Question

Which transport introduction stages and progression-material roles form the accepted working baseline for route design?

## Resolution

First spaceflight begins at HV. Small Hammers span EV, IV, and LuV, large Hammers span LuV, ZPM, and UV, and the first Spaceship requires IV production after desh access. The material roles below are accepted working assumptions. This resolves the baseline only, not the exact route feasibility, recipes, or full progression portfolio.

## Working Transport Introduction

Owner direction on 2026-09-11:

| Transport | Working production stage | Material and capability context |
| --- | --- | --- |
| First spaceflight by Rocket | HV | The opening space missions start at HV, before EV infrastructure |
| Small local Hammer variants | EV, IV, LuV | Existing module tiers retained as the working design |
| Large Hammer variants | LuV, ZPM, UV | Existing module tiers retained as the working design. LuV appears in both families |
| First Spaceship | IV | Comes after desh access and requires an IV production recipe. Desh is a probable construction ingredient, not yet a fixed recipe |

These stages guide production requirements, not player-level permission checks. The accepted transport topology is owned by Define Alpha Transport Roles.

### Hammer Tier Progression

On 2026-09-11 the owner accepted retaining the existing module model for now. Higher tiers within one Hammer family improve firing frequency and charging speed. The small or large family determines energy capacity and the supported connection scope. Exact numbers remain tuning values.

The inspected module configuration uses 60, 45, and 30 second shot cooldowns across each family's three tiers at 20 TPS. Small Hammers hold 500,000 EU and large Hammers hold 8,000,000 EU. Energy cost is derived from route delta-v. Capacity does not grow with tier within a family. These are current implementation values, not permanent balance contracts.

The physical Hammer must receive proper tier progression in later implementation. Its current controller constructs a large UV module unconditionally and still contains a tiering TODO. Retaining the module model does not approve this hardcoded physical-machine setup as the finished gameplay.

Evidence inspected on 2026-09-11: `ModuleHammer`, `HammerVariant`, `FacilityModuleRegistry`, `HammerDispatchPlanner`, and `TileHammerCannon` in the Galaxia checkout. No implementation change was made during this decision.

## Working Material Direction Beyond Luna

These are accepted working material roles, not a completed route through all ten Ore Tiers. Remaining route assignments belong to Map Alpha Tier Routes.

On 2026-09-11 the owner selected titanium, desh, and naquadah as the working material direction for the progression under discussion. Platinum is not retained as a required material in this proposed Galaxia route, even though it appears in the original GTNH Rocket construction recipe.

This is a provisional material selection, not an exact recipe or a requirement that all three materials be available before the same flight. In particular, naquadah must not silently become a prerequisite for reaching its intended first source. Exact recipes and remaining material assignments are open.

### Desh Vehicle Parts

On 2026-09-11 the owner accepted desh as the working material for lighter vehicle structures and tanks that retain their capacity. Lower dry mass can improve payload or achievable maneuvers with the same propulsion and fuel. This does not assign desh a simultaneous improvement to thrust, fuel performance, and every other vehicle property. Numerical performance and production costs remain balance work.

Original GTNH research retains its platinum requirement as historical source evidence. This decision concerns Galaxia's target route, not removal of platinum from the wider modpack.

### Callisto Coolant and Europium

On 2026-09-11 the owner proposed using Callisto ice as the source of a special coolant that enables higher-tier engines. This is the working Galaxia role for the material rather than copying its original Rocket plating role.

The owner provisionally accepted coolant as a third engine fluid, alongside fuel and oxidizer. The added supply complexity remains a reason to revisit this choice. Processing recipes, exact quantities and eligible engine specifications are not finalized.

[[Define Engine Coolant Consumption]] owns the accepted consumable-coolant rule, preserving ongoing demand for extraction and supply.

The owner proposed that a subsequent planet after Callisto have sufficiently high gravity to require higher-thrust engines for landing. Callisto supplies the coolant before that capability is needed at the later destination. The destination, numerical gravity, and required vehicle performance remain open balance choices. This expresses a capability-based progression proposal, not a destination whitelist.

The working assumption is that reaching this later destination requires both a lightweight vehicle and higher-thrust propulsion. The owner deferred evaluating an earlier lightweight-vehicle bypass until concrete balance work. This combination is provisional, not a proven feasibility threshold.

The owner flagged the risk of overly linear gameplay. The accepted nearby asteroid source below provides one alternative supply route. Further alternatives remain open for later design and are not required before continuing.

The owner accepted an asteroid orbiting Callisto as a working alternative source of Callisto Ice. An Automated Outpost extracts its resource and eligible docked vehicles handle transport. This offers an alternative to surface extraction on Callisto while keeping the source in Callisto's vicinity. It uses the existing asteroid Outpost model and does not make this asteroid a player-visitable moon or require an orbital Station around it.

Callisto Ice in other asteroid belts remains a candidate, not an accepted placement. A synthetic coolant route was also proposed but not accepted. Exact asteroid abundance, discovery, extraction balance, and access costs remain open. Alternative logistics alone does not remove a linear technology prerequisite.

The owner confirmed that europium is required at higher tiers. Its assignment to a particular part remains open. This does not yet specify a new Galaxia recipe or independently settle every alternative to the original fusion acquisition route.

## Decision Boundary

[[Define First Coolant Engine Production Stage]] places first use roughly after access to the relevant fuel and coolant. No fixed LuV production requirement was accepted. Full-route dependencies remain in [[Map Alpha Tier Routes]].

Extracted from already accepted rounds on 2026-09-12 so the complete Ore Tier audit does not block access to settled baseline decisions.
