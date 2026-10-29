---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Destinations
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Galacticraft-Equivalent Destination Backfill

## Scaffold and Backfill

Use the Galacticraft layout first as a Star Map design scaffold, then add minimal Galacticraft-equivalent destination implementations only as a final Alpha backfill where needed.

### Star Map Design Scaffold

- Begin with the Galacticraft celestial system and ore layout represented in Galaxia's Star Map.
- At this stage, scaffold destinations are data used for planning and editing. They do not require backing dimensions, registered blocks, terrain, or playable mechanics.
- Use the visible scaffold to rename, merge, remove, replace, relocate, and reorganize destinations while designing Galaxia's system.

### Galaxia-First Design

- Build Galaxia-specific destination roles, mechanics, and progression on top of the scaffold wherever the team has a concrete design it wants to pursue.
- A scaffold destination does not become playable merely because it exists on the Star Map or has ore assignments.
- Destinations that are removed, merged, or replaced during design do not need a basic implementation of their former Galacticraft version.

### Galacticraft-Equivalent Destination Backfill

- Near the Alpha cutoff, identify destinations the team still wants in the product but for which it cannot quickly define a stronger Galaxia-specific gameplay loop.
- Implement those retained destinations inside Galaxia with a minimal version of their original Galacticraft-style role and behavior.
- This is a Galaxia-owned implementation inspired by the baseline, not runtime delegation to the original Galacticraft or addon implementation.
- The backfill supplies enough real destination content to support its required ore access and Closed Tier Cycle instead of shipping a Star Map-only placeholder.
- Backfilled destinations may be redesigned and deepened in later iterations.

## Consequences

- Alpha may contain both deeply redesigned Galaxia destinations and deliberately basic Galacticraft-equivalent destinations.
- The team can stop inventing new mechanics when further design would delay a working product, without leaving required destinations mechanically empty.
- A dummy Star Map object is planning material, while a backfilled destination is playable Alpha content; they must not be counted as the same completion state.
- Every retained playable Star Map object must satisfy [[Require Star Map Object Actionability|Star Map Actionability]]. If no meaningful object-appropriate interaction can be defined, the object is removed, merged, replaced, or deferred rather than shipped inert.
- The strategy preserves the minimum-first delivery goal without requiring unchanged Galacticraft code or content to remain Galaxia's runtime owner.

## Remaining Fog

- Which scaffold destinations are retained, removed, merged, replaced, or deferred before the Alpha backfill pass.
- How backfilled destinations are marked for later redesign without turning future ambitions into Alpha blockers.

## Related Topics

- Define Celestial Object and Gameplay Space Mapping
- Require Star Map Object Actionability
- Define Minimum Galacticraft-Equivalent Destination Contract
- Define Tier Destination Portfolio
- Define Closed Tier Cycle
- Require Persistent Tier Infrastructure
- GTNH Ore Progression Baseline
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder

## Gameplay Flow

Players reach retained backfilled destinations through Galaxia's own playable implementations and obtain the resources needed for their Closed Tier Cycles. A planning-only Star Map entry does not provide that gameplay or count as a completed destination.
