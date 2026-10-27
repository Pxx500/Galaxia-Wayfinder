---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Observation and Research
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Alpha Research and Production Floor

## Question

Which research, satellite-data, destination-dependent production and other non-extraction chains must appear in Alpha beyond the accepted acquisition and processing contracts?

## Production Machinery Baseline

Galaxia primarily uses GregTech machines and their normal production capabilities. A custom machine needs a concrete process requirement that existing machinery cannot satisfy. Investigate existing capabilities before proposing an exception. A new acquisition recipe does not imply a new machine.

### Native GT Machine Failure Semantics

GT-like machines use the native failure lifecycle of their underlying GT machine when required power, environment, cooling or another running-operation requirement is lost. Do not introduce a custom retained-progress pause, automatic continuation of a failed operation or refund scheme. Preserve the actual distinction between GT singleblock and multiblock behavior instead of imposing one invented cancellation model on both. The owner made this the general rule on 2026-10-23, superseding previous retained-work proposals.

Ordinary checks before starting work remain ordinary checks. Missing recipe inputs or protected output capacity do not create a running operation that must be failed. Native save/load and chunk-unload behavior remain native behavior, not an automatic simulated power failure. Already completed products remain ordinary stored inventory. Rocket waiting, android control and time-sliced background calculations are not GT recipe operations and retain their own contracts.

Domain accounting follows the owning mechanic. Crater reserve and fracking cost history advance only for successful extraction under [[Review Crater Nodes Proposal]]. This does not restore consumed inputs after a failed operation.

## Accepted Production Minimum

Alpha requires complete silicon-germanium crystal and specialty fluoride optical-fiber chains, each from obtainable feedstock to a product with a concrete use. Both require Microgravity, not an orbital-location flag. Current player-facing progression locates that environment in orbital dimensions. Final satellite assembly need not happen in orbit. [[Define Celestial Capability Rules]] owns consistent environmental eligibility and SGA's separate No Atmosphere requirement.

| Material family | Required allocation |
| --- | --- |
| Silicon-germanium crystals | Electronics for Rockets and satellites, including the first Rocket automation/control upgrade |
| Specialty fluoride optical fibers | Satellite production, not a mandatory ingredient in the first Rocket-control upgrade |

The opening satellite and first Station bootstrap do not require these orbital materials. [[Define First Physical Station Contract]] owns the workshop bootstrap. [[Define Satellite Manufacturing and Deployment Progression]] owns satellite behavior and deployment.

[[Design Early Orbital Production Recipe Chain]] owns the seed cycle, fluoride thermal flow, satellite hardware, solar components and remaining recipe proposals. Space Grade Solar Panel is a recipe-component item only. Placeable generators and EU output are outside that chain's scope, and existing GTNH solar balance stays unchanged.

### Early Germanium Supply

Add a low-yield sphalerite route before the existing IV Alloy Blast Smelter method. HV is the working early target. Inputs, reagents and machinery must actually fit that stage. The recipe-chain ticket records the selected 8 mB early yield and its comparison with the unchanged 36 mB ABS route.

Retain a meaningful reason to upgrade to ABS. Earlier access still needs checking against unrelated GTNH progression during implementation. It does not approve lowering the existing recipe's tier or changing its consumers.

## Related Settled Contracts

- [[Define Alpha Technology Knowledge Contract]] owns consumed Technology Blueprints, team knowledge, production checks and catalog behavior. Rocket Automation and Functional Satellites are the selected first groups. Later groups and blueprint costs remain content decisions
- [[Define Prospecting Data Processing]] owns origin-bound processing and the return pipeline. [[Define Data Processor Machine Topology]] owns the powered controller multiblock, bounded independently powered/cooled clusters and single-block rack hardware
- Mandatory bosses and dungeons are excluded from progression. Richer planetary experiments are later work, not a prerequisite for the Alpha blueprint mechanism
- [[Review Crater Nodes Proposal]] resolves the crater gameplay chain. [[Design Lunar Crater Processing Recipe Chain]] owns current lunar content and open recipe choices

## Remaining Decisions

- Which additional destination-dependent chains are essential to Alpha rather than optional depth?
- Which reviewed proposals provide a complete input, player activity, output and progression continuation?
- Which later technologies and recipe groups are needed beyond the two selected initial groups?
- Complete early orbital feedstock and recipe review in its owning ticket, including practical availability and environment enforcement

This broader production-floor ticket remains open even though its two-material minimum and the technology mechanism are settled.

The proposed complete industrial floor is indexed in [[Define Alpha Galaxia-Specific Capability Floor]]. Selecting that package can settle the required chains together. Numerical recipe tuning and implementation evidence remain with their owners rather than becoming additional product-floor questions.
