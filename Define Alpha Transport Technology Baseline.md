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

# Alpha Transport Technology Baseline

## Accepted Working Baseline

These production stages guide routes and recipes, not player permission checks or proof of completed balance.

| Transport | Production stage | Material context |
| --- | --- | --- |
| First Rocket spaceflight | HV | Before EV infrastructure |
| Small local Hammers | EV, IV, LuV | Retain existing module family |
| Large Hammers | LuV, ZPM, UV | LuV belongs to both families |
| First Spaceship | IV, after desh access | IV production recipe required, desh is a probable ingredient rather than a fixed recipe |

Higher tiers within each Hammer family improve firing frequency and charging speed. Family determines energy capacity and connection scope, not a tier-growing tank. Exact values remain tuning.

## Current Hammer Tuning And Gap

The module configuration inspected on 2026-09-11 uses 60, 45 and 30 second cooldowns at 20 TPS across each family's tiers. Small capacity is 500,000 EU and large capacity 8,000,000 EU. Shot energy derives from route delta-v. These are implementation values, not permanent balance contracts.

Evidence: `ModuleHammer`, `HammerVariant`, `FacilityModuleRegistry`, `HammerDispatchPlanner` and `TileHammerCannon`. The physical controller hardcoded a large UV module with a tiering TODO. Retaining the module model does not accept that as finished physical progression.

## Working Material Roles

Titanium, desh and naquadah are the selected working direction, not exact recipes or a requirement to obtain all three before one flight. Platinum is not required by this proposed Galaxia route, although it remains historical GTNH Rocket-recipe evidence and may exist elsewhere in the modpack. Naquadah cannot become a circular prerequisite for reaching its first source.

- Desh provides lighter structures and tanks retaining capacity. Lower dry mass can improve payload or maneuvers with the same fuel. It does not simultaneously improve thrust, fuel performance and every other property.
- Callisto Ice is a proposed source of special higher-engine coolant, rather than copying its original plating role. Coolant is provisionally a third fluid alongside fuel and oxidizer. Added supply complexity remains a reason to revisit it. [[Define Engine Coolant Consumption]] owns ongoing consumable demand.
- A later destination after Callisto may require high-thrust engines for landing and a lightweight vehicle. This is a provisional capability-based progression proposal, not a proven threshold or destination whitelist. No destination, gravity or exact performance is selected.
- An asteroid orbiting Callisto is an accepted working alternative Callisto Ice source. An Automated Outpost extracts it and eligible docked vehicles transport it. It is not player-visitable and needs no invented orbital Station.
- Europium is required at higher tiers. Its part/recipe assignment and alternatives to original fusion acquisition remain unspecified.

## Proposals And Open Choices

Exact recipes, part performance, material costs, asteroid abundance/discovery/extraction costs and full ten-Ore-Tier routes remain open in [[Map Alpha Tier Routes]]. The lightweight-vehicle bypass awaits concrete balance work.

Callisto Ice in other belts and synthetic coolant remain unaccepted candidates. The nearby asteroid gives alternative logistics but does not by itself remove a linear technology prerequisite. Further alternatives remain possible.

[[Define First Coolant Engine Production Stage]] places first coolant-engine use roughly after relevant fuel/coolant access. No fixed LuV production requirement was accepted.

## Provenance

Direct owner decisions on 2026-09-11, extracted as a baseline on 2026-09-12. Transport topology is owned by [[Define Alpha Transport Roles]].

## Gameplay Flow

Players first reach space by Rocket at the HV production stage, then develop local Hammer infrastructure and an IV Spaceship after access to desh. These stages guide recipes and infrastructure rather than imposing abstract transport permissions.

Later material and engine choices may enable harder routes. Exact recipes and route thresholds remain open, including how coolant and lightweight vehicles affect progression.
