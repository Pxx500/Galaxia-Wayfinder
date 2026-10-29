---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Celestial Object and Gameplay Space Mapping

## Objects and Gameplay Spaces

A Star Map Object and a Dimension are separate concepts. Galaxia does not require one dimension per celestial object or one Star Map object per dimension.

### Representation Modes

- A celestial body may own a direct player-accessible dimension, as a conventional planet can.
- A celestial region may own a Regional Dimension shared by the region's gameplay concept.
- A Star Map Object may support persistent infrastructure, extraction, logistics, observation, or other gameplay without having its own player-accessible dimension.
- A Star Map Object may exist for orbital structure or presentation without being a travel destination, but it must still expose at least one meaningful object-appropriate interaction.

### Asteroid Belt Example

- Frozen Belt is a celestial region that may provide a player-accessible asteroid-belt dimension.
- Persistent asteroids shown inside Frozen Belt on the Star Map remain distinct Star Map Objects. They may host persistent resource-producing infrastructure with effectively inexhaustible resources without receiving individual dimensions.
- The Frozen Belt dimension generates smaller local asteroids as physical terrain for player exploration and mining.
- Those locally generated asteroids are not one-to-one physical incarnations of the persistent asteroids shown on the Star Map.
- Both layers represent gameplay in the same broad celestial region at different abstraction levels; they do not require identity or spatial synchronization.

### Completeness Rule

Every retained Star Map Object must satisfy [[Require Star Map Object Actionability|Star Map Actionability]]. It needs a defined Gameplay Representation and at least one meaningful context-menu action, not necessarily its own dimension. Its representation may be direct physical access, access through a Regional Dimension, Star Map-managed infrastructure, or another explicit interaction model.

## Existing Code Alignment

- `CelestialObject` already allows objects without a `PlayableDimensionProfile`.
- Dynamic asteroid minor bodies already resolve as separate celestial objects with stable keys.
- Frozen Belt already has a dimension provider that procedurally generates local asteroids.
- The current dimension materialization path still centers a playable dimension profile on a celestial owner. Regional and indirect representation should deepen that existing celestial/dimension ownership model rather than introduce an asteroid-only parallel registry.

## Consequences

- Do not use `has a dimension` as the general test for whether a celestial object is complete or actionable.
- Travel targets, infrastructure targets, and physical dimension ownership may refer to different levels of the celestial hierarchy.
- Do not attempt to place every persistent Star Map asteroid into the asteroid-belt dimension as matching world geometry.
- Destination contracts must state their intended Gameplay Representation before requiring physical travel, world generation, or return behavior.
- Destination contracts must also identify at least one action derived from the object's authored physical, environmental, or orbital nature.

## Remaining Fog

- Which actions belong to persistent Star Map asteroids and which belong to locally generated asteroids inside the belt dimension.
- Whether locally generated asteroids have any persistent identity, depletion, discovery, or resource-state relationship across visits.
- How the UI distinguishes direct dimensions, regional access, automated-only objects, and contextual objects.

## Related Topics

- Define Asteroid Belt Physical Travel and Beacons
- Require Star Map Object Actionability
- Define Tier Destination Portfolio
- Define Player Presence and Automation Tradeoffs
- Define Minimum Galacticraft-Equivalent Destination Contract
- Define Galacticraft-Equivalent Destination Backfill
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder

## Gameplay Flow

The player may travel directly to a body's dimension, enter a regional space or interact with an object through infrastructure and other map actions. Each retained object needs a meaningful action, even when it has no dimension of its own.

In Frozen Belt, players can explore and mine locally generated asteroids in the regional dimension while managing distinct persistent asteroids on the Star Map. The two layers do not identify matching individual asteroids.
