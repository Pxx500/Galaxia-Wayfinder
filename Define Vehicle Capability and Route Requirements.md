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

# Define Vehicle Capability and Route Requirements

## Question

What is the smallest physics-informed, balance-authored model that can derive modular vehicle capability and route requirements from vehicle assembly, endpoints, atmosphere, gravity, travel time, and infrastructure without becoming a literal aerospace simulator or a destination whitelist?

## Resolution

Alpha evaluates each concrete mission from the assembled single-stage vehicle, its structural and propellant mass, engine thrust, available delta-v, endpoint compatibility, local gravity and atmosphere, maneuver timing, mission duration, and existing infrastructure. Surface ascent, orbital maneuvers, landing, and endpoint handling remain separate checks with concrete failure reasons. Route summaries expose transfer time, required delta-v, propellant use, and an on-demand factor breakdown. Cargo contents do not change vehicle mass, and nested portable item containers are rejected to prevent recursive capacity. Exact formulas and separate fuel or oxidizer design are later propulsion and implementation-prototype decisions rather than blockers for this capability contract.

## Accepted Requirements

The route and vehicle contract is accepted. Numerical tuning and the propulsion representation remain implementation-time work, not evidence of completed balance.

- Alpha Rockets use one propulsion stage representing the main Rocket. Multi-stage vehicles and detachable boosters are outside the Alpha capability model.
- Vehicle eligibility and route cost derive from multiple endpoint, environment, and vehicle variables rather than atmosphere alone or a hardcoded destination whitelist.
- Before the player commits to a route, the interface must explain the derived result in accessible terms: contributing cost factors, satisfied capabilities, unmet requirements, and the practical consequence for the selected vehicle.
- Explainability is part of the route model's product contract. An internally correct calculation presented only as an opaque total or disabled action is insufficient.
- The default route summary presents the selected mission's most important actionable values: transfer time, required delta-v, and expected propellant use relative to available tank capacity.
- For the Alpha single-stage Rocket, propellant use is shown as required volume, tank capacity, and percentage, for example `6,200 / 8,000 L (78%)`.
- Route values are calculated for the concrete scheduled flight segment or mission sequence. Unscheduled return travel is not included, and planned refueling separates the propellant requirements of later flight segments.
- Different propellants may provide different available delta-v per liter. Oxidizer requirements and the exact engine-propellant interaction remain open for the later propulsion design.
- The provisional capability split treats the engine as the source of thrust and the propellant as the source of available delta-v per stored volume. Stored volume and total vehicle mass still contribute to the resulting vehicle capability.
- Cargo inventory contents do not contribute mass to the accepted model. This is not merely an Alpha limitation. A Cargo Module contributes only its own structural module mass, whether its inventory is empty or full.
- Cargo transport rejects nested item-storage payloads that preserve or expose another item inventory. This prevents backpacks, storage cells, and similar containers from recursively multiplying transport capacity.
- The initial Alpha blacklist applies to the container item type even when a particular instance is empty. Ordinary block-items that do not preserve their inventory when itemized remain valid cargo.
- This type-level rule is provisional and may be relaxed later for a concrete safe use case.
- Rocket operating cost includes propellant consumed by the scheduled mission and module-specific repair or replacement costs. Module wear must integrate with automated turnaround rather than require repeated manual servicing.
- Module wear is statistically variable around one player-visible expected value derived from mission duration, relevant exposures, and module-specific coefficients. Sampling timing and the precise bounded safety guarantee retain the provisional status recorded in [[Define Automated Rocket Turnaround and Module Wear]]. A module that reaches zero durability during transit loses its capability and applies its module-specific failure consequence.
- A small adjacent `?` information control exposes a hover summary of how each factor influenced the total. The factor breakdown is available on demand rather than occupying the primary route interface.
- When the selected vehicle cannot perform the route, the summary displays `Route impossible` instead of a misleading total cost. The same `?` control lists the concrete blocking capabilities or endpoint constraints.

## Current Prototype Boundary

Read-only inspection on 2026-09-12 found that the current Rocket analyzer is not the accepted capability model. `registry/rocketmodules/rocket/analysis/RocketAnalyzer.java:23` partitions decoupler-based stages and checks launch thrust against mass using a fixed multiplier. `registry/rocketmodules/rocket/analysis/RocketStage.java:26` uses fixed Isp 300 and nominal fuel-capacity-based dry mass. These paths do not establish destination-aware gravity, propellant, or finite-burn feasibility. `registry/orbital/OrbitalTransferPlanner.java:124` accepts bodies, time, and route priority rather than vehicle propulsion. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

The current staging prototype does not approve staging for Alpha. The accepted single-stage and environment-aware requirements remain resolved design with implementation work outstanding.
