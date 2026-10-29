---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
secondary_areas:
  - Area - Destinations
source_file: "Discord Source - Crater Nodes Proposal.md"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Crater Extraction

Crater extraction is an Alpha gameplay chain. Extractors use a shared finite deposit, then unlimited fracking with progressively increasing fluid cost. Normal GT processing separates enriched fluid and recovers its carrier. Existing GT scanners and map integration expose deposit information. Space-Grade Alloy is one atmosphere-free bulk construction material, not a technology-tier gate.

This establishes the gameplay direction, not implementation or numerical balance. [[Design Lunar Crater Processing Recipe Chain]] owns lunar profiles, recipes, occurrence weights, reserves, fracking slopes and remaining content proposals. The original proposal remains provenance under [[Sources]], not an additional set of accepted requirements.

## Extraction Contract

- A dedicated Crater Extractor has ordinary-mining and fracking modes. Its separate machine identity was selected on 2026-10-23. Reuse suitable GT multiblock, hatch and energy infrastructure without changing existing miners. Geometry and integration remain open
- Ordinary mining consumes the crater's finite initial reserve. Fracking is available only after exhaustion and requires fluid. Supplying fluid early does not bypass that transition
- All four selected lunar profiles support wet ordinary mining from the beginning, or dry ordinary mining with lower resource efficiency. Both consume the same reserve. The recipe-chain ticket owns the accepted outputs and 25% chance of double reserve consumption during dry mining
- After exhaustion, fracking can continue indefinitely. Enriched output per operation stays fixed while input increases with shared fracking history. Additional input does not increase mineral output
- Initial carrier recovery is approximately closed. Progressive use creates increasing replacement demand. The accepted working lunar tuning starts perfectly closed and uses profile-dependent linear growth
- Existing GT Drilling Fluid is the provisional carrier. Its ordinary GT manufacture remains the supply route. Downstream separation and recovery use ordinary GT machines and recipe maps
- Any number of extractors can share one crater. More machines increase throughput and advance the same history. Space, equipment, energy, processing and logistics are the practical limits
- The general deposit system is not limited to the current lunar profiles. Titanium may occur in craters but retains its separate GTNH processing chain

## Deposit Identity And Shared Accounting

Each generated crater owns one Crater Deposit across chunk boundaries. Membership follows the geometric footprint, not a biome or chunk. A chunk index narrows lookup to candidate craters, followed by exact containment. On binding, an extractor resolves and persistently remembers its Crater ID. Routine extraction does not repeat that lookup.

The deposit owns finite reserve and fracking history. Ordinary mining consumes reserve only on successful completion. Starting or power-failing work does not deplete it. Concurrent extractors must not produce the same last portion more than once. Temporary reservations and completion-time admission are implementation choices, not separate reserve owners.

Power failure follows GT multiblock behavior: reset the operation, discard pending outputs and do not refund consumed inputs or energy. Save/load and chunk lifecycle follow supported GT behavior, not a simulated power failure on unloading. The 2026-10-23 decision replaced start-time permanent reserve debit and retained work on power loss.

Fracking costs come from shared history. Only successful fracking advances it. Failed work loses consumed inputs but does not increase the next cost. Concurrent pricing and admission must preserve shared accounting without duplicating output, resetting history or counting failed attempts. Reservation and commit mechanics remain open. Completion-only accounting was confirmed on 2026-10-23.

## Generation And Richness Model

Crater terrain should be easy to find and inexpensive to analyze with existing GT prospectors. Switching deposits primarily costs relocation or extension of extraction, power, processing and logistics, not a long search. This does not guarantee every profile near a landing site. Derive density and size distribution from sample terrain and this relocation loop.

Craters use authored Small, Medium and Large size classes. Each destination has class occurrence weights. Each class has a mean diameter and standard deviation, with diameter sampled from its normal distribution. The distributions can overlap, so physical diameter does not uniquely identify or reclassify a crater. Working Moon means are approximately one, three and eight chunks. Standard deviations remain tuning.

Generation selects a size class, samples diameter, then selects a material profile using that class's profile weights. Each profile has independent weights per class. Zero makes it ineligible, while positive weights are proportional. Accepted lunar profile weights are in the recipe-chain ticket. The separate proposed 70/25/5 class mix is not approved.

Finite reserve depends on the originating class's reserve scale, the profile's reserve multiplier and its response to actual diameter relative to that class's mean. The response can amplify, dampen or reverse the size effect. A replaceable working formula is:

```text
baseReserve = sizeClassBaseReserve * materialReserveMultiplier
sizeChange = actualDiameter / classMeanDiameter - 1
richnessMultiplier = 1 + sizeChange * materialSizeResponse
initialReserve = baseReserve * richnessMultiplier * initialVariation
```

Authored values must keep richness positive. A size-derived +50% change with response 0.1 gives +5% richness. The once-only initial variation is approximately 0.9 to 1.1, applied after size/profile adjustment and shared by all extractors. It never rerolls on binding, replacement, scanning or reload. It does not alter composition, operation output or fracking slope. Formula details can change without changing deposit identity or shared ownership.

## Fluid Representation

Enriched fluids form one family with separate registered Fluid IDs for each subtype. Definitions and behavior may be shared. Normal GT recipe matching and NEI must distinguish the variants without NBT-only identity. Verify this integration against the actual dependency versions.

## Progression And Material Role

New primary Galaxia Sc acquisition is crater-exclusive, starting with lunar Sc-bearing bauxite. Enriched fluid yields ordinary Bauxite and Sc-bearing products without a new ore identity. Ordinary bauxite refining is not a general Sc source. The much later existing Blood Magic Chinfinity meteor source remains unchanged. The recipe-chain ticket owns the chemistry and useful consumers.

Crater-specific resources need real progression uses, but this does not make SGA itself a tier gate or force a fixed crater itinerary. SGA is one canonical material with normal GT metal forms. Its selected forming route is melting and casting, not unrestricted default metal conversions. Feedstock composition changes equivalent construction output, not material identity or grade. Full dusts are the selected granularity wherever the lunar chain uses dust.

SGA alloying, melting, casting and material recovery require No Atmosphere, without a gravity requirement. Assembly from finished cast parts does not automatically inherit that restriction. The recipe-chain owner defines permitted forms and disabled direct conversions. An artificial vacuum chamber on an atmospheric world does not satisfy that environment rule. Different alloy routes produce the same material without origin metadata. Ordinary space recipes still need their appropriate progression materials and need not all consume SGA.

## Scanner Contract

Reuse existing GT ore scanners and extend their prospecting/minimap integration rather than adding a Galaxia scanner machine.

- Scan from inside the crater's geometric footprint. The visible terrain feature lets players locate it before scanning
- A normal supported GT prospector scan performed within that footprint also analyzes the crater. No separate expensive survey machine or new Galaxia scanner item is required
- Show deposit composition, remaining ordinary reserve, fracking state and current fluid input per operation
- Existing scanner/map integration owns record storage and refresh behavior. A scan-time-only snapshot policy is not selected
- Scanning is not an accepted prerequisite for extraction

### Prospector Feedback

The short chat result shows the crater's natural name, remaining reserve and next fracking operation on separate lines, without final periods. Omit size, diameter and completed-operation count from this short result.

### NEI Overview

Provide a Crater Extractor recipe map so looking up enriched fluid shows which extractor operation produces it. Prefer graphical or mechanical presentation over prose labels for wet extraction, reserve requirements and depletion.

A combined overview of dry mining, wet mining, depletion, fracking and downstream recovery is a proposed layout direction. Exact artwork, dimensions and arrangement remain open.

Source: lunar extraction feedback, 2026-10-28 to 2026-10-29.

## Open Integration And Content Questions

- Existing scanner/map data ownership and the extension needed to display crater state
- Registered-fluid matching and subtype-specific NEI integration
- Diameter standard deviations, spatial density and richness-response tuning
- Unfinished recipes, extractor geometry and whole-chain balance in [[Design Lunar Crater Processing Recipe Chain]]

## Gameplay Flow

Players find visible crater terrain and can use an existing GT prospector inside its footprint to inspect the deposit. Scanning is optional. A dedicated extractor mines the shared finite reserve, with wet mining preserving more of it than dry mining. Additional extractors increase throughput but draw from the same deposit.

After the reserve is exhausted, fracking continues with a fixed enriched-fluid output and increasing Drilling Fluid input. Ordinary GT machinery separates the minerals and recovers carrier, while replacement fluid becomes a growing cost. Players can expand their supply or move equipment to another crater. The recovered materials feed ordinary refining and the lunar Sc and SGA chains.
