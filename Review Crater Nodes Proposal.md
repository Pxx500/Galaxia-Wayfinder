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

# Review Crater Nodes Proposal

## Resolution

Crater extraction is an Alpha gameplay chain. One extractor uses a shared finite deposit, then unlimited fracking with progressively increasing fluid cost. Normal GT processing separates enriched fluid and recovers its carrier. Existing GT scanners and map integration expose deposit information. Space-Grade Alloy is one atmosphere-free bulk construction material, not a technology-tier gate.

This resolves the gameplay proposal, not implementation or numerical balance. [[Design Lunar Crater Processing Recipe Chain]] owns the current lunar profiles, recipes, occurrence weights, reserves, fracking slopes and remaining content proposals. The original Discord proposal remains provenance under [[Sources]], not an additional set of accepted requirements.

## Extraction Contract

- One crater-extraction machine has ordinary-mining and fracking modes. A dedicated controller recipe is provisionally accepted, but an existing modpack multiblock miner may host the behavior instead. Final machine choice, name and geometry remain open
- Ordinary mining consumes the crater's finite initial reserve. Fracking is available only after exhaustion and requires fluid. Supplying fluid early does not bypass that transition
- All four selected lunar profiles support wet ordinary mining from the beginning, or dry ordinary mining with lower resource efficiency. Both consume the same reserve. The recipe-chain ticket owns the accepted outputs and 25% chance of double reserve consumption during dry mining
- After exhaustion, fracking can continue indefinitely. Enriched output per operation stays fixed while input increases with shared fracking history. Additional input does not increase mineral output
- Initial carrier recovery is approximately closed. Progressive use creates increasing replacement demand. The accepted working lunar tuning starts perfectly closed and uses profile-dependent linear growth
- Existing GT Drilling Fluid is the provisional carrier. Its ordinary GT manufacture remains the supply route. Downstream separation and recovery use ordinary GT machines and recipe maps
- Any number of extractors can share one crater. More machines increase throughput and advance the same history, not independent reserves or cheap starts. Practical limits are space, equipment, energy, processing and logistics
- The general deposit system is not limited to the current lunar profiles. Titanium may occur in craters but retains its separate GTNH processing chain

## Deposit Identity And Shared Accounting

Each world-generated crater owns one Crater Deposit even across chunk boundaries. Membership uses the geometric footprint, not a biome or chunk ownership. A chunk index narrows spatial lookup to candidate craters, followed by exact containment. An extractor resolves and persistently remembers its Crater ID when binding. Routine extraction does not repeat that lookup.

The deposit is the single authority for finite reserve and fracking history. Ordinary mining permanently claims its portion at operation start. Fracking claims the next shared cost position at operation start. The next extractor sees the updated state before completion, so concurrent work cannot reuse a cheaper position.

The started operation records its claimed batch, cost and progress. Power loss or chunk unloading pauses it. Resumption never claims again, and completion never debits a second time. Destroying or explicitly discarding the operation loses its already claimed portion and consumed inputs. This bounded loss is accepted. It requires no particular locking mechanism or persistence layout.

## Generation And Richness Model

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

Crater-specific resources need real progression uses, but this does not make SGA itself a tier gate or force a fixed crater itinerary. SGA is one canonical GT5 material with normal metal forms and generated processing. Feedstock composition changes equivalent construction output, not material identity or grade. Full dusts are the selected granularity wherever the lunar chain uses dust.

SGA manufacture, material processing and recycling require No Atmosphere, without a gravity requirement. An artificial vacuum chamber on an atmospheric world does not satisfy that environment rule. Different alloy routes produce the same material without origin metadata. Ordinary space recipes still need their appropriate progression materials and need not all consume SGA.

## Scanner Contract

Reuse existing GT ore scanners and extend their prospecting/minimap integration rather than adding a Galaxia scanner machine.

- Scan from inside the crater's geometric footprint. The visible terrain feature lets players locate it before scanning
- Show deposit composition, remaining ordinary reserve, fracking state and current fluid input per operation
- Existing scanner/map integration owns record storage and refresh behavior. A scan-time-only snapshot policy is not selected
- Scanning is not an accepted prerequisite for extraction

## Remaining Integration And Content Questions

- Existing scanner/map data ownership and the extension needed to display crater state
- Registered-fluid matching and subtype-specific NEI integration
- Diameter standard deviations, spatial density and richness-response tuning
- Unfinished recipes, extractor geometry and whole-chain balance in [[Design Lunar Crater Processing Recipe Chain]]
