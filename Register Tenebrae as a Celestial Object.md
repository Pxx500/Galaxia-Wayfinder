---
type: wayfinder-ticket
ticket_type: task
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Destinations]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/task
---

# Register Tenebrae as a Celestial Object

## Question

What minimal authored registration keeps the existing Tenebrae content visible in the Vael system on the Star Map without pretending that its incomplete dimension, hazards, world generation, or gameplay contract already exist?

## Established Input

- Add `CelestialObjectId.TENEBRAE` associated with the existing `DimensionEnum.TENEBRAE`.
- Register Tenebrae as a Planet under `CelestialObjectId.VAEL`.
- Use the existing `EnumTextures.ICON_TENEBRAE` Star Map icon and existing Tenebrae localization name.
- Do not add a `PlayableDimensionProfile`, world provider, hazards, gravity, atmosphere, ores, features, station eligibility, outpost eligibility, or sky rendering in this change.
- A Celestial Object may own `DimensionEnum.TENEBRAE` without a playable profile. It appears in the registry and Star Map but the dimension is not registered as playable.
- Every dimension declared by Galaxia must resolve to one registered Celestial Object, whether or not it is playable yet.
- Existing Tenebrae sky and environment artwork is owned by another contributor and remains untouched.

## Resolution

Tenebrae is a registered non-playable Planet under Vael. It uses the existing Tenebrae icon and localization, with temporary Star Map presentation values of `1.20` orbit radius, `0.00016` orbital speed, and `0.20` sprite size.

Every `DimensionEnum` declared by Galaxia must resolve through the Celestial Registry. This is a registry-wide contract rather than a Tenebrae-specific exception.

Tenebrae has no playable profile, environment contract, hazards, resources, capabilities, world generation, or sky rendering yet. The temporary presentation values do not claim physical or gameplay meaning.

## Related Topics

- [[Define Celestial Capability Rules]]
- [[Area - Destinations]]
