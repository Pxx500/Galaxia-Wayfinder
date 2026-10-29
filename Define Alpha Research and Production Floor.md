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

# Alpha Research And Production

Alpha needs research and production chains that connect obtainable materials to useful progression beyond extraction.

## Production Machinery Baseline

Galaxia primarily uses GregTech machines and their normal production capabilities. Check existing machinery before proposing a custom machine, which needs a concrete process requirement those machines cannot satisfy. A new acquisition recipe alone does not imply a new machine.

### Native GT Machine Failure Semantics

When a running GT-like machine loses power, environment, cooling or another required condition, it follows its underlying GT failure lifecycle. Singleblocks and multiblocks retain their actual distinct behavior. There is no custom retained-progress pause, automatic continuation or refund. This general rule was selected on 2026-10-23, replacing retained-work proposals.

Missing inputs or output capacity prevent work from starting. Save/load and chunk unloading retain native behavior and do not simulate power failure. Completed products remain stored. Rocket waiting, android control and time-sliced background calculations are not GT recipe operations and retain their own contracts.

Crater reserve and fracking history advance only on successful extraction under [[Review Crater Nodes Proposal]]. Failed work does not restore consumed inputs.

## Accepted Production Minimum

Alpha requires complete silicon-germanium crystal and specialty fluoride optical-fiber chains, from obtainable feedstock to useful products. Both require Microgravity, not an orbit flag. Current progression places this environment in orbital dimensions, but final satellite assembly need not occur there. [[Define Celestial Capability Rules]] owns environmental eligibility and SGA's separate No Atmosphere requirement.

| Material family | Required allocation |
| --- | --- |
| Silicon-germanium crystals | Electronics for Rockets and satellites, including the first Rocket automation/control upgrade |
| Specialty fluoride optical fibers | Satellite production, not a mandatory ingredient in the first Rocket-control upgrade |

The opening satellite and first Station bootstrap do not require these orbital materials. [[Define First Physical Station Contract]] owns the workshop bootstrap. [[Define Satellite Manufacturing and Deployment Progression]] owns satellite behavior and deployment.

[[Design Early Orbital Production Recipe Chain]] owns the seed cycle, fluoride thermal flow, satellite hardware, solar components and remaining recipe proposals. Space Grade Solar Panel is a recipe-component item only. Placeable generators and EU output are outside that chain's scope, and existing GTNH solar balance stays unchanged.

### Early Germanium Supply

Add a low-yield sphalerite route before the existing IV Alloy Blast Smelter method. HV is the working early target, and inputs, reagents and machinery must fit that stage. The selected early yield is 8 mB, compared with 36 mB from the unchanged ABS route. Preserve a reason to upgrade and check earlier access against unrelated GTNH progression. The existing recipe's tier and consumers do not change.

## Related Settled Contracts

- [[Define Alpha Technology Knowledge Contract]] owns consumed Technology Blueprints, team knowledge, production checks and catalog behavior. Rocket Automation and Functional Satellites are the selected first groups. Later groups and blueprint costs remain content decisions
- [[Define Prospecting Data Processing]] owns origin-bound processing and the return pipeline. [[Define Data Processor Machine Topology]] owns the powered controller multiblock, bounded independently powered/cooled clusters and single-block rack hardware
- Mandatory bosses and dungeons are excluded from progression. Richer planetary experiments are later work, not a prerequisite for the Alpha blueprint mechanism
- [[Review Crater Nodes Proposal]] resolves the crater gameplay chain. [[Design Lunar Crater Processing Recipe Chain]] owns current lunar content and open recipe choices

## Open Decisions

- Which additional destination-dependent chains are essential to Alpha rather than optional depth?
- Which reviewed proposals provide a complete input, player activity, output and progression continuation?
- Which later technologies and recipe groups are needed beyond the two selected initial groups?
- Complete early orbital feedstock and recipe review in its owning ticket, including practical availability and environment enforcement

The broader production floor remains open even though its two-material minimum and technology mechanism are settled. [[Define Alpha Galaxia-Specific Capability Floor]] indexes the proposed complete industrial package. Recipe tuning and implementation evidence remain with their owners.

## Gameplay Flow

Players bootstrap a first workshop without orbital materials, then produce silicon-germanium crystals and specialty fluoride optical fibers in microgravity. The crystals support Rocket and satellite electronics, while the fibers support satellites. Final satellite assembly can take place elsewhere.

Early germanium extraction makes the SiGe chain accessible before the more efficient ABS route. Players can later upgrade for better yield. The production chains use normal GT machinery, and lost operating requirements follow the machine's native failure behavior.
