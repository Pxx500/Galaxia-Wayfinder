---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Space Transport Dispatch Model

## Vehicle Schedules

Rockets and Spaceships execute player-authored, vehicle-owned linear schedules. Travel Blocks connect endpoint Visit Blocks, whose actions apply to that visit. A schedule can `Run once` or `Loop`.

The tile editor and scheduler also serve the first satellite deployment. They are inspired by Factorio Space Age, without adopting its condition catalogue or circuit-network integration. [[Define Rocket Route Fuel Budgets]] extends places and generated routes. Orbital payload deployment needs no receiver endpoint.

## Schedule Ownership And Execution

- Each persistent vehicle stores its schedule, mode, current block and action, and execution state. Players view and edit it through the Star Map.
- A visit targets one exact Transport Endpoint or symbolic Endpoint Group. The editor selects a celestial object first, then its team's targets. The body provides environmental/orbital context, not the final prepared transport address.
- Visits can load, unload, refuel and expect maintenance. Repeated visits may have different actions, and endpoint types may offer different services.
- Schedules have no branches, `if/else`, `goto` or conditional next-action choice. An action either completes and advances or waits and retries.
- `Run once` stops after the sequence. `Loop` returns to the first block after the last.
- Evaluate flights against actual vehicle state, modules, propulsion, endpoint conditions and planned refueling. Costs cover scheduled actions only, with no assumed return.
- [[Define Rocket Route Fuel Budgets]] owns route-tile allowances, usable delta-v, fuel-efficiency/speed priorities and forecast guidance.
- A busy destination pad does not block an otherwise feasible departure. The Rocket reaches the destination and waits before docking with maneuver fuel intact.
- [[Define Rocket Missions Without Recovery]] owns deliberate terminal disposal and its planning warning. Waiting is not disposal.

## Cargo Actions And Priorities

Vehicle actions specify cargo and exact amounts. Endpoint cargo rules participate by default without the vehicle copying, requesting or knowing them. Each side may configure multiple transfers, and compatible actions can run in one visit.

- Vehicle actions have policy priority. A dock cannot veto them by configuration, although capacity, supply and other physical limits still apply.
- Each visit has `Block dock actions`, disabled by default. It is neither a global vehicle setting nor an endpoint-wide rule.
- Allowing dock actions accepts the dock's completion policy, without a vehicle override for whether they hold the visit open.
- A dock chooses one policy for its whole cargo configuration. `Best effort` transfers what it can and completes. `Wait until complete` holds the visit until its requirements are met. Individual instructions cannot choose different policies.
- Exact vehicle transfers remain blocking until their amount is moved. Best effort is dock-owned, not duplicated on both sides.
- A dock service that cannot progress keeps the visit open with one active notification. A partial best-effort transfer completes rather than failing.
- Conflicting dock actions yield to vehicle actions with a concrete warning rather than silently changing either configuration.
- [[Define Bulk Fluid Cargo Contract]] applies the same visit/load/unload semantics to direct fluid freight. Propulsion refueling remains separate.

## Failure And Observability

A failed action emits a typed event with one concrete localized reason, such as insufficient fuel. It remains current and retries at a bounded cadence until successful or edited. Maintain one active notification for the vehicle, action and reason, not one per retry. Success clears it and advances.

The team can observe blocked, waiting, failed and completed work through [[Define Team Notification System]]. Retry cadence remains tuning. Hammer dispatch does not define Rocket or Spaceship behavior.

## Deferred Scope

Autonomous supply and demand assignment may later create short vehicle-owned schedules using the same executor. Alpha does not require this layer or a final fleet interaction design.

## Implementation Evidence

Read-only inspection on 2026-09-12 found dimension destination/construction state in `registry/rocketmodules/tileentities/TileEntitySilo.java:43,74,445,483`, under `src/main/java/com/gtnewhorizons/galaxia/`. That does not implement vehicle itineraries, Visit Blocks, groups, retries or maintenance checks.

## Related Decisions

- [[Define Alpha Transport Roles]]
- [[Define Player Flight Interaction Model]]
- [[Define Player Presence and Automation Tradeoffs]]
- [[Define Automated Rocket Turnaround and Module Wear]]

## Destination Selection

Selecting a celestial destination in a schedule opens the actual Star Map rather than a separate planet list. Use the shared destination-selection behavior.

Source: Rocket implementation feedback, 2026-10-18.

## Gameplay Flow

A player gives a Rocket or Spaceship a schedule of visits and travel, chooses whether it runs once or loops, and sets the actions for each visit. The vehicle carries out those actions using its own instructions and any allowed dock rules.

When an action cannot progress, it waits and retries while a notification identifies the problem. A Rocket headed to a busy pad still travels there and waits for docking capacity.
