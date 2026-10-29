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

# Tier Destination Portfolio

Each Ore Tier uses a **Tier Destination Portfolio** that supports at least one player-chosen **Valid Tier Route**, rather than prescribing one planet or itinerary.

## Portfolio and Routes

Galaxia authors destinations, their activities, resources, capabilities, conditions, rewards and prerequisites, as well as the Tier Gate's required results or capabilities. A Valid Tier Route is any accessible sequence that satisfies that gate without a Progression Bypass. Consistent world and production rules constrain broad progression order.

| Destination relationship | Meaning |
| --- | --- |
| Mandatory | Every valid route needs it |
| Alternative | Different choices can satisfy the same requirement |
| Optional | No Tier Gate depends on it |

These relationships emerge from the content rather than being assigned to force an itinerary. Optional destinations do not count toward required Alpha closure, but their included mechanics must not be orphaned. Alternatives are welcome when supported by content, not a quota. A single route is valid when meaningful resource, environment and capability rules produce it.

Every valid route uses [[Require Persistent Tier Infrastructure|Persistent Tier Infrastructure]] under the current Alpha default. It may be on a surface, in orbit or elsewhere in space, with deliberate tier-specific exceptions possible.

## Baseline Examples

These examples describe the current GTNH/Galacticraft ore-layout logic and are evidence for the portfolio model, not final Galaxia Alpha destination assignments:

- Under the one-based counting used in this charting discussion, the starting accessible-world group is Tier 1 and the Mars group is Tier 3.
- In the current Mars-group ecosystem, Desh availability makes Mars part of every known valid route, while alternative access to the other progression resources associated with that group, including uranium, Draconium, and Orichalcum, lets the player choose Deimos or Phobos. The resulting route uses at least two destinations but not all three.
- This can be expressed as `Mars AND (Deimos OR Phobos)`, describing the ecosystem's consequences rather than a hardcoded itinerary.
- Later groups repeat alternative sourcing. Ceres, Ganymede, and Callisto illustrate destinations whose overlapping new-resource access may allow one route to substitute for another. The exact resource matrix remains subject to verification against [[GTNH Ore Progression Baseline]].

## Destination Design and Validation

Capability and progression compatibility matter more than matching the baseline planet count. Prefer fewer destinations with deeper activity to many shallow extraction stops. A consolidated destination may take on several baseline bodies' responsibilities if critical resources, capabilities, route choices and Tier Gates remain available at the intended point. Alpha need not use, visit or implement every available destination, and destination count per tier is a content decision.

Celestial properties such as atmosphere composition, pressure, temperature, gravity, illumination and orbital conditions can give persistent infrastructure a purpose. For example, atmospheric compression could produce the actual local mixture or its components. Do not use an exact environmental value solely as a disguised planet identifier.

Each tier needs a content specification for incoming capabilities, required results, destination contributions and optional content. Validate at least one route, the viability of intended alternatives, absence of bypasses, and progression-critical earliest access when consolidating destinations. The minimum depth of destination-specific infrastructure remains open.

## Existing Atmosphere Foundation

The current code already provides part of the required foundation:

- `CelestialBodyProperties` authors surface pressure and weighted atmosphere-fluid ingredients.
- `GalaxiaAtmosphereFluids` registers atmosphere gases as GT fluids.
- celestial properties can derive weighted values from the local atmosphere composition.

The current code search did not surface a complete compressor or production integration that consumes those facts to produce location-dependent atmospheric output. That consumer remains later design and implementation work.

Resolved on 2026-07-31. The baseline examples are evidence for the model, not final Galaxia assignments.

## Related Topics

- Define Closed Tier Cycle
- GTNH Ore Progression Baseline
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder

## Gameplay Flow

The player chooses accessible destinations and activities that together supply a tier's required results. A destination is mandatory only if every valid route needs it, and alternatives exist when different choices satisfy the same requirement.

The route must close the tier without bypassing progression and, under the current Alpha default, use persistent infrastructure. A single route is valid when it follows from meaningful resource, environment and capability rules.
