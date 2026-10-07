---
type: wayfinder-map
status: active
tags:
  - galaxia/alpha
  - wayfinder/map
---

# Star Map Visibility Wayfinder

## Destination

Define a single, deterministic visibility model for the Star Map. It must make dense stellar systems readable at every zoom level while preserving physical size relationships, stable player selection, and consistent presentation across all star systems.

## Goal

Replace the current collection of sprite-size constants and orbital-distance culling heuristics with one visibility policy. The policy decides an object's screen radius, alpha, collision eligibility, culling result, and parent hidden-object count from the current scene.

## Problem Summary

The current Star Map has no coherent visibility contract. Major bodies use author-chosen sprite sizes, while asteroids use a separate relative-zoom rule. Major-body culling compares orbital perigee with icon radii instead of testing actual rendered overlap. This produces inconsistent apparent body sizes and abrupt disappearances while leaving no explanation of what was hidden.

The existing physical-radius field is Earth-relative, is only populated for a small subset of bodies, and is not used by Star Map rendering. Dynamic asteroids also use separate size classes rather than the same physical presentation model.

## Decisions So Far

1. Every Star Map Object has a physical radius expressed in kilometres. The radius is authored data for registered objects and deterministic generated data for dynamic objects.

2. All objects use one global size-normalisation model across every stellar system. The model is global to preserve cross-system consistency; it is not normalised per parent or sibling set, and player discovery must never change the scale.

3. Dynamic asteroids participate in the same visibility system and the global normalisation population. They cannot be excluded merely because they are generated at runtime.

4. The size model has four continuous phases per object:
   - natural physical size at close zoom;
   - reduction toward a minimum readable screen size;
   - a plateau at that minimum readable size;
   - final shrink and fade as the object approaches an occlusion state.

5. The global radius curve must preserve the ordering of physical sizes while compressing the enormous range between asteroid, moon, planet, gas giant, and star. It must keep comparable bodies visibly distinct without allowing large objects to dominate the map.

6. Collision and culling are screen-space decisions made after final positions and final icon radii are known. Collision culling can occur before an object reaches its plateau; it is independent from the size lifecycle. Orbital perigee, authored sprite size, and arbitrary world-space separation are not valid culling inputs.

7. An object selected by the player is excluded from both fade-out and collision culling. It remains interactive and is rendered above conflicting bodies.

8. A star is never culled in its own stellar-system view. In the galaxy view, a star may be culled only by collision with another star.

9. A parent displays an informational `+n` count for immediate children hidden by collision with that parent. A planet's count represents hidden moons or comparable direct children. A star's count represents only direct children currently colliding with that star.

10. The `+n` count is not interactive. It does not zoom, select, expand, or otherwise alter the camera.

11. Objects outside the viewport do not contribute to any `+n` count. Intentional layer-transition disappearance and non-collision fading also do not contribute to the count.

12. The galaxy transition is not a separate arbitrary culling mode. As the camera recedes, each object's visibility resolves through its own screen-space relationship to its parent and the current scene.

13. [[Define Star Map Overlap Priority]] resolves ordinary non-parent overlaps in favor of the physically larger body. Existing selected-object and star protections retain precedence.

## Target Visibility Resolution

For every renderable object, resolve the following in order:

1. Obtain its physical radius in kilometres.
2. Map that radius through the global, order-preserving compressed size curve.
3. Apply the current zoom to obtain the natural screen radius.
4. Clamp smoothly into the object's readable-size plateau.
5. Use final screen bounds to resolve collisions and available clearance to the parent.
6. Apply final fade or culling, except for a selected object.
7. Record collision-culling against the direct parent for the parent's informational count.

The renderer consumes the resolved state rather than independently recalculating size and visibility in separate code paths.

## Current Code Baseline

Source inspection on 2026-09-12 reconfirmed authored sprite sizing, separate asteroid sizing, Earth-relative body radii, and perigee-based culling. The remaining historical selection and indicator observations below were not fully retraced and remain checks for implementation. This is not runtime visual verification.

- Physical body radius exists as `radiusEarthRelative`, not kilometres. It is domain data for dimension materialisation and is not read by the Star Map renderer.
- Major bodies use `spriteSize` and a hard-coded map-radius formula with a two-pixel minimum.
- Major-body culling compares scaled orbital perigee against parent and child icon radii plus a fixed margin.
- Asteroids have a separate relative-zoom sizing rule and the only current screen-space declutter pass.
- During the current system-to-galaxy departure, continued zoom-out makes planets converge with their parent star until the old culling heuristic removes them abruptly.
- The focused body bypasses part of the old culling logic, but selection is not a complete visibility exemption for asteroid declutter.
- No `+n` hidden-child indicator exists.

## Verified Integration Dependency

Current anchors under `src/main/java/com/gtnewhorizons/galaxia/`: `client/gui/orbitalGUI/OrbitalView.java:1408`, `:1423`, and `:2286`, and `registry/celestial/CelestialBodyProperties.java:21`.

An important integration dependency was also found: `client/gui/orbitalGUI/InterplanetaryTransferSystem.java:384` and `:452` derive minimum periapsis from `star.spriteSize() * 0.5`. Removing rendering's sprite-size dependency must not silently change transfer behavior. Transfer redesign remains outside this visibility effort.

## Open Design Questions

- Define the global compression curve and its stable calibration range, including how dynamic asteroid population participates without causing visual jumps.
- Define deterministic kilometre-radius generation for each dynamic asteroid size class and any authored exceptional asteroid.
- Define the exact fade function based on parent clearance, including the transition from plateau to zero visibility.
- [[Define Star Map Overlap Priority]] owns non-parent collision priority, preserving the already accepted selected-object override and star protection.
- Define labels, hitboxes, and markers during fade and while a selected object overlaps another body.
- Populate authoritative kilometre radii for all registered celestial objects and remove the renderer's dependence on authored sprite-size values.

## Out Of Scope

- Changing orbital mechanics, transfer planning, discovery rules, ore data, or gameplay progression.
- Making the `+n` indicator interactive.
- Compatibility handling for the present pre-release sprite-size rendering model after the new visibility policy replaces it.
