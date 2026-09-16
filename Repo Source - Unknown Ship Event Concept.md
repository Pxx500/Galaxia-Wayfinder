---
type: source
status: unreviewed
origin: "Repository AI/Briefs/UnknownShipEvent.md"
imported: 2026-08-01
tags:
  - galaxia/alpha
  - wayfinder/source
  - galaxia/observation
---

# Repo Source - Unknown Ship Event Concept

Source: repository planning brief `AI/Briefs/UnknownShipEvent.md`
Imported: 2026-08-01

Implementation mechanisms from the original brief were intentionally discarded during migration. This snapshot preserves only the event concept, requirements, boundaries, and unresolved product decisions.

## Source Snapshot

### Concept

The Unknown Ship is a scripted, team-scoped Star Map event that is separate from logistics. It begins when a team first opens the Star Map, plays out as a long-lived encounter in the viewed stellar system, and leaves behind a persistent anomaly that can become a progression hook for interstellar travel.

### Intended Lifecycle

1. The event waits for a team to activate the Star Map.
2. A portal appears and an unidentified ship enters the system.
3. The ship follows a slow trajectory while dispatching probes to nearby astronomical bodies.
4. The probes return before the ship departs through a second portal.
5. A persistent, researchable anomaly remains after departure.

### Player Interaction

- Before contact, the ship is identified only as `Unknown`.
- The team may attempt contact and receive a changed identity or response.
- The event should be visible and interactive through the existing Star Map experience.
- A development-only trigger may exist, but it is not part of the player-facing contract.

### Requirements And Boundaries

- Event state and mutations are authoritative per team, not global.
- The event, ship, probes, portals, and residue are not logistics tasks, cargo, signals, stations, or ordinary celestial bodies.
- Probes do not interact with inventories, construction, dispatch systems, or station state.
- Visual similarity to logistics markers must not imply shared domain identity.
- The anomaly is durable progression state if the event is retained as an interstellar unlock.

### Open Decisions

- Whether the event belongs in Alpha, later progression, or optional narrative content.
- What the contact attempt changes for the team.
- What research or mission completes the anomaly and unlocks interstellar travel.
- Whether probe paths are presentation only or reflect real orbital routes.
- Whether the event survives reloads before completion.


## Intake

- [[Sources]]
