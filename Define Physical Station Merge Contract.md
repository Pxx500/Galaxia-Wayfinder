---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
blocked_by:
  - "[[Resolve Physical Station Controller Succession]]"
  - "[[Define Transport Endpoint Identity and Registration]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Physical Station Merge Contract

## Question

How should an explicit merge of Physical Stations handle construction contact, surviving Station identity, controllers and logistics references without silently changing ownership or routing?

## Established Input

Station membership and controller succession are already accepted. Joining construction with different Station IDs must not silently merge the Stations or select an arbitrary identity. Explicit merge was the preferred direction, but the complete contract was left unconfirmed.

Station-local named endpoint groups are scoped by Station identity. Individual endpoint identities and shared Routing Names are distinct. Controller succession and splitting an existing Station must not be reopened as part of this discussion.

## Owner Direction

On 2026-09-16 the owner asked to inspect existing behavior rather than design an additional merge interaction. Placing the connecting block is itself a manual player action. The phrase "manual connection" must not imply that a separate command or confirmation has been accepted.

The owner considers merging two independently identified Stations a low-priority edge case. A missing merge feature may remain deferred and must not block the current Wayfinder work. The preceding proposals to reject the connecting placement, choose a surviving Station and rewrite references were not accepted.

## Current Implementation Evidence

Read-only inspection of Galaxia master `b1e42710` on 2026-09-16 found airlock-based membership. `TileStation.attemptBoot` at line 222 adopts an existing graph through registered airlocks. `StationGraph.connectPiece` at line 195 and `rebuild` at line 244 traverse airlock controller registrations, not face-connected construction blocks. A structural bridge is therefore not the proposed construction-based identity merge operation. Connecting graph pieces is not evidence of a complete merge of independent assets and their routing references.

Sources are under `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/station/`. This is source inspection, not a new in-game reproduction.

The separate local `station-construction-identity` rework already detects conflicting construction ownership. In its `Station.blockAdded` at line 334, a new structural block is claimed only when its six neighbors identify exactly one Station. With two Station IDs, the block remains physically placed but unclaimed. This path neither merges identities nor removes the block, drops an item or notifies the player. `claimConnectedConstruction` at line 365 also stops without applying collected additions when it encounters another Station's construction. A new controller touching different Station identities refuses boot in `TileStation.attemptBoot` at line 237. No complete identity/reference merge was found in the inspected rework paths.

These local conflict guards are existing implementation facts, not owner approval of an unclaimed bridge as the final design. The rework is separate from master and was inspected without modification.

## Deferred Scope

If this case becomes relevant, revisit identity, ownership and reference handling together with the actual construction implementation. No new command, confirmation, automatic merge or reference-rewrite behavior is selected now. Room discovery and validation optimization remain separately deferred.
