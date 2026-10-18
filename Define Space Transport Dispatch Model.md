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

# Define Space Transport Dispatch Model

## Accepted Decision

Alpha Rockets and Spaceships execute player-authored, vehicle-owned linear schedules. Top-level Travel Blocks connect endpoint Visit Blocks, whose actions are local to that occurrence. Modes are `Run once` and `Loop`. This is the accepted minimal scheduler contract, not an implemented scheduler or central fleet queue.

The Factorio Space Age-inspired tile editor and its scheduler are the actual Rocket system, not optional infrastructure added after a separate opening-only executor. The first satellite deployment uses this same vehicle, resource and action ownership. [[Define Rocket Route Fuel Budgets]] extends places and generated routes, while prepared servicing visits retain the endpoint rules below. An orbital payload-deployment action does not require a fabricated receiver endpoint. The Factorio reference is inspiration, not approval of its entire condition catalogue or circuit-network integration.

## Schedule Ownership And Execution

- Each persistent vehicle stores its schedule, mode, current block/nested action and execution state. The Star Map observes and edits it.
- A visit targets one exact Transport Endpoint or symbolic Endpoint Group. The editor selects a celestial object first, then its team's targets. The body provides environmental/orbital context, not the final prepared transport address.
- Visit actions include load, unload, refuel and expected maintenance. Repeated visits to one endpoint may have different actions. Different endpoint types may offer different servicing.
- Schedules have no branches, `if/else`, `goto` or conditional next-action choice. A current action completes and advances or remains current waiting/retrying.
- `Run once` stops after the sequence. `Loop` returns to the first block after the last.
- Evaluate each flight against actual vehicle state, modules, propulsion, endpoint conditions and planned refueling. Costs cover only scheduled actions. An unscheduled return is not assumed.
- [[Define Rocket Route Fuel Budgets]] owns route-tile allowances, usable delta-v, fuel-efficiency/speed priorities and forecast guidance.
- A busy destination pad does not block an otherwise feasible departure. The Rocket reaches the destination and waits before docking with maneuver fuel intact.
- [[Define Rocket Missions Without Recovery]] owns deliberate terminal disposal and its planning warning. Waiting is not disposal.

## Cargo Actions And Priorities

Vehicle-directed transfers specify cargo and exact amounts. Endpoint-owned cargo rules participate by default without the vehicle copying, requesting or knowing them. Both sides may configure multiple transfers and compatible actions can execute during one visit.

- Vehicle actions have policy priority. A dock cannot veto them by configuration, although capacity, supply and other physical limits still apply.
- Each visit has `Block dock actions`, disabled by default. It is neither a global vehicle setting nor an endpoint-wide rule.
- Allowing dock actions accepts the dock's completion policy. The vehicle has no separate override for whether those actions hold the visit open.
- A dock chooses one policy for its whole cargo configuration: `Best effort` transfers what it currently can and completes, while `Wait until complete` holds the visit until its requirements are met. Individual instructions do not select separate policies.
- Exact vehicle transfers remain blocking until their amount is moved. Best effort is dock-owned, not duplicated on both sides.
- An impossible-to-progress waiting dock service maintains the visit and one active notification. Partial best-effort transfer is completion, not failure.
- Conflicting dock actions yield to vehicle actions with a concrete warning rather than silently changing either configuration.
- [[Define Bulk Fluid Cargo Contract]] applies the same visit/load/unload semantics to direct fluid freight. Propulsion refueling remains separate.

## Failure And Observability

A failed action emits a typed event with one concrete localized reason, such as insufficient fuel. It remains current and retries at a bounded cadence until successful or edited. Maintain one active notification for the vehicle, action and reason, not one per retry. Success clears it and advances.

Blocked, waiting, failed and completed work must be observable to the team through [[Define Team Notification System]]. Exact retry cadence is tuning. Existing Hammer dispatch does not define Rocket/Spaceship behavior automatically.

## Deferred Scope

Autonomous supply/demand assignment may later create short vehicle-owned schedules for jobs such as moving a resource from A to B. It remains above the same executor, not a replacement ownership model. Alpha does not require that layer or final fleet interaction design.

## Implementation Evidence

Read-only inspection on 2026-09-12 found dimension destination/construction state in `registry/rocketmodules/tileentities/TileEntitySilo.java:43,74,445,483`, under `src/main/java/com/gtnewhorizons/galaxia/`. That does not implement vehicle itineraries, Visit Blocks, groups, retries or maintenance checks.

## Related Decisions

- [[Define Alpha Transport Roles]]
- [[Define Player Flight Interaction Model]]
- [[Define Player Presence and Automation Tradeoffs]]
- [[Define Automated Rocket Turnaround and Module Wear]]
