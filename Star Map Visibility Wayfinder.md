---
type: wayfinder-map
status: active
tags:
  - galaxia/alpha
  - wayfinder/map
---

# Star Map Visibility Wayfinder

## Destination

Define one deterministic visibility policy that keeps dense systems readable across zoom levels while preserving physical-size relationships, stable selection and cross-system consistency. The renderer consumes resolved size and visibility rather than applying independent heuristics.

## Accepted Contract

- Every Star Map Object has a physical radius in kilometres, authored for registered objects and deterministic for dynamic objects
- One global, order-preserving compressed size curve applies across stellar systems. It is not normalized per parent or sibling set, and discovery must not change the scale
- Dynamic asteroids participate in that same model and calibration population
- Each object passes continuously through natural close-zoom size, reduction to a readable minimum, a minimum-size plateau, then final shrink and fade towards occlusion
- The curve compresses the asteroid-to-star range without reversing physical size order or letting large bodies dominate. Comparable bodies remain visibly distinct
- Collisions use final screen positions and icon radii. Collision culling is independent of the size lifecycle and may happen before the plateau. Orbital perigee, authored sprite size and arbitrary world separation are not culling inputs
- The selected object never fades out or collision-culls. It remains interactive and renders above conflicting bodies
- A star is never culled in its own system view. In galaxy view it may be culled only by another star
- A parent's informational `+n` counts only immediate children hidden by collision with that parent. Offscreen objects, layer-transition disappearance and non-collision fading do not count
- The `+n` control is not interactive and never changes selection or camera state
- Galaxy departure follows the same screen-space parent relationship, not a separate arbitrary culling mode
- [[Define Star Map Overlap Priority]] owns ordinary non-parent collisions, with selected-object and star protections taking precedence

## Open Decisions

- Choose the global curve and stable calibration range, including dynamic asteroid participation without visual jumps
- Define deterministic kilometre radii for generated asteroid size classes and authored exceptions
- Define the parent-clearance fade function and transition from plateau to invisibility
- Define labels, hitboxes and markers during fade and selected-object overlap
- Populate authoritative kilometre radii for registered bodies and remove rendering dependence on authored sprite sizes

These are unresolved design questions, not an approved implementation sequence.

## Dated Integration Evidence

Source inspection on 2026-09-12 found Earth-relative physical radii unused by rendering, authored major-body sprite sizes, perigee-based major-body culling and separate asteroid sizing and decluttering. It was not runtime visual verification.

That inspection also found transfer-planning code deriving minimum periapsis from `star.spriteSize() * 0.5` in `InterplanetaryTransferSystem`. Removing rendering's sprite-size dependency must not silently change transfer behavior. Recheck that coupling before implementation. Transfer redesign is outside this effort.

## Out Of Scope

Orbital mechanics, transfer planning, discovery, ore data, gameplay progression, interactive `+n` controls and compatibility handling for the replaced pre-release rendering model.
