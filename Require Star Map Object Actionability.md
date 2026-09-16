---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Require Star Map Object Actionability

## Question

What minimum gameplay role must every object retained on the Star Map provide?

## Resolution

Every Star Map Object in Galaxia Alpha must satisfy Star Map Actionability: it must expose at least one meaningful, object-appropriate interaction through its context menu. An object cannot ship only as decoration, an empty menu, or an inert placeholder.

### Object-Native Gameplay

- Supported actions should follow from the object's authored physical, environmental, and orbital properties rather than being arbitrary content attached only to fill a menu.
- A gas giant naturally suggests atmospheric gas extraction.
- A station in stellar orbit may exploit unusually strong solar-energy conditions.
- Rocky bodies may support surface extraction or infrastructure, while remote asteroids may support eligible Automated Facilities and vehicle traffic.
- These examples establish the design direction; they do not yet commit Alpha to a complete mechanic list for every object class.

### Interaction Contract

- A player-accessible dimension is not required. Infrastructure placement, logistics, observation, extraction, regional access, and physical travel are all valid Gameplay Representations when appropriate to the object.
- Structural eligibility still determines which actions make sense for an object. For example, celestial properties may permit a station while rejecting a surface outpost.
- Once a construction action is applicable and exposed, missing construction materials do not by default disable its context-menu button.
- If no meaningful object-appropriate role can be defined by the Alpha cutoff, remove, merge, replace, or defer the object instead of shipping it inert.
- Temporary Star Map-only scaffold entries remain planning material and do not qualify as playable Alpha content.

### Construction Direction

- Selecting an applicable build action creates a Construction Site rather than instantly producing the finished Automated Facility or other asset.
- The Construction Site owns a resource requirement and becomes complete only after the required materials have been delivered.
- GTNH does not expose a reliable player or team technology-tier state. Galaxia therefore cannot truthfully determine that the player "is LuV" or declare a construction available or unavailable from a detected tier.
- The UI may communicate the exact bill of materials and an advisory phrase such as `uses LuV-tier materials`, allowing the player to judge feasibility. Such a label describes the requirements; it is not a claim about the player's current tier.
- The primary construction action creates its Construction Site immediately without opening a mandatory preview or confirmation window.

### Split-Action Presentation

- A construction row in the context menu pairs its primary build button with a smaller `?` information control on the right.
- Hovering the information control shows required materials and other relevant construction information without changing the primary action.
- The primary button immediately creates the Construction Site; the information control is optional and does not introduce a confirmation step.
- Because the information control remains available, Galaxia does not need a saved `skip preview` preference scoped globally or per celestial object.
- After Construction Site creation, the same requirements should remain reachable from the site's own UI.

## Existing Code Alignment

- `Buildable` already compares each asset's required resources with its Construction Site inventory and derives construction progress from delivered materials.
- `CelestialAssetStore` already represents incomplete assets with `CONSTRUCTION_SITE` status.
- Current action eligibility checks celestial station support and relevant integration availability; no general GTNH player-tier state was found.

## Consequences

- An empty context menu is a content-completeness failure, not an acceptable destination category.
- Object type and authored celestial parameters should become reusable sources of gameplay rules across destinations.
- Dimension ownership and Star Map Actionability remain independent: an object can be actionable without being physically visitable.
- Destination review must validate both a Gameplay Representation and at least one object-native action.

## Remaining Fog

- Decide whether clicking the `?` information control also opens or pins a persistent detail view for material lists that are too large for a transient hover widget.
- Define the exact contents and layout of the information hover widget beyond the required material list.
- Decide whether construction requirements remain visible on the Construction Site after creation; this is currently expected but not yet a finalized UI contract.
- Whether advisory progression labels such as `LuV-tier materials` are manually authored or derived from another authoritative source.
- Which reusable object-property rules belong in Alpha and which object-specific mechanics may remain later depth.
- The exact action set for stars and other extreme celestial objects.

## Related Topics

- Define Celestial Object and Gameplay Space Mapping
- Define Galacticraft-Equivalent Destination Backfill
- Define Tier Destination Portfolio
- Galaxia Alpha Charting Notes
- CONTEXT
- Galaxia Alpha Wayfinder
