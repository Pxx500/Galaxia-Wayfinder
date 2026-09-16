---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Destinations
blocked_by:
  - "[[Define Galacticraft-Equivalent Destination Backfill]]"
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Minimum Galacticraft-Equivalent Destination Contract

## Question

What is the minimum playable contract for a retained Alpha destination that receives a Galacticraft-equivalent backfill instead of a unique Galaxia-specific gameplay loop?

## Resolution

A Galacticraft-Equivalent Destination is complete enough for Alpha when it provides a functional round-trip extraction destination connected to the intended progression.

This contract describes a physically visited Galacticraft-equivalent destination. It must not be generalized into a requirement that every Star Map Object own a dimension; regional and non-dimensional objects require role-specific Gameplay Representations.

### Required Capabilities

- **Travel in:** the player can reach and enter the destination using the capabilities available on its intended Ore Tier route.
- **Playable dimension:** the destination has a functioning player dimension with the basic terrain, world generation, and environmental rules needed for normal play.
- **Intended operation:** the player can survive and perform the destination's basic activity using equipment available at the intended progression stage.
- **Required ore access:** the destination generates and exposes the ores it must contribute to its Tier Destination Portfolio and Ore-Backed Tier Gate.
- **Complete extraction activity:** the player can locate, acquire, and carry or export the required material through a real gameplay interaction rather than receiving it from a placeholder or debug path.
- **Travel out:** the player can leave the destination and return the extracted result to the place where its progression processing continues.
- **Progression continuation:** the extracted and processed result participates in a Valid Tier Route and advances a Closed Tier Cycle without creating a dead end.

### Not Required by This Contract

- A unique research mechanic.
- A destination-specific production chain beyond what its required progression material needs.
- Automated Facilities or destination-specific automation.
- A unique narrative, encounter, or bespoke gameplay loop.
- Final mechanical depth or permanent protection from later redesign.

Persistent Tier Infrastructure remains an Ore Tier-level requirement. This minimum contract does not require every Galacticraft-Equivalent Destination to host its own permanent base or unique infrastructure when the tier satisfies that requirement elsewhere.

## Consequences

- A Star Map-only scaffold entry never satisfies this contract.
- A destination is not complete merely because its dimension loads; the extraction result must connect to subsequent progression.
- Basic Galacticraft-style extraction is an accepted Alpha completion path when stronger destination design is unavailable.
- The contract defines a floor, not a target depth, and backfilled destinations remain eligible for later Galaxia-specific redesign.

## Remaining Fog

- The shared technical and content template used to implement this contract efficiently across multiple destinations.
- Which environmental facts, terrain assets, world-generation features, and ore parameters vary per backfilled destination.
- How Alpha communicates that a basic destination is complete and playable without implying that it has final planned depth.

## Related Topics

- Define Celestial Object and Gameplay Space Mapping
- Define Galacticraft-Equivalent Destination Backfill
- Define Closed Tier Cycle
- Define Tier Destination Portfolio
- Require Persistent Tier Infrastructure
- GTNH Ore Progression Baseline
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder
