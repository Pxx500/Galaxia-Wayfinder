---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Progression]]"
secondary_areas:
  - Area - Destinations
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Tier Destination Portfolio

Resolved: 2026-07-31

## Question

Does every Ore Tier correspond to one required celestial destination, or can multiple mandatory and alternative destinations collectively satisfy its [[Define Closed Tier Cycle|Closed Tier Cycle]]?

## Resolution

An Ore Tier is defined by a **Tier Destination Portfolio**, not by one planet. Galaxia authors the portfolio's destinations, capabilities, activities, rewards, prerequisites, and Tier Gate requirements; the player constructs a **Valid Tier Route** through that ecosystem.

The system constrains the order of broad progression through consistent world and production rules. Each portfolio must contain enough Progression-Bearing Destinations to support at least one valid route. Multiple alternatives are welcome when the content supplies them, not a quota that every objective must satisfy.

## Portfolio Structure

- A Tier Gate defines the results or capabilities that must be obtained, not a quest-authored list of planets to visit.
- Destinations expose activities, resources, capabilities, operating conditions, and prerequisites.
- A **Valid Tier Route** is any player-chosen sequence of accessible actions and destinations that satisfies the Tier Gate without a Progression Bypass.
- **Mandatory**, **alternative**, and **optional** are derived classifications. A destination is mandatory only when every valid route happens to require it; destinations are alternatives when different choices can satisfy the same requirement; a destination is optional when no Tier Gate depends on it.
- A route may resolve logically to `Mars AND (Deimos OR Phobos)`, but that expression describes the consequences of the authored ecosystem rather than a hardcoded itinerary imposed on the player.
- Optional destinations do not count as required Alpha closure, but any mechanics included on them must still avoid becoming orphaned.

## Baseline Examples

These examples describe the current GTNH/Galacticraft ore-layout logic and are evidence for the portfolio model, not final Galaxia Alpha destination assignments:

- Under the one-based counting used in this charting discussion, the starting accessible-world group is Tier 1 and the Mars group is Tier 3.
- In the current Mars-group ecosystem, Desh availability makes Mars part of every known valid route, while alternative access to the other progression resources associated with that group, including uranium, Draconium, and Orichalcum, lets the player choose Deimos or Phobos. The resulting route uses at least two destinations but not all three.
- Later groups repeat alternative sourcing. Ceres, Ganymede, and Callisto illustrate destinations whose overlapping new-resource access may allow one route to substitute for another. The exact resource matrix remains subject to verification against [[GTNH Ore Progression Baseline]].

## Galaxia Content Direction

- Galaxia does not preserve the baseline destination count as a product requirement.
- Capability and progression compatibility matter more than literal planet-for-planet parity.
- Prefer fewer destinations with deeper, destination-specific activity over many shallow locations used only for brief ore extraction.
- Build a Progression Ecosystem whose authored rules let players discover and choose their own valid routes; do not turn the destination portfolio into a planet-by-planet quest chain.
- A consolidated destination may absorb progression responsibilities previously spread across several baseline bodies, provided every critical resource, capability, route choice, and Tier Gate remains available at the intended point.
- Destination roles should exploit authored celestial properties such as atmosphere composition, pressure, temperature, gravity, illumination, or orbital conditions to create reasons for persistent infrastructure.
- Destination-dependent production is one available mechanism: for example, atmospheric compression can produce the actual local atmospheric mixture or its components instead of a universal dimension-independent air output.

## Existing Atmosphere Foundation

The current code already provides part of the required foundation:

- `CelestialBodyProperties` authors surface pressure and weighted atmosphere-fluid ingredients.
- `GalaxiaAtmosphereFluids` registers atmosphere gases as GT fluids.
- celestial properties can derive weighted values from the local atmosphere composition.

The current code search did not surface a complete compressor or production integration that consumes those facts to produce location-dependent atmospheric output. That consumer remains later design and implementation work.

## Consequences

- Each Ore Tier needs a later ticket defining its portfolio rules, incoming capabilities, required results, available destination contributions, and optional content rather than prescribing one canonical route.
- Tier validation must demonstrate that at least one Valid Tier Route exists, that intended alternatives are genuinely viable, and that no route creates a Progression Bypass.
- A destination may become mandatory as an emergent consequence of being the only source of a required result; it should not be marked mandatory merely to force a preferred itinerary.
- Destination consolidation must be checked against progression-critical earliest access and meaningful route alternatives, not only against total ore availability.
- Alpha does not require every available destination to be used, visited, or implemented.
- The exact number of destinations per tier is a content decision, not a global invariant.
- A single available route is valid when it follows from meaningful resources, environment and capabilities. Do not create interchangeable alternatives merely to avoid a unique destination. Conversely, an exact environmental value chosen only as a disguised planet identifier does not make a location lock meaningful.
- Under the current Alpha default, every Valid Tier Route also depends on [[Require Persistent Tier Infrastructure|Persistent Tier Infrastructure]], although the asset may be surface-based, orbital, or elsewhere in space and later tier-specific exceptions may be added deliberately.
- The minimum required depth of destination-specific infrastructure remains a separate Wayfinder question.

## Related Topics

- Define Closed Tier Cycle
- GTNH Ore Progression Baseline
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder
