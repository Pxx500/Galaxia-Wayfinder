---
type: wayfinder-ticket
ticket_type: research
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Progression]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/research
---

# Verify GTNH Ore Tier Gates

## Question

Which highlighted first-occurrence ores and exceptional alternate sources in Ore Tiers 1–10 are actual GTNH progression requirements, and what exact technology-tier entry and exit gates do they support according to authoritative progression sources?

## Research Progress

- [x] Verify the ordinary early route, Overworld to Moon to Mars, against version-pinned quest and recipe sources. Exhaustive alternate-route and runtime validation are outside this completed slice.
- [x] Separate material requirements, convenient ore access, and processing prerequisites for the early route. Later tiers remain open.
- [x] Identify the applicable source version and mark any evidence from a different version explicitly.
- [ ] Cover later Ore Tiers 4 through 10 before claiming this whole ticket resolved.

The early-route investigation began on 2026-09-10. The existing ore-placement baseline uses Ore Sheet 2.8.0. Current development sources must not silently replace that baseline. Partial research can support a concrete route discussion without certifying all ten Ore Tiers.

## Reviewed Early-Route Findings

[[Early GTNH Progression Gate Research]] provides the bounded, version-pinned evidence and its limitations.

- Titanium feedstock and processing are the ordinary Moon-to-EV outcome. Bauxite and ilmenite are alternative feedstock routes, not two individually mandatory vein visits.
- Lunar meteoric iron contributes to Tier 2 Rocket plating. Small ore and fallen surface meteors provide documented acquisition routes.
- Pre-Mars tungstensteel is needed by the plating recipe, but this does not require Mars tungsten ore. The source quests describe earlier bootstrap sources.
- Some highlighted lunar veins improve supply rather than establishing first access to their constituent materials.
- The original Galacticraft route also includes a Tier 2 schematic and a Rocket-tier destination check. Galaxia's accepted boss-free progression and capability-based travel explicitly replace those mechanisms, rather than inheriting them from the source.

This distinguishes source evidence from target design. It does not assign final Galaxia recipes, treat every lunar resource as exclusive, or certify later Ore Tiers.

On 2026-09-11 research continued with the next bounded slice, Mars to Galacticraft Asteroids and its immediate material/technology gates.

## Reviewed Mars-to-Asteroids Findings

[[Mars to Asteroids Progression Gate Research]] supplies the next bounded slice, reviewed on 2026-09-11.

- Original Tier 3 Rocket hull production consumes desh and platinum and requires IV manufacturing. Electronics add a separate IV cleanroom requirement. These are source facts, not approval to add platinum to Galaxia's selected blueprint materials.
- Phobos is a documented ore alternative to Mars. Deimos is optional in the cited guidance.
- Initial usable naquadah can come from inefficient oxide-mixture smelting. Full later processing is not required for the first product. Ceres offers a documented same-Ore-Tier source alternative.
- A naquadah-doped boule is a verified consumer, not proof of a universal LuV gate. LuV also depends on rhodium-plated palladium and Assembly Line components.
- Original dungeon schematics and Rocket-tier destination checks remain provenance only. Galaxia replaces these with its accepted knowledge and capability rules.

The full Ore Tier 4 resource audit remains unresolved. No final Galaxia material-to-technology assignment follows automatically from this evidence.

## Reviewed Inner-Planet Findings

[[Inner Planets Progression Gate Research]] records the corrected bounded Ore Tier 5 investigation.

- Original Tier 4 hull production combines an IV ice-composite recipe with LuV-rated Assembly Line manufacturing. Its IV electronics do not make the complete chain IV-only. Minimum hatch arrangements remain unverified.
- The original composite consumes compressed Callisto ice, compressed Ledox, and IC2 coolant. Using Callisto ice as engine coolant is a separate accepted Galaxia direction.
- Mercury provides a documented Deep Iron to trinium route connected to naquadah alloy and fusion infrastructure. Universal source exclusivity is not proven.
- Ceres supplies quantium before Venus. Io's samarium is also not demonstrated to be first access. Destination ore highlights must not automatically become mandatory visits.
- Initial europium has a documented fusion route and is consumed by the next Rocket hull. That hull has a ZPM-rated recipe, while its computer recipe is LuV-rated.
- Boss schematics, fixed Rocket destination tiers, exact old hull recipes, and fuel-grade whitelists remain original GTNH provenance, not automatic Galaxia requirements.

Full alternative-source and resource-role audits remain incomplete. The later source-collection round below covers Ore Tiers 6 through 10, but its evidence still needs classification and targeted gap checks. This ticket remains open.

## Current Research Round

On 2026-09-16, research resumed for the remaining outer-system and extrasolar groups at the same GTNH 2.8.0 baseline. The bounded goal is to identify source-backed entry requirements, progression-bearing resources and their concrete downstream consumers. Research does not select Galaxia recipes or certify exhaustive alternative-source coverage.

The bounded pass completed and deposited two source notes in Sources for later Wayfinder classification: Outer System Progression Gate Research and Extrasolar Progression Gate Research. Their intake status does not resolve this ticket. Remaining work includes classification of the evidence and narrowing unresolved resource-role and alternate-source gaps, not repeating the completed source collection.

## Pinned Research Baseline

The release manifest at [DreamAssemblerXXL, GTNH 2.8.0](https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/035dc34a6199b51114cc142ccc7937e1c6872235/releases/manifests/2.8.0.json) pins the applicable component versions. The local release tags were resolved on 2026-09-10 without changing any checkout.

| Source | Version | Commit |
| --- | --- | --- |
| GT-New-Horizons-Modpack quests and configuration | 2.8.0 | c3ba07ccba1b772777f6fc57e53bb70c8547adb7 |
| GT5-Unofficial | 5.09.51.470 | 000a4d9b24d77f40a79da7a105bb79ac7efca817 |
| NewHorizonsCoreMod | 2.7.260 | fe1a49ae577fee5ec4c1cf53d2545b475fb6b5af |
| Galacticraft | 3.3.12-GTNH | e3026156e3c8f626d409bba17fd927b447cb50aa |
| Galaxy-Space-GTNH | 1.1.121-GTNH | 2a7b220dec76560ef0af109c4b6cb53c8470c3fa |

Current local repository heads are newer and are not evidence of the 2.8.0 release behavior. Mod version numbers are not pack version numbers. Future changes to the research baseline must be explicit.
