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

# Transport Endpoint Identity and Registration

## Endpoint Identity

Prepared logistics targets a team-owned Transport Endpoint or symbolic Endpoint Group, not a whole celestial object. CelestialAsset provides the identity foundation, and transport is an optional asset capability. Manual Unprepared Landing and physical Belt Coordinates use separate travel contracts.

## Ownership And Registration

- A standalone physical endpoint creates a CelestialAsset on first successful multiblock formation, not controller placement. Its controller retains that asset ID through disformation and unload, which disable availability until reform or reload.
- Destroying the controller removes the asset. Rebuilding or relocating creates a new asset and Endpoint ID. IDs are never reused.
- Automated Facilities reuse their asset, which can own multiple subordinate endpoints rather than endpoint child assets.
- Physical Station machines belong to the Station asset and inherit its Station ID, but have distinct exact Endpoint IDs. Destroying an endpoint breaks its identity, not the Station. [[Resolve Physical Station Controller Succession]] preserves Station identity.
- Endpoints belong directly to a team UUID. Builder identity is provenance, not an ownership chain. Multiple endpoints may share a body.
- Singleton and multiplayer ownership use the same model. Merging transfers consumed-team assets to the surviving team. Leave or kick does not transfer established infrastructure to the departing member.

GTNHLib gives a new unteamed player a random-UUID singleton. A singleton has one member. Before deleting a consumed team, GTNHLib synchronously emits `TeamMergeEvent(consumed, surviving)`. Leave or kick creates a singleton without that event.

## Exact Targets And Symbolic Groups

| Target | Identity and scope | Change behavior |
| --- | --- | --- |
| Exact endpoint | Immutable Endpoint ID, independent of mutable Routing Name | Destruction breaks the reference and requires explicit repair |
| Standalone Endpoint Group | Team, celestial object, compatible endpoint kind and Routing Name | Eligible members may change without schedule edits |
| Physical Station group | Team, Station ID, compatible endpoint kind and Routing Name | Same-named machines in another Station are excluded, even on the same body |

A standalone or Automated Facility asset exposing one logical endpoint may use its asset ID as Endpoint ID. Multiple endpoints inside one Station cannot all use Station ID as exact identity.

- New endpoints get a unique default name such as `Landing Pad #353`. Players may rename and deliberately reuse names.
- Groups provide routing equivalence, not proof of equivalent cargo or maintenance services. Physical automation remains the player's responsibility.
- A group visit selects an eligible compatible member, skipping unavailable members. If none are available, retain the symbolic target, wait and maintain one active notification.
- Destroying a member warns the team but does not break the group. Even an empty group remains valid and resumes when a compatible endpoint recreates its key.
- Renaming an endpoint changes group membership without changing Endpoint ID. Renaming a symbolic group across schedules requires a separate explicit bulk operation.
- For Station-and-Routing-Name deliveries, retain the symbolic destination in flight and choose the receiver at arrival. A compatible same-name replacement in that Station can receive it. This does not waive launch feasibility.
- An unavailable exact target waits with one active notification. Reform or reload restores routing without schedule edits.
- Broken exact references retain original body and endpoint kind for explicit repair defaults. [[Define Bulk Repair of Broken Endpoint References]] permits an explicit body override for relocation.
- Destruction should expose the Endpoint ID and practical command suggestion/autocomplete rather than requiring long-ID typing.

## Automated Facility Services

Alpha exposes one logical endpoint per Automated Facility. Each landing-capable module adds a service slot, not another player-visible endpoint. The facility assigns slots and all modules share its item inventory rather than per-module pipe networks.

Physical endpoints and Automated Facilities may offer different services. More facility endpoints could support independent routing without changing asset identity, but Alpha does not require them.

The schedule editor selects the celestial object, then that team's registered endpoints/groups. A grouped maintenance visit does not prove repair happened. Actual unchanged durability can block the next departure under [[Define Automated Rocket Turnaround and Module Wear]].

## Implementation Evidence And Provenance

Original research found no shared Silo/Pad/Dock routing identity. TileEntitySilo used world coordinates. TileStation and CelestialAssetStore provided the closest backing-asset pattern, with ownership, indexing, naming and synchronization.

Inspection on 2026-09-12 confirmed existing asset team-transfer hooks in `handlers/TeamEventHandler.java:48`, `registry/celestial/CelestialServerRuntime.java:35` and `registry/celestial/CelestialAssetStore.java:286`. `registry/celestial/station/TileStation.java:572` could transfer backing identity to a successor. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. This does not establish implemented Silo IDs, endpoint groups or Station-local named routing.

Station-local group scope and arrival-time receiver selection were established on 2026-09-13.

## Related Decisions

- [[Define Space Transport Dispatch Model]]
- [[Define Vehicle Capability and Route Requirements]]
- [[Define In-Flight Delivery Handling for Unavailable Physical Stations]]

## Gameplay Flow

Players select a team's exact endpoint or a named group when configuring a prepared visit. A group can route to an available compatible member, while an exact endpoint retains its identity through temporary disformation or unload.

Destroying an exact endpoint breaks its references and calls for explicit repair. A group remains valid even when empty and can resume when a compatible member with the same group key becomes available.
