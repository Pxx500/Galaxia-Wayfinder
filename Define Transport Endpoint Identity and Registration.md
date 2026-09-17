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

# Define Transport Endpoint Identity and Registration

## Question

How do concrete physical and abstract destinations such as Rocket Pads, Docks, and Automated Facilities become stable, team-addressable Transport Endpoints that the Star Map and Vehicle Schedules can target without treating an entire celestial object as the destination?

## Resolution

Every prepared logistics destination is a Transport Endpoint owned by a team-owned `CelestialAsset`. Manual Unprepared Landing and physical Belt Coordinates have their separately accepted travel contracts. Exact schedule targets use an immutable Endpoint ID. Interchangeable endpoints use symbolic groups scoped by Station ID for Station members, or by celestial object for standalone endpoints, together with team, compatible endpoint kind and Routing Name. Standalone controllers preserve backing identity across temporary disformation and lose it on destruction. Station identity instead follows the accepted controller-succession contract. Destroyed individual endpoints require explicit repair of exact references, while an empty Endpoint Group remains a valid waiting target and resumes when compatible members recreate the same group key.

## Established Direction

### Physical Station Membership and Named Arrival

Accepted on 2026-09-13. Within a Physical Station, the hierarchy is Station ID, then compatible machines grouped by Routing Name, then individual machines. Machines inherit the owning Station ID as membership. They do not each become a separate Station asset. Same-named machines in another Station are not members of this group, even on the same Celestial Object and within the same team.

A Rocket or Hammer package addressed to a Station and Routing Name retains that symbolic destination during flight. The concrete compatible receiver is selected at the arrival event, not permanently bound before departure. Replacing a machine with another compatible machine of the same name in the same Station before arrival therefore preserves the delivery target. This does not remove route or launch feasibility checks and does not make incompatible receivers interchangeable.

These Station-local rules override the broader celestial-object group scope and per-machine backing-asset wording below for machines belonging to a Physical Station. Standalone endpoints retain the previously accepted scope. Exact endpoint references remain distinct from named group references. Controller succession is owned by [[Resolve Physical Station Controller Succession]].

### General Endpoint Rules

- A vehicle targets one concrete Transport Endpoint or one Endpoint Group, not a celestial object in general.
- Every standalone routable physical endpoint machine receives a backing `CelestialAsset`. The physical controller stores the backing asset ID, while the asset provides durable identity, team ownership, celestial placement, naming, persistence, and Star Map representation. Station members instead use the Station-local ownership rule above.
- A physical endpoint creates its backing `CelestialAsset` when its multiblock successfully forms for the first time, not when the controller block is merely placed.
- After creation, the controller persists the backing asset ID for its own entire lifetime. Temporary multiblock disformation disables the endpoint but does not delete the asset or release its identity.
- Reforming the multiblock reconnects to and enables the same backing asset. It never creates a replacement asset while the original controller and stored asset ID remain.
- Destroying a standalone endpoint controller permanently removes its backing asset. Exact references become broken and require explicit repair. This does not override Station-controller succession or delete a surviving Station when one of its endpoints is destroyed.
- Rebuilding or relocating the physical machine creates a new asset ID.
- The system must support an explicit bulk replacement operation that substitutes one broken endpoint reference with a player-selected replacement across every affected Vehicle Schedule. This requirement is developed in [[Define Bulk Repair of Broken Endpoint References]].
- A controller that still exists but has a disformed multiblock remains registered as the same endpoint with unavailable status. An unloaded, non-chunkloaded controller follows the same rule.
- A Vehicle Schedule targeting one unavailable exact endpoint keeps its reference, waits, and maintains one active notification.
- Endpoint Group selection skips unavailable members. If no member is available, the scheduled action waits until one becomes available.
- Reforming or reloading the endpoint restores it to routing without editing schedules or changing its asset ID.
- Existing abstract Automated Facilities remain their existing `CelestialAsset` rather than creating a duplicate asset solely for transport.
- `CelestialAsset` is the common identity foundation. Transport access remains a capability exposed by that asset and does not make every asset transport-capable.
- A `CelestialAsset` may own one or more Transport Endpoints. The endpoints remain subordinate to the asset rather than becoming child assets.
- Multiple team endpoints may exist on the same celestial object and expose different services or automation.
- Physical Rocket Pads and Docks belong to a world system that is not automatically aware of all Star Map state.
- Automated Facilities may expose a different and potentially more advanced automation contract than physical endpoints.
- Automated Facility modules share one facility-wide item inventory. They do not use physical pipes or move items between per-module inventories as machines do in a normal world.
- Multiple landing-capable modules inside one Automated Facility therefore add potential service capacity or concurrency rather than separate physical item-logistics networks.
- For Alpha, one Automated Facility exposes one logical Transport Endpoint. Each installed landing-capable module adds one service slot to that endpoint rather than creating another player-visible endpoint.
- Vehicle Schedules target the facility endpoint, and the facility assigns an available slot. All slots use the shared Automated Facility Inventory.
- The model may later allow one Automated Facility to expose multiple independent Transport Endpoints if a concrete gameplay requirement needs separate per-pad routing or service policies. This extension does not require changing the facility's `CelestialAsset` identity.
- Every player-built Rocket Pad, Silo, or other physical endpoint has its own stable unique identifier independent of its display or routing name.
- Exact Vehicle Schedule references use the endpoint's immutable Endpoint ID. For a standalone physical endpoint or Automated Facility exposing one logical endpoint, its backing `CelestialAsset` ID supplies that identity. Distinct endpoints within one Physical Station cannot all use the Station ID as their individual exact identity.
- An Endpoint ID is never reused after its endpoint is destroyed. Rebuilding the machine creates a new Endpoint ID even if the player gives it the same Routing Name.
- Routing Name is mutable, may be shared by compatible endpoints, and must never be used as the stable identity of an exact reference.
- A new endpoint receives a default unique name such as `Landing Pad #353`. Players may rename endpoints and deliberately reuse a name.
- Same-named compatible endpoints on the same celestial object may be addressed as one Endpoint Group. A scheduled visit to that group is routed to one eligible member rather than to a preselected exact endpoint.
- Endpoint Group membership requires the same celestial object, routing name, and compatible landing or docking kind. Same-named incompatible endpoint types remain separate routing groups.
- A Vehicle Schedule that targets an Endpoint Group references the group rather than the Endpoint ID of whichever member happens to serve a visit.
- Destroying one group member does not break the group reference while another compatible member remains. It only produces a warning that the member was destroyed and that the group continues through its remaining members.
- A newly created compatible endpoint on the same celestial object joins the existing group when given the same Routing Name. It may therefore take over service before the older members are destroyed without requiring schedule edits.
- An Endpoint Group target is a symbolic key scoped by owning team, celestial object, compatible endpoint kind, and Routing Name. It does not depend on one member's Endpoint ID.
- A broken exact reference retains its original Celestial Object and endpoint kind so repair tooling can default to a same-scope Endpoint Group without asking the player to re-enter that context. The player may explicitly override the Celestial Object when intentionally rerouting schedules to a relocated destination.
- The group remains a valid but unavailable schedule target when no compatible members are registered. The scheduled action waits and maintains one active notification.
- Creating a compatible endpoint with the same group key resurrects the empty group and automatically resumes its existing schedule references.
- Renaming one endpoint moves that endpoint between groups without changing its Endpoint ID. Renaming a group and all references to its symbolic key is a separate explicit bulk operation, which may initially use a chat command.
- Endpoint Groups provide routing equivalence only. The Star Map does not inspect physical cargo, maintenance, or other world-machine automation to prove that members are operationally interchangeable; configuring equivalent infrastructure is the player's responsibility.
- If a grouped visit expects maintenance but the selected endpoint does not actually repair the Rocket, the next departure reads the unchanged durability, remains blocked by the schedule's safety policy, and exposes the active failure notification.
- The schedule editor selects a celestial object first and then lists the team's registered endpoints and endpoint groups on that object.
- Endpoint grouping does not make the celestial object itself the destination.
- An endpoint records the player who built it as provenance, but ownership is not continuously derived from that player's current team.
- GTNHLib creates a singleton team with its own random team UUID when a player first logs in without an existing team. Singleton status is derived from having one member rather than stored as a separate flag.
- Transport Endpoints belong directly to a team UUID, including endpoints built by a player represented by a singleton team. They do not use a dynamic `builder -> current team` ownership chain.
- When a singleton team joins a multiplayer team, GTNHLib synchronously emits `TeamMergeEvent(consumed, surviving)` before deleting the consumed singleton. Galaxia already transfers existing asset ownership through that event. Extending the same behavior to planned physical endpoint identities remains implementation work.
- Once an endpoint belongs to a multiplayer team, it remains with that team if its builder or another member leaves. A departing member cannot take established team infrastructure.
- Normal leave and kick create a new singleton team for the departing player but do not emit `TeamMergeEvent`, so team-owned endpoints remain with the old multiplayer team.
- An intentional merge of two multiplayer teams transfers all team-owned endpoints from the consumed team UUID to the surviving team UUID. This is a whole-team merge, not a departing member taking infrastructure.
- The ownership model supports cooperative play and does not allow a departing member to remove established team infrastructure.
- For Alpha, destroying an endpoint may report its Endpoint ID in chat and provide a command-based repair path such as `/galaxia replace-endpoint <old-id> <new-id>`. A clickable command suggestion or autocomplete should avoid requiring the player to type long IDs manually.

## Historical Architecture Evidence

These findings describe the checkout examined during the original endpoint research. They are not a current implementation or completion claim.


- Physical Silo, Launchpad structure blocks, and station Dock behavior do not currently expose a shared routable endpoint identity to the Star Map.
- `TileEntitySilo` currently has only world and coordinate identity. It has no stable endpoint ID, team ID, routing name, or `CelestialObjectKey`.
- `TileStation` already implements the closest physical-asset pattern. A formed physical controller creates or reconnects to a backing `Station` in `CelestialAssetStore` and persists only the owner and backing asset ID locally.
- `CelestialAsset` already owns stable UUID identity, `CelestialObjectKey`, display name, kind, and celestial location.
- `CelestialAssetStore` already owns team assignment, indexing by team and celestial object, rename, enable or disable state, destruction, persistence flow, team transfer, and Star Map synchronization.
- Chunk unload and physical destruction are distinct lifecycle concepts for physical Stations. Current destruction also includes the successor-controller exception described below, so the historical simple deletion description is incomplete.
- Automated Facilities already use `CelestialAsset`, so using the same owner for physical endpoints can provide one identity and Star Map path instead of a parallel endpoint registry.

## Current Evidence and Reconciliation

Inspection on 2026-09-12 confirms team-merge handling through `handlers/TeamEventHandler.java:48`, `registry/celestial/CelestialServerRuntime.java:35`, and `registry/celestial/CelestialAssetStore.java:286`, under `src/main/java/com/gtnewhorizons/galaxia/`. This proves transfer of existing assets, not completion of Silo endpoint IDs or schedule groups.

`registry/celestial/station/TileStation.java:572` can transfer the same backing asset ID to a successor controller during invalidation. [[Resolve Physical Station Controller Succession]] now accepts Station identity continuity through that succession. The Station-local hierarchy and named arrival contract above remain requirements, not an implementation claim.

## Related Topics

- [[Define Space Transport Dispatch Model]]
- [[Define Automated Rocket Turnaround and Module Wear]]
- [[Define Vehicle Capability and Route Requirements]]
- [[Define Bulk Repair of Broken Endpoint References]]
- [[Define In-Flight Delivery Handling for Unavailable Physical Stations]]
