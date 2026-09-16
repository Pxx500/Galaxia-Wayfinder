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

## Question

How are automated Rockets and Spaceships assigned transport work: fixed player-authored routes, autonomous matching of supply and demand, explicit individual orders, or deliberate layers of more than one model?

## Resolution

Alpha uses vehicle-owned, player-authored linear schedules composed of travel blocks and visit blocks, with `Run once` and `Loop` execution. Visit actions are nested inside the relevant visit block. A future supply-and-demand layer may assign simple transport jobs by creating short schedules for vehicles, but it remains a higher-level abstraction rather than replacing vehicle ownership or execution.

## Established Input

- This ticket defines the accepted Rocket and Spaceship dispatch contract. Its resolution does not certify an implemented scheduler.
- Alpha requires at least a minimal vehicle scheduler so Rockets and Spaceships can perform useful transport automation without repeated manual launches.
- A player selects a concrete persistent vehicle and assigns an ordered sequence of top-level blocks. Travel blocks represent flight between endpoints. Visit blocks represent the vehicle being present at one endpoint and contain visit-specific actions such as unloading, loading, refueling, or expecting maintenance before continuing.
- Visit actions belong to one occurrence of a visit block, not globally to the celestial object or endpoint. Repeated visits to the same endpoint may therefore contain different actions.
- A visit block targets either one concrete Transport Endpoint or one Endpoint Group rather than a celestial object in general. For example, a schedule may select one particular team Rocket Pad on Luna or a same-named group whose available member may receive the vehicle.
- The containing celestial object supplies the environmental and orbital context for route calculation, but it is not the final transport destination when a concrete endpoint is required.
- Different Transport Endpoint types may expose different visit automation. In particular, an Automated Facility may eventually support a more advanced endpoint workflow than a physical Rocket Pad or Dock.
- When authoring a visit, the player first selects the celestial object and then selects an addressable endpoint or endpoint group registered on that object.
- Cargo handling supports vehicle-directed transfers and endpoint-directed servicing during the same visit. A vehicle-directed action names the requested item and amount; the landing pad or dock independently applies its own cargo rules and reports when its work is complete.
- Dock-owned actions participate by default when a compatible vehicle is present. The vehicle does not need to request, duplicate, or know which items the dock intends to move.
- The vehicle and the landing pad or dock each own their own cargo-action configuration. Neither side must duplicate or embed the other side's rules.
- Both sides may configure multiple item transfers rather than being limited to one item type per visit.
- Compatible actions from both sides may execute during the same visit. For example, a vehicle may unload one item while the dock loads another.
- Vehicle-owned actions have higher policy priority because the mobile vehicle may use the same endpoint differently across routes. A dock cannot veto a vehicle action through its configuration, although real inventory capacity, missing resources, or other physical constraints may still prevent the transfer.
- Each scheduled visit has its own `Block dock actions` option, disabled by default. It is not a global vehicle setting. Otherwise compatible dock actions execute in addition to vehicle actions.
- The same vehicle may therefore allow a dock's actions during one visit and block them during another visit to the same endpoint.
- A vehicle does not separately override whether accepted dock actions may hold the visit open. Allowing dock actions means accepting the dock's configured completion policy.
- The dock chooses between two completion policies. `Best effort` transfers as much as it currently can and then completes; `Wait until complete` keeps the service active until its configured transfer requirements are satisfied.
- One completion policy applies to the dock's entire cargo-service configuration. Individual Cargo Instructions do not select separate best-effort or waiting behavior.
- A `Wait until complete` service that cannot currently progress maintains the visit and an active notification. A partial `Best effort` transfer is a completed action rather than a failure.
- Vehicle-owned exact transfer actions remain blocking until their requested amount is transferred. The best-effort choice is currently dock-owned rather than duplicated on both sides.
- When vehicle and endpoint actions cannot be jointly satisfied, the conflicting dock action yields to the vehicle action and the system exposes a concrete warning rather than silently changing either configuration.
- Each persistent Rocket or Spaceship owns and stores its own schedule, execution mode, current block or nested-action position, and execution state. There is no central fleet scheduler that owns every vehicle's queue.
- The Star Map observes and edits vehicle-owned schedules. A future supply-and-demand layer may assign work to vehicles, but the vehicle remains the owner and executor of its schedule.
- Alpha supports two execution modes for an explicit sequence: `Run once` executes the sequence once and stops; `Loop` returns to the first block after the final block and repeats the sequence.
- Alpha schedules are strictly linear. They do not contain branches, `if/else`, `goto`, or conditional selection of the next action.
- Conditions belong to the current action. The action either completes and advances to the next entry or remains current while waiting and retrying.
- Each scheduled flight segment is evaluated separately against the vehicle state, installed modules, available propellant, endpoint conditions, and any planned refueling before that segment.
- Route time, required delta-v, and propellant use cover only the actions and flight segments actually present in the schedule. A hypothetical return is not included until the player schedules it.
- The Alpha scheduler may be a deliberately limited first version. It does not need the final interaction design or every future logistics mode.
- When a scheduled action fails, the scheduler emits a typed failure event with one concrete reason. The rendered notification follows the localized semantic form `Scheduled action failed: <reason>`, such as insufficient fuel, rather than reporting an unexplained generic failure.
- A failed action remains the vehicle's current action. The vehicle retries it at a bounded cadence until it succeeds or the player changes the schedule; the exact retry interval is implementation tuning.
- Repeated attempts maintain one active notification for the current vehicle, action, and reason rather than emitting a new notification on every retry.
- When the action becomes executable and succeeds, the vehicle clears the active notification and advances normally.
- Autonomous supply-and-demand assignment is a future abstraction above the explicit scheduler. It may generate or assign work automatically while reusing the same underlying vehicle actions and execution model, but it is outside the current design frontier.
- The future supply-and-demand layer assigns a simple transport job such as moving a resource from endpoint A to endpoint B. The selected vehicle represents that job as a short vehicle-owned schedule; the higher-level system does not directly execute the vehicle's actions.
- Different vehicle or progression layers may expose different levels of dispatch abstraction.
- The chosen model must make blocked, waiting, failed, and completed work observable to the team.
- Existing HAMMER dispatch behavior is evidence from one transport system, not an automatic contract for Rockets or Spaceships.

## Related Topics

- [[Define Alpha Transport Roles]]
- [[Define Player Flight Interaction Model]]
- [[Define Team Notification System]]
- [[Define Player Presence and Automation Tradeoffs]]

## Current Implementation Boundary

Read-only inspection on 2026-09-12 found a dimension destination and physical construction state in `src/main/java/com/gtnewhorizons/galaxia/registry/rocketmodules/tileentities/TileEntitySilo.java:43`, `:74`, `:445`, and `:483`. These fields do not implement the accepted vehicle-owned itinerary, Visit Blocks, endpoint groups, retries, or maintenance-cycle checks. Existing Hammer supply/request dispatch must not be presented as the Rocket/Spaceship scheduler.

The gameplay contract remains resolved. Scheduler implementation is not another round of unanswered itinerary-design questions.
