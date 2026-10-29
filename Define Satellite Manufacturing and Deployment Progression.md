---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
secondary_areas:
  - Area - Travel and Logistics
  - Area - Alpha Scope
blocked_by: []
claimed_by: null
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Satellite Manufacturing And Deployment

The Primitive Telescope Satellite is a limited scripted opening payload made from starting-world materials. Functional satellites follow orbital-material production. Rocket automation comes from upgraded electronics, not a new inherent reusability class. This accepted design does not certify implemented satellite or achievement progression.

## Galaxia Achievement Ownership And Sharing

Galaxia uses its own achievement system. Achievements belong to teams, not individual players, and are distinct from Minecraft's personal achievements.

Only designated special scripted achievements are copied when a member changes teams. The previous team retains the achievement and its benefits, while the receiving team gains them. Ordinary achievements are not copied. Technology Knowledge, blueprints and all celestial knowledge do not automatically transfer.

## Opening Achievement And Survey

- Successful Overworld-orbit deployment grants the persistent launch achievement to the team. Its members share the team achievement regardless of whether they are online. Building the item or starting launch does not count.
- The achievement unlocks the team's Star Map and provides passive progress toward Luna's celestial resource/profile knowledge. The achievement is granted before the scan finishes. Initially only Overworld resources are known. Luna is already known as an object.
- This is planetary knowledge, not scanning physical blocks, generated terrain or Minecraft ore deposits.
- The opening achievement is a special scripted achievement copied on a member's team change. Both teams retain its benefits. Known results are not erased and completed surveys do not restart.
- The payload remains an item and launch objective. It requires no registered orbital asset, ordinary satellite worker or managed satellite lifecycle.

### Accepted Survey Timing And Partial Progress Sharing

The passive Luna profile survey takes a configurable 15 minutes of active server simulation by default. It advances while the server is running even when no players are online. Time while the server is stopped does not advance it. Map access is immediate after deployment, and completed Luna profiling is not an additional permission gate on travel to Luna.

When the opening achievement copies between teams, preserve the greater compatible Luna survey progress of source and destination, without summing elapsed work. The source retains its progress. Completed profile knowledge is never downgraded or restarted. For example, eight minutes of compatible source progress and two at the destination leave the destination at eight, not ten.

[[Specify Alpha Opening Mission Flow]] owns local pre-map launch, authored starting visibility and recovery. [[Define Alpha Celestial Knowledge Layers]] owns general disclosure.

## Functional Satellites And Rocket Control

### Current Alpha Scope And Lifecycle

Alpha uses one basic Communication Satellite type and one basic Prospecting Satellite type, with no limit of one deployed satellite per role. [[Design Early Orbital Production Recipe Chain]] owns their baseline recipes. The opening payload is separate.

Functional satellites remain in orbit indefinitely and cannot be returned, recovered or refitted. A team can deprecate one, removing its contributions without returning the item, modules or materials. There is no lifetime expiry, servicing or recovery mission in this lifecycle.

Modular construction, tiered chassis and modules, a Satellite Assembler and mutual satellite bonuses are deferred in [[Define Modular Satellite Construction]]. They can be reconsidered closer to the end of Alpha once actual services, data processing and consumers justify them, but are not promised Alpha content.

Both SiGe crystal and specialty fluoride optical-fiber chains are required in Alpha. Their selected production operations require Microgravity, not an orbit-specific location flag. Final satellite assembly may happen on a planet or elsewhere.

[[Define Alpha Research and Production Floor]] records the accepted early low-yield sphalerite-to-germanium route supporting SiGe. The existing ABS route remains better later.

Upgraded orbital-material electronics add automatic flight/control to the existing Rocket. Manual Luna travel remains possible without that upgrade. Rockets can deploy from a surface or carry satellites to another body's orbit.

[[Design Early Orbital Production Recipe Chain]] owns the selected payload name, materials, recipes, technologies and their acceptance/tuning status. Space-Grade Alloy is not part of the current bootstrap and must not become an implicit pre-Luna requirement.

## Hammer Deployment

With a satellite in the payload slot, the Hammer exposes a localized `Deploy to Orbit` checkbox. Enabled deployment targets an orbit and needs no cargo receiver. Disabled, the satellite item remains ordinary cargo and requires a receiver.

[[Define Hammer Satellite Deployment Reach]] owns atmosphere-free surface launch, same-orbit local reach and whole-star-system Big Hammer reach. Ordinary freight retains [[Define Alpha Transport Roles]] endpoint rules. Deployment is a scoped exception, not general receiver-free freight.

## Proposals And Open Tuning

The opener's detailed presentation remains content work. Unapproved elaborations include a fixed non-retargetable task without recurring prospecting-bonus data, persistent results without maintenance, and a warning that duplicate launches are unnecessary rather than a global one-item crafting limit.

Numerical Hammer deployment costs and detailed mission accounting remain balance work. Concrete orbital feedstock, processing, payload and electronics recipes live in their recipe owner rather than this note.

## Evidence And Provenance

Existing team knowledge and membership-transfer hooks do not establish the Galaxia achievement system or the scripted Luna survey. Keep team achievement records and celestial knowledge as distinct domain responsibilities, not a fake satellite or scattered flags.

Owner clarification on 2026-10-17 establishes Galaxia's own team-owned achievements and limits copying on team changes to designated special scripted achievements, including the opener. This supersedes the earlier personal-achievement wording. The 2026-09-17 discussion establishes the scripted opener, optional pre-Luna automation and both orbital chains. The 2026-10-07 answers resolve Hammer deployment origin/reach. Later recipe decisions name Primitive Telescope Satellite.

## Gameplay Flow

Players build the Primitive Telescope Satellite from starting-world materials and deploy it to Overworld orbit. Successful deployment immediately unlocks the team's Star Map and starts the passive Luna profile survey. The survey advances during active server time, including when players are offline, but is not a prerequisite for travel to Luna.

Later, players produce SiGe and fluoride materials in microgravity to build functional Communication and Prospecting Satellites. An upgraded controller adds automatic flight to the existing Rocket, while manual Luna travel remains possible without it. Functional satellites remain in orbit until deprecated, with no recovery or servicing. A Hammer can deploy a payload without a receiver when its deployment option is selected and the route meets the separate reach rules.
