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

## Question

How should an in-flight logistics delivery behave when its physical Station endpoint still has a durable identity but its controller is temporarily unloaded, unavailable, reformed, or permanently destroyed?

## Resolution

Temporary unavailability preserves the endpoint identity and the delivery waits for that endpoint to become available again. Permanent destruction ends the identity and has vehicle-specific consequences. A Rocket or Spaceship completes travel to the destination object's vicinity, retains its cargo, and waits for the player to assign a new destination. A Hammer package targeting a permanently destroyed receiver is lost because it cannot navigate, hold position, or redirect itself.

## Accepted Requirements

- The problem is specific to physical Stations. Abstract Automated Facilities remain continuously represented by their authoritative asset state.
- A Physical Station retains its backing `CelestialAsset.ID` through controller succession as defined in [[Resolve Physical Station Controller Succession]].
- Chunk unload and temporary multiblock disformation do not end that identity.
- Destroying the main controller does not end Station identity when another controller takes over. Destroying an individual endpoint still ends that endpoint's exact identity.
- A delivery addressed by Station ID and Routing Name selects its concrete compatible receiver at arrival. Destruction of an earlier group member does not lose the delivery when a matching replacement exists at arrival. [[Define Transport Endpoint Identity and Registration]] owns this rule.
- A delivery already in flight continues toward its exact endpoint identity while that identity exists.
- If the delivery arrives while the endpoint is temporarily unavailable, it must wait against that endpoint identity and complete after the controller becomes available again.
- Reappearance must produce the same arrival result as if the endpoint had been available at the original arrival time.
- A full destination inventory already retains the undelivered remainder and retries.
- The design must distinguish temporary unavailability from permanent destruction without introducing a second Station identity registry.
- The implementation should deepen the existing Station asset and logistics owners with the smallest practical production-code increase.
- Requiring explicit decommission as the only deletion path is unsafe because a player may destroy a controller and leave an unreachable identity permanently registered.
- Physical item and fluid contents remain in dimension-backed inventories. Controller destruction primarily risks logical identity, display and logistics configuration, construction state, in-flight delivery targets, and other exact references rather than deleting the physical inventories themselves.
- A Rocket or Spaceship whose exact destination is destroyed does not disappear with that endpoint. It still reaches the destination object's vicinity and remains represented by flight-system data with its cargo intact.
- The waiting location can be described as orbit or nearby space as appropriate for the object. It does not require inventing an Eligible Orbit around a low-gravity asteroid or creating a physical entity or landing site.
- The vehicle maintains an active notification about the lost destination and waits for the player to assign a replacement. It does not silently pick another receiver.
- Movement to the replacement target obeys ordinary flight requirements. Reassignment does not teleport the vehicle or cargo.
- Waiting near the destination for a replacement target or resolution of a blocking problem consumes no fuel and causes no module durability loss. Normal flight and maneuver costs resume when the vehicle actually travels. Waiting does not introduce a hidden countdown to vehicle loss.
- An already launched Hammer package cannot be held or redirected when its exact receiver is permanently destroyed. The package and its cargo are lost.
- Hammer loss on permanent receiver destruction does not change the accepted waiting behavior for a temporarily unloaded controller, a disformed multiblock with a surviving controller, or a full receiving inventory.

## Logistics Source Availability

A physical Station without an available live controller emits no current logistics supply or demand signal. This does not delete the Station's persistent identity or cancel its in-flight deliveries. Signals retain their source identity, are visible only to the owning team, and do not retain stale contributions after a source becomes unavailable or the client session is cleared.

Retained from the September 2026 logistics decisions during the 2026-09-11 cleanup. The rule does not prescribe a snapshot cache, packet shape, or per-tick implementation.

## Current Implementation Evidence

Read-only inspection on 2026-09-12 under `src/main/java/com/gtnewhorizons/galaxia/` answered the delivery ownership checks:

- `registry/outpost/logistics/LogisticStore.java:84` and `:114` retain arrived cargo that cannot be inserted and retry the remaining amount without creating another inventory. Pending inbound amounts also reduce further demand at line 185.
- `handlers/CelestialEventHandler.java:53` and `:66` drive server delivery updates. `core/persistence/FacilityPersistenceManager.java:194` and `:247` restore and save delivery time, identities, amounts, and trajectory data.
- `registry/celestial/station/Station.java:56` exposes no inventory children while its controller is unavailable. A zero insertion leaves cargo pending. A missing destination asset follows the delivery-loss path in `LogisticStore`.

This is evidence for the existing Hammer delivery path, not implementation of Rocket or Spaceship waiting and rerouting. Temporary-controller reload parity still needs runtime verification.

`registry/celestial/station/TileStation.java:587` can transfer the same backing asset ID to a successor controller. [[Resolve Physical Station Controller Succession]] accepts this continuity for the Station. It does not preserve the exact identity of a destroyed Silo or other individual endpoint.

Define Bulk Repair of Broken Endpoint References establishes that bulk replacement preserves a flight already in progress. The vehicle reaches the original object's vicinity before recalculating travel to the replacement. Notification and any acknowledgement use the general team notification system, whose detailed presentation remains deferred.

## Provenance

Owner decision in the Wayfinder conversation on 2026-09-10: the Rocket arrives near its destination, waits for a new target, and keeps its cargo. Hammer packages are lost because they are unguided launched objects without propulsion for recovery.

## Related Topics

- [[Define Transport Endpoint Identity and Registration]]
- [[Define Space Transport Dispatch Model]]
- [[Evaluate Team-Scoped Logistics Ledger]]
- [[Area - Travel and Logistics]]
