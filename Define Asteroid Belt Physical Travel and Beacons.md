---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
secondary_areas:
  - Area - Travel and Logistics
blocked_by:
  - "[[Define Celestial Object and Gameplay Space Mapping]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Asteroid Belt Physical Travel and Beacons

## Question

How does physical player travel into an asteroid belt coexist with persistent Star Map asteroids that cannot be visited directly?

## Resolution

Asteroid-belt gameplay has two separate layers: persistent Star Map asteroids for remote infrastructure and a planned ring-shaped Regional Dimension for physical player travel.

### Persistent Star Map Asteroids

- Asteroids shown on the Star Map are stable persistent objects.
- The player cannot physically travel to or stand on them.
- Rockets and Spaceships may travel to them when their route capabilities allow it.
- They may host persistent remote infrastructure such as Automated Outposts and provide effectively inexhaustible resource extraction.
- They are not physical terrain instances inside the belt's Regional Dimension.

### Planned Asteroid Belt Regional Dimension

- The current asteroid-belt dimension is a normal dimension. The following design extends it; the ring geometry and coordinate routing do not exist yet.
- The belt will become one very large player-accessible Regional Dimension shaped as a ring.
- Every selectable point on the belt's Star Map band will map to coordinates in that dimension.
- The player will right-click a point on the belt, choose `Fly here`, and target the corresponding physical coordinates.
- The dimension will continue to contain locally generated smaller asteroids for direct exploration and mining. These remain distinct from persistent Star Map asteroids.

### Belt Beacon

- Arbitrary belt coordinates are difficult to revisit reliably without a persistent anchor.
- The player will place a working-name `Beacon` block inside the Regional Dimension.
- Placing a Beacon will register its dimension coordinates as a persistent Star Map travel point.
- The player can then target that point for reliable return flights.
- `Beacon` is the working name.

## Current Code Boundary

- Frozen Belt currently uses a normal dimension with procedurally generated local asteroids.
- Persistent asteroid minor bodies already have stable celestial keys and Star Map positions.
- The current Star Map presentation explicitly gives the asteroid-belt container no interaction target.
- Ring-shaped world semantics, belt-point coordinate routing, `Fly here`, and Beacons are not implemented.

## Consequences

- Selecting a persistent Star Map asteroid and selecting a physical belt coordinate are different actions with different travel rules.
- A Belt Beacon creates a persistent travel anchor; it does not turn nearby generated terrain into a persistent Star Map asteroid.
- Player-built bases in the Regional Dimension use Beacons for repeatable navigation.
- The new routing should deepen the existing celestial, Star Map, and dimension owners rather than introduce a parallel asteroid-only identity system.

## Remaining Fog

- Exact mapping from a rendered belt point to dimension coordinates and the ring's world geometry.
- [[Define Belt Beacon Lifetime]] owns retained markers and team-scoped deletion after Beacon destruction. Broader sharing, final naming and limits remain open.
- Arrival safety, collision handling, and spawn placement around arbitrary coordinates and Beacons.
- Whether a first visit may target any belt coordinate or must satisfy scan, range, or trajectory constraints.
- How Rockets and Spaceships differ when traveling to persistent Star Map asteroids versus physical Belt Coordinates.

## Related Topics

- Define Celestial Object and Gameplay Space Mapping
- Define Player Presence and Automation Tradeoffs
- Define Tier Destination Portfolio
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder

## Gameplay Flow

Once the applicable access conditions are met, a player selects a point on the belt and uses `Fly here` to reach coordinates in its planned Regional Dimension. First-visit conditions remain open. There they explore and mine locally generated asteroids, and can place a Beacon to register a reliable return point on the Star Map.

Persistent Star Map asteroids are separate remote infrastructure targets. Eligible vehicles can travel to them, but players cannot stand on them.
