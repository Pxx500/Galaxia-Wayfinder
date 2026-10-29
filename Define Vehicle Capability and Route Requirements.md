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

# Vehicle Capability and Route Requirements

## Accepted Decision

Evaluate the concrete assembled vehicle and scheduled mission using structural/propellant mass, thrust, usable delta-v, local gravity/atmosphere, maneuver timing, duration, endpoint compatibility and existing infrastructure. Explain failures through missing capabilities rather than a destination whitelist. Accepted design is not an implemented or balanced propulsion model.

## Vehicle And Cargo

- Alpha Rockets have one main propulsion stage. Detachable boosters and multi-stage vehicles are outside Alpha.
- Cargo contents never add mass under the accepted model, not only as an Alpha shortcut. Cargo Modules contribute their structural mass whether full or empty.
- Ordinary non-container items are accepted. Container rejection includes nested storage and packaged-fluid bypasses. [[Define Bulk Fluid Cargo Contract]] owns exact coverage and blacklist/whitelist choices.
- Bulk fluids use general dedicated freight capacity, not separate gas/liquid modules. Freight is distinct from propulsion supplies.
- Actual tanks contain real resources. Propellant types may give different delta-v per liter. Provisional ownership assigns thrust to engines and fuel performance to propellants, with mass and volume affecting the resulting capability. Oxidizer and exact engine/propellant rules remain open.
- Costs include scheduled propellant consumption and module repair/replacement. [[Define Automated Rocket Turnaround and Module Wear]] owns bounded wear, expected-value presentation, failure consequences and automated service.

## Mission And Presentation

Surface ascent, orbital burns, landing and endpoint handling are separate checks. [[Define Destination Access Levels]] owns physical/environmental constraints and the provisional finite-burn model.

- Evaluate only scheduled segments/actions. Do not include an unscheduled return. Planned replenishment separates later propellant requirements.
- Before commitment, explain cost factors, satisfied capabilities, unmet requirements and practical consequences. An opaque total or disabled action is insufficient.
- The default summary shows transfer time, required delta-v and usable delta-v from actual supplies. [[Define Rocket Route Fuel Budgets]] owns allowances and fuel-efficiency/speed selection.
- Physical volume/capacity remains available for servicing and resource inspection rather than the primary budget comparison.
- An adjacent small `?` control provides a hover factor breakdown instead of occupying the main interface.
- For an infeasible route show the localized equivalent of `Route impossible`, not a misleading cost. The same control names concrete vehicle or endpoint blockers.

Exact formulas, propulsion representation and numerical tuning remain implementation/prototype choices.

## Implementation Evidence

Read-only inspection on 2026-09-12 found that `registry/rocketmodules/rocket/analysis/RocketAnalyzer.java:23` partitioned decoupler stages and checked thrust using a fixed mass multiplier. `RocketStage.java:26` used fixed Isp 300 and nominal-capacity-based dry mass. `registry/orbital/OrbitalTransferPlanner.java:124` did not accept vehicle propulsion. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

These prototypes do not establish destination-aware gravity, real-propellant or finite-burn feasibility. Their staging does not approve staging for Alpha.

## Gameplay Flow

The player assembles a Rocket, supplies propulsion resources and plans its scheduled actions. Before commitment, the route view shows transfer time and delta-v and explains missing vehicle or endpoint capabilities. Only the scheduled segments and planned replenishment determine the budget.
