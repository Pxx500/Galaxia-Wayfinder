---
type: source
status: reviewed
origin: "Repository docs/architecture/frozen-belt-ring-beacons-and-travel.md"
imported: 2026-08-01
tags:
  - galaxia/alpha
  - wayfinder/source
  - galaxia/destinations
  - galaxia/travel
---

# Repo Source - Asteroid Belt Ring and Beacons

Source: repository design document `docs/architecture/frozen-belt-ring-beacons-and-travel.md`
Imported: 2026-08-01

The implementation slices and code-level acceptance plan were intentionally discarded. The retained model is already represented by Define Asteroid Belt Physical Travel and Beacons; this note preserves additional conceptual requirements and provenance.

## Wayfinder Integration

- The integrated concept is a generic [[Define Celestial Object and Gameplay Space Mapping|Asteroid Belt]] model; `Frozen Belt` remains only the source document's working name.
- The dual-scale representation is covered by [[Define Celestial Object and Gameplay Space Mapping]].
- Belt-coordinate travel and navigation anchors are covered by Define Asteroid Belt Physical Travel and Beacons.
- Remaining implementation details and open choices in the snapshot are not accepted by this classification.

## Source Snapshot

### Locked Dual-Scale Model

- The Frozen Belt has a strategic Star Map scale and a physical ambient scale.
- The strategic scale contains the belt and a finite set of persistent giant asteroids with ordinary celestial identities.
- The physical scale is one large, player-accessible ring-shaped Regional Dimension containing procedural ambient asteroid terrain.
- The two scales share themes and content families but do not share individual asteroid identity or coordinates.
- Ambient asteroid terrain never becomes a celestial body, knowledge record, or persistent per-blob object.
- A strategic giant asteroid must never resolve to an arbitrary ambient terrain blob.

### Ring And Entry Requirements

- The physical belt forms a deterministic annular volume rather than a uniform field.
- The center and far exterior remain empty, with density concentrated in the ring tube.
- The same world inputs produce the same terrain regardless of generation order.
- Initial belt travel resolves to a stable, safe entry point derived from the same world layout.
- Existing local terrain can be regenerated during development; no legacy coexistence is required.

### Belt Beacon Requirements

- A Belt Beacon is a team-owned navigation point inside the Regional Dimension.
- It is not a celestial body, remote asset, or independent Registry citizen.
- Placement creates a durable travel anchor; block destruction removes it, while chunk unload does not.
- Only the owning team sees and uses the point by default.
- The Star Map marker is a view of authoritative team state.
- Repeated travel to the same beacon resolves to the same coordinates.

### Travel Requirements

- Players select destination identity, not authoritative coordinates.
- The server validates access and resolves a safe position.
- Travel distinguishes ordinary celestial or base targets, default belt entry, and team navigation points.
- Unknown, stale, or unauthorized destinations are rejected.
- Physical belt-coordinate travel and travel to persistent strategic asteroids remain different actions.

### Remaining Decisions

- Final Beacon name, ownership limits, removal and destruction behavior, and team visibility exceptions.
- Exact rendered-belt-point to Regional Dimension coordinate mapping.
- Arrival safety and collision behavior.
- Whether first entry can target any belt coordinate or requires prior scanning or route capability.
- How Rockets and Spaceships differ for strategic asteroid travel and physical belt travel.


## Related Decisions

- [[Define Celestial Object and Gameplay Space Mapping]]
- Define Asteroid Belt Physical Travel and Beacons
