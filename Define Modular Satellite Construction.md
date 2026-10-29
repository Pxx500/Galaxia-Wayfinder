---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
secondary_areas:
  - Area - Alpha Scope
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
  - wayfinder/deferred
---

# Modular Satellite Construction

## Question

When sufficient satellite services exist, how should players construct useful specialized satellites from components without multiplying fixed item variants or creating only the illusion of choice?

## Current Scope Decision

The owner deferred modular satellite design and implementation on 2026-10-17. Alpha currently uses one basic Communication Satellite type and one basic Prospecting Satellite type, not a limit of one deployed instance of each. The separate Primitive Telescope opening mission remains unchanged.

Do not implement the proposed Satellite Assembler, configurable chassis, tiered Satellite Modules or mutual support effects now. They are not prerequisites for the basic satellite recipes or the lunar production chain. Revisit the topic closer to the end of Alpha if useful consumers and data processing justify it. This is a review opportunity, not a commitment to include modular satellites before Alpha ends.

The reason is content readiness. Communication and prospecting still need useful end-to-end gameplay, including processing and consumption of data. A large configurable construction system should follow those services rather than precede them. This deferral does not by itself cancel the existing prospecting-data or Data Processor decisions.

## Retained Future Direction

- A dedicated Satellite Assembler could combine a chassis with chosen modules or parts and support repeat production of a saved design.
- Several chassis tiers could provide different slot counts. Module tiers and interactions should create different useful designs at comparable progression and total cost, not only sequential numerical upgrades.
- Local component synergies and support between satellites on the same orbit are desirable directions. The owner's illustrative resonator bonus of 1% is not selected tuning.
- RF Resonator and Laser Crystal remain candidate component concepts. Their exact recipes and modular-satellite consumers are not Alpha commitments.
- Proposed compression, onboard processing, complementary sensors, observatory and landing-guidance effects were not accepted. Each needs a real consumer and a coherent operational lifecycle before reconsideration.

## Lifecycle Constraint For Reconsideration

[[Define Satellite Manufacturing and Deployment Progression]] owns the accepted lifecycle: deployed functional satellites cannot be returned, recovered or refitted. They remain on their orbit indefinitely until deprecated. Deprecation removes their gameplay contributions without returning hardware. Do not reintroduce a retrieval or servicing workflow as an assumed solution.

Future module choices must work within that lifecycle, including finite observation tasks, obsolete equipment and loss of supporting satellites. Support effects need explicit beneficiaries and stacking. Existing origin-bound data and network contracts remain the starting point, not an invitation to add parallel systems.

## Revisit Questions

- Which actual services give several same-stage configurations useful roles?
- Which parts directly provide capabilities and which manufacture functional modules?
- What constraints, interactions and stacking rules produce meaningful specialization?
- How are designs manufactured repeatedly and preserved through deployment?
- How does the chosen model fit the existing satellite asset, network and data owners?

## Ownership

[[Design Early Orbital Production Recipe Chain]] owns current basic satellite and orbital-material recipes. [[Design Lunar Crater Processing Recipe Chain]] owns Sc supply and candidate components. [[Define Satellite Manufacturing and Deployment Progression]] owns functional-satellite lifecycle and the opening boundary. [[Define Prospecting Data Processing]] owns the sustained origin-bound data pipeline.

## Gameplay Flow

For the current Alpha scope, players deploy basic Communication and Prospecting Satellites, with no limit of one instance of each. Deployed functional satellites remain in orbit until deprecated and cannot be recovered or refitted. Modular construction is deferred, so no component-selection workflow is yet promised.
