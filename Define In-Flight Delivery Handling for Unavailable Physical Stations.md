---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by:
  - "[[Define Transport Endpoint Identity and Registration]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define In-Flight Delivery Handling for Unavailable Physical Stations

## Accepted Decision

Temporary physical endpoint unavailability preserves identity and waits. Permanent destruction breaks exact identity, with different consequences for powered vehicles and Hammer packages. Abstract Automated Facilities remain represented by their authoritative asset state.

| Condition | Required behavior |
| --- | --- |
| Surviving controller unloaded or multiblock disformed | Preserve identity and in-flight delivery, wait at arrival, complete after availability returns |
| Occupied planned Rocket pad | Depart if the mission is otherwise feasible, reach the destination, then wait before docking with maneuver fuel intact |
| Full receiving inventory | Retain undelivered remainder and retry |
| Exact Rocket/Spaceship receiver destroyed | Reach the original body's vicinity with cargo intact, notify and await an explicitly assigned replacement |
| Exact Hammer receiver permanently destroyed | Lose package and cargo, since it cannot hold position or redirect |
| Station controller succeeds another | Preserve Station identity under [[Resolve Physical Station Controller Succession]] |
| Named Station group changes members | Select a compatible receiver at arrival under [[Define Transport Endpoint Identity and Registration]] |

Destroying an individual endpoint does not automatically destroy its Station. A same-name replacement can serve a symbolic Station target, but it does not restore an exact destroyed Endpoint ID.

## Waiting And Redirection

- A waiting Rocket/Spaceship remains flight-system data, not necessarily a physical entity, landing site or invented Eligible Orbit around a low-gravity asteroid.
- Waiting near the destination consumes no fuel and causes no module wear. There is no hidden loss countdown. Actual further travel resumes normal maneuver and wear costs.
- Maintain one active notification for a lost exact target. Do not silently choose another receiver or teleport vehicle/cargo.
- Reassigning or bulk-repairing a target leaves active travel intact. Complete travel to the original object's vicinity, then calculate the journey from that actual location to the replacement using normal fuel, propulsion, time and safety checks. Infeasible onward travel waits.
- A feasible recovery action blocked only by occupancy is not an intentional mission ending. [[Define Rocket Missions Without Recovery]] owns deliberate disposal with warning.
- Reappearance must yield the same delivery result as availability at the original arrival time. Hammer's permanent-loss rule does not apply to temporary unload, disformation or inventory fullness.

Physical contents stay in dimension-backed inventories. Controller loss primarily threatens identity, logistics configuration, construction state and references, not automatic deletion of those inventories. Use the existing Station/logistics owners rather than a second identity registry. Deletion cannot rely solely on explicit decommission while a destroyed controller leaves unreachable identity behind.

## Logistics Source Availability

A Station without an available live controller emits no current supply/demand signal. Persistent identity and in-flight deliveries survive. Signals retain source identity, are team-only and drop stale contributions when a source becomes unavailable or the client session clears.

General route-change notifications and any acknowledgement belong to [[Define Team Notification System]]. Their presentation does not change physical feasibility.

## Implementation Evidence And Provenance

Read-only inspection on 2026-09-12 found that `registry/outpost/logistics/LogisticStore.java:84,114,185` retains undelivered cargo, retries insertion and accounts for pending inbound demand. `handlers/CelestialEventHandler.java:53,66` drives delivery updates and `core/persistence/FacilityPersistenceManager.java:194,247` persists delivery identity/time/trajectory. `registry/celestial/station/Station.java:56` exposes no inventory while its controller is unavailable. Missing destination assets follow a loss path. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

This supports the existing Hammer path, not implemented Rocket/Spaceship waiting or verified controller-reload parity. Station-controller identity transfer does not preserve destroyed individual endpoint identity.

Owner decision on 2026-09-10 establishes powered-vehicle cargo retention and Hammer loss. The 2026-09-17 clarification establishes arrival-side occupancy waiting and distinguishes deliberate unrecoverable mission endings.

## Related Decisions

- [[Define Bulk Repair of Broken Endpoint References]]
- [[Define Space Transport Dispatch Model]]
- [[Evaluate Team-Scoped Logistics Ledger]]
