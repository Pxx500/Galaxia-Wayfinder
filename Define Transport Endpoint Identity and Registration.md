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

## Accepted Decision

Prepared logistics targets a team-owned Transport Endpoint or symbolic Endpoint Group, not a whole celestial object. CelestialAsset supplies the identity foundation. Transport is an asset capability, not a capability of every asset. Manual Unprepared Landing and physical Belt Coordinates retain their separate travel contracts. These are accepted requirements, not a completed endpoint registry.

## Ownership And Registration

- Standalone physical endpoints create a backing CelestialAsset on first successful multiblock formation, not controller placement. The controller persists its asset ID for its lifetime. Temporary disformation or unload disables availability without deleting identity. Reform/reload reconnects the same asset.
- Destroying a standalone controller removes the backing asset. Rebuilding or relocating creates a new asset and Endpoint ID. IDs are never reused.
- Automated Facilities reuse their existing asset. One asset may own multiple subordinate endpoints, not endpoint child assets.
- Within a Physical Station, machines belong to the Station asset and inherit its Station ID. They do not each create another Station asset. Individual exact Endpoint IDs remain distinct from Station ID.
- Destroying a Station endpoint breaks its exact identity, not the surviving Station. Station-controller succession preserves Station identity under [[Resolve Physical Station Controller Succession]].
- Endpoints belong directly to a team UUID. Builder identity is provenance, not a live builder-to-current-team ownership chain. Multiple endpoints may share a body.
- Singleton and multiplayer team ownership use the same model. Joining/merging transfers consumed-team assets to the surviving team. Ordinary leave/kick does not transfer established infrastructure to the departing member.

GTNHLib creates a random-UUID singleton for a new unteamed player. Singleton status derives from one member. It emits `TeamMergeEvent(consumed, surviving)` synchronously before deleting a consumed team. Leave/kick creates a new singleton without that merge event.

## Exact Targets And Symbolic Groups

| Target | Identity and scope | Change behavior |
| --- | --- | --- |
| Exact endpoint | Immutable Endpoint ID, independent of mutable Routing Name | Destruction breaks the reference and requires explicit repair |
| Standalone Endpoint Group | Team, celestial object, compatible endpoint kind and Routing Name | Eligible members may change without schedule edits |
| Physical Station group | Team, Station ID, compatible endpoint kind and Routing Name | Same-named machines in another Station are excluded, even on the same body |

A standalone or Automated Facility asset exposing one logical endpoint may use its asset ID as Endpoint ID. Multiple endpoints inside one Station cannot all use Station ID as exact identity.

- New endpoints get a unique default name such as `Landing Pad #353`. Players may rename and deliberately reuse names.
- Groups provide routing equivalence, not proof of equivalent cargo or maintenance services. Physical automation remains the player's responsibility.
- A group visit selects one eligible compatible member. Unavailable members are skipped. If none are available, retain the symbolic target, wait and maintain one active notification.
- Destroying one member does not break the group. Warn that the member was destroyed and retain remaining members.
- Empty groups remain valid unavailable targets. A compatible endpoint recreating the same key automatically resumes existing references.
- Renaming an endpoint changes group membership without changing Endpoint ID. Renaming a symbolic group across schedules requires a separate explicit bulk operation.
- For Station-and-Routing-Name deliveries, retain the symbolic destination in flight and choose the receiver at arrival. A compatible same-name replacement in that Station can receive it. This does not waive launch feasibility.
- Exact unavailable targets retain their identity and wait with one active notification. Reform/reload restores routing without schedule edits.
- Broken exact references retain original body and endpoint kind for explicit repair defaults. [[Define Bulk Repair of Broken Endpoint References]] permits an explicit body override for relocation.
- Destruction should expose the Endpoint ID and practical command suggestion/autocomplete rather than requiring long-ID typing.

## Automated Facility Services

Alpha exposes one logical endpoint per Automated Facility. Each landing-capable module adds a service slot, not another player-visible endpoint. The facility assigns slots and all modules share its item inventory rather than per-module pipe networks.

Physical endpoints and Automated Facilities may offer different service workflows. A future concrete need for independent routing can justify more facility endpoints without changing asset identity, but it is not an Alpha requirement.

The schedule editor selects the celestial object, then that team's registered endpoints/groups. A grouped maintenance visit does not prove repair happened. Actual unchanged durability can block the next departure under [[Define Automated Rocket Turnaround and Module Wear]].

## Implementation Evidence And Provenance

Original endpoint research found no shared Silo/Pad/Dock routing identity. TileEntitySilo had world/coordinate identity, while TileStation and CelestialAssetStore already supplied the closest backing-asset pattern, ownership, indexing, naming and synchronization.

Inspection on 2026-09-12 confirmed existing asset team-transfer hooks in `handlers/TeamEventHandler.java:48`, `registry/celestial/CelestialServerRuntime.java:35` and `registry/celestial/CelestialAssetStore.java:286`. `registry/celestial/station/TileStation.java:572` could transfer backing identity to a successor. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. This does not establish implemented Silo IDs, endpoint groups or Station-local named routing.

Owner clarification on 2026-09-13 establishes Station-local group scope and arrival-time receiver selection. It narrows celestial-object grouping to standalone endpoints rather than contradicting it.

## Related Decisions

- [[Define Space Transport Dispatch Model]]
- [[Define Vehicle Capability and Route Requirements]]
- [[Define In-Flight Delivery Handling for Unavailable Physical Stations]]
