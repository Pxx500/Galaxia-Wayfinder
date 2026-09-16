---
type: wayfinder-provenance
status: archived
tags:
  - galaxia/alpha
  - wayfinder/provenance
---

# Galaxia Alpha Charting Notes

> Historical or reference record. Read dated outcomes and later corrections before using earlier proposals. This record is not an active instruction to execute its plan, and its code or verification claims have not been revalidated by the 2026-09-10 vault consolidation.

Status: Archived charting provenance

This note preserves the durable state of the initial Wayfinder charting session. Galaxia Alpha Wayfinder is now the canonical map; this file remains provenance and must not be used as the active tracker.

## Destination

Produce Galaxia Alpha: a playable product milestone in which Galaxia acts as GTNH's space-progression hub across the complete Ore Tier 1–10 progression. A player must be able to traverse every Galaxia-controlled tier gate without blockers, continue through the wider GTNH progression, and encounter no orphaned mechanics. Alpha requires a closed playable cycle at every tier, but it does not require the final planned mechanical depth of every destination.

## Confirmed Product Direction

- Galaxia is a progression hub for GregTech New Horizons, not a standalone campaign.
- The main progression spine is linear at the GTNH technology-tier level, while gameplay within each stage may branch and support alternative activities and strategies.
- The repeating product rhythm is a Celestial Progression Cycle: a technology tier enables an off-world mission; completing the mission provides a material, knowledge result, infrastructure capability, or other requirement needed for later GTNH progression.
- The milestone is called Galaxia Alpha. The word prototype remains available for throwaway experiments.
- Galacticraft and its selected addons provide a capability baseline, not a feature-for-feature design specification. Galaxia may satisfy the same player capability through substantially different mechanics, such as modular rather than static rockets.
- Every included mechanic must participate in a complete cause-and-effect gameplay chain. A mechanic with no meaningful input, player decision, consequence, or downstream progression use is an orphaned mechanic.
- Galaxia Alpha covers the complete Ore Tier 1–10 progression. A smaller early-tier subset may be used as an intermediate vertical slice, but it is not Galaxia Alpha.
- Alpha breadth and Alpha depth are separate constraints: every tier must be traversable through a closed gameplay cycle, while advanced research, satellite-data, and production-chain mechanics may be introduced selectively rather than duplicated at every tier.
- Celestial destinations intentionally support different forms and depths of engagement. Major destinations may require persistent infrastructure; some resource destinations may justify short extractive visits; remote destinations may be served by automated assets; and large generated asteroid populations are choice spaces from which the player selects only a useful subset. Galaxia's anti-placeholder goal applies to the destination ecosystem as a whole, not as an identical base-building obligation for every celestial body.
- `Automated` describes an interaction model and ecosystem: the player manages an asset through the Star Map and has no physical access to a player dimension for that asset. `Automated Outpost` and `Automated Station` are distinct placements within that ecosystem, not interchangeable names.
- Automated asset eligibility and capability derive from celestial and orbital parameters. An outpost is anchored to a body or surface and may support mining while inheriting local conditions such as a day-night cycle. A station occupies an eligible orbit, cannot mine the underlying body, and may receive orbital advantages such as continuous or improved solar generation.
- Spaceships and rockets are distinct transport classes. Spaceships may connect endpoints that do not require escaping an atmosphere or a significant gravity well, such as an asteroid outpost and a planetary orbital station. They cannot provide a surface-to-orbit link from a planetary outpost. Rockets provide the higher-acceleration surface-to-space capability.
- Interplanetary movement must not be bypassed through player, item, or fluid teleportation. Players must maintain explicit transport infrastructure at its endpoints and move through Galaxia's travel and logistics systems, including rockets and Hammer electromagnetic cannons.
- Exact claims about GTNH items, recipes, machines, materials, and technology tiers require an authoritative source. They must not be invented from incomplete Galaxia-repository context.
- All Obsidian vault content is written in English for direct sharing with the development team.

## Source Material

- [Galaxia gameplay concept map](file:///C:/Users/Pxx500/Documents/GitHub/Galaxia/docs/architecture/galaxia-concept-map.drawio) — a 37-page gameplay-first atlas containing nine domains and 36 detailed concepts. It mixes implemented foundations, planned direction, gameplay descriptions, and unresolved gaps; it is source material rather than a Wayfinder map.
- [Concept-map discussion](codex://threads/019f89d3-71d2-7c02-9b25-7c034707e20f) — the conversation that produced and refined the Draw.io artifact.
- [GTNH Spreadsheet](https://docs.google.com/spreadsheets/d/1EIZtJU5eBbnUlrg7fD_ZyIzsr9sn4l4no9ek6M_iSVM/edit?gid=955235406#gid=955235406) — developer-maintained pack data. The `Ore Sheet (2.8.0)` tab is the authoritative starting source for current ore availability and destination tier grouping.
- GTNH Ore Progression Baseline — extracted source semantics and verified examples from the Ore Sheet.
- CONTEXT — the authoritative working Galaxia domain glossary, stored in the Vault rather than the repository checkout.

## Accepted Charting Decisions

- Ore compatibility preserves progression-critical earliest-access Ore Tiers and meaningful route exceptions rather than copying the entire planet-by-planet matrix or every generation parameter literally. See GTNH Ore Progression Baseline.
- Galaxia Alpha spans the full Ore Tier 1–10 progression, while the final planned mechanical depth of every destination is not required for Alpha.
- Every Ore Tier must satisfy the Closed Tier Cycle completeness invariant: intended prior progression unlocks a completable Galaxia activity, the activity yields a usable progression result, and that result leads into the next intended step without a blocker or dead end. This invariant does not prescribe identical mechanics or tier-specific content.
- An Ore Tier is planned as a Tier Destination Portfolio. Galaxia authors destination capabilities and Tier Gate rules, while the player constructs a Valid Tier Route through the resulting Progression Ecosystem; classifications such as mandatory, alternative, and optional emerge from those rules. Galaxia may consolidate the baseline into fewer, deeper destinations while preserving progression access and meaningful choice.
- As the working Alpha default, every Ore Tier requires Persistent Tier Infrastructure somewhere in its Closed Tier Cycle. It may be surface-based, orbital, automated, or otherwise located in space; later exceptions require a concrete tier-specific reason and must be documented explicitly.
- Define Player Presence and Automation Tradeoffs — physical presence is selected per activity, while later automation trades player time and attention for capital, logistics, constraints, and candidate recurring upkeep. Casual dictated uses of `Automated Station` and `Automated Outpost` are normalized to `Automated Facility`; in the extraction example, the specific asset is an Automated Outpost.
- Define Non-Material Tier Gate Role — every Ore Tier currently defaults to an Ore-Backed Tier Gate: acquiring and processing its intended off-world progression material is the primary non-substitutable requirement. Research, knowledge, and data may add gameplay or gate activities inside a Closed Tier Cycle, but Alpha does not require a research-only, data-only, or universally composite Tier Gate. A compelling future concept may introduce an explicit exception.
- Define Galacticraft-Equivalent Destination Backfill — begin with the Galacticraft celestial and ore layout as a Star Map-only design scaffold, then build Galaxia-specific content by editing that scaffold. Near the Alpha cutoff, retained destinations that still lack a stronger custom design receive a minimal Galaxia-owned implementation of their original Galacticraft-style role; Alpha does not delegate their runtime gameplay to the original mod and does not treat dummy Star Map entries as complete content.
- Define Minimum Galacticraft-Equivalent Destination Contract — a basic backfilled destination must support travel in, a playable dimension and environment, access to its required ores, a real extraction activity, travel out, and a usable result that continues a Valid Tier Route. Unique research, production, automation, narrative, and final depth are not required by this floor; Persistent Tier Infrastructure remains a tier-level rather than per-destination obligation.
- Interplanetary teleportation of players, items, and fluids is unavailable; explicit travel and logistics infrastructure must carry those flows.
- Alpha does not impose one universal destination loop. Different destinations may be infrastructure anchors, limited resource expeditions, remote automation sites, or optional members of a generated population.
- Define Celestial Object and Gameplay Space Mapping — Star Map Objects and Dimensions are not one-to-one. A body may own a direct dimension, a region such as an asteroid belt may own a shared Regional Dimension, and persistent child objects may support infrastructure or extraction without appearing as matching terrain inside that dimension.
- Require Star Map Object Actionability — every retained Star Map object exposes an object-native action. A construction row uses an immediate primary action that creates a material-fed Construction Site plus a smaller `?` information control for requirement previews; Galaxia does not infer the player's GTNH tier or ship inert placeholders.
- Define Asteroid Belt Physical Travel and Beacons — persistent Star Map asteroids are remote infrastructure targets that cannot be visited by the player. The planned extension of the current normal belt dimension makes it a ring-shaped Regional Dimension: the player selects a belt point to fly to mapped coordinates and places a Belt Beacon there to create a reliable return target.
- Automated outposts, automated stations, rockets, and spaceships are separate concepts whose allowed placement and routes follow the physical parameters of their origins and destinations.
- No physically possible mission may create a Progression Bypass. Reaching, observing, or interacting with a later destination is acceptable only when its outcomes do not satisfy a later Tier Gate without the intended prerequisite progression.
- Celestial Discovery is an observational capability, not proof of physical access or resource access. Naturally conspicuous objects may begin discovered, while smaller, obscured, or specially authored objects require better observation capability.
- Registered celestial bodies currently default to `DISCOVERED` unless authored otherwise. Generated large asteroids begin discovered, while generated medium and small asteroids begin `HIDDEN`.
- Object discovery and resource knowledge are separate. Discovering an asteroid does not automatically reveal its ore profile; current generated large asteroids only have a deterministic chance to begin with profile knowledge, while non-large generated asteroids begin with unknown ore knowledge unless authored otherwise.
- Galaxia Alpha uses one discovery-satellite capability level and one hidden-object detection level. Alpha does not need a sensor-tier ladder whose partial failures would be difficult to communicate without revealing that an undiscovered object exists.
- The Star Map begins unavailable. The team activates it by successfully launching and deploying its first observation telescope or discovery-satellite payload into the starting world's orbit. Activation exposes initially discovered objects but does not reveal hidden objects or their resources.
- For Galaxia Alpha, a deployed observation satellite is a permanent orbital asset with no maintenance, failure, destruction, or other lifecycle interaction. Star Map Activation and acquired knowledge therefore remain available; richer satellite lifecycle behavior may be reconsidered after Alpha.

## Accepted Alpha Opening

Begin Galaxia before the team has access to the Star Map. The player builds the first rocket with an observation telescope or discovery-satellite payload and launches it into the home world's orbit. Successful deployment activates the Star Map and exposes the team's initially discovered celestial objects; subsequent satellite scans reveal hidden objects through the existing discovery system.

This opening would make the first rocket establish Galaxia's observation capability instead of immediately serving as a destination-selection vehicle. The current code already has satellite-driven discovery work, scan radius, scan progress, and hidden-asteroid revelation, but it does not yet provide this Star Map activation gate or a dedicated opening telescope payload.

Accepted during Galaxia Alpha Wayfinder charting on 2026-07-31.

## Candidate Flight Design Direction — Awaiting Confirmation

Use a physics-informed but balance-authored flight model. Route requirements should be derived on demand from celestial properties, endpoint placement, orbital geometry, and atmosphere rather than from a hardcoded destination whitelist. Modular vehicle capabilities should be derived from the assembled vehicle rather than from a fixed vehicle tier.

The values and comparison rules do not need to reproduce real-world performance literally. Galaxia needs a deliberate balance layer that preserves the ten-tier progression and prevents an early optimized vehicle from making the later progression irrelevant. Physical feasibility, progression availability, and economic practicality should remain distinguishable questions.

This direction is not yet an accepted design. In particular, realistic orbital behavior can make transfers between distant outer-system objects relatively cheap in delta-v while making them extremely long. It is unresolved whether progression should be protected through mission duration and consumables, environmental capabilities, infrastructure, authored adjustments to route cost, explicit progression constraints, or a combination of these levers.

Existing code already provides part of this foundation: rocket stages and assemblies expose mass and delta-v, celestial bodies expose gravity, mass, radius, atmosphere, sphere-of-influence, and parking-orbit properties, and orbital transfers use Lambert-route calculations.

The design should deepen those existing owners: assembled vehicles own derived capability, celestial bodies own authored physical facts, and orbital mechanics own route requirements. Avoid a parallel destination-tier table or a feature-local capability score that duplicates those models.

## Open Decisions

- Establish which ore first occurrences are actual GTNH progression gates and which are only strong candidates.
- Map Ore Tiers 1–10 to the exact GTNH technology-tier entry and exit gates using authoritative progression sources.
- Identify the mandatory and optional destinations inside every Ore Tier and define their Celestial Progression Cycles.
- Define each destination through concrete gameplay, actions, infrastructure, and progression contribution without introducing a shared destination-role taxonomy or requiring persistent player-built infrastructure everywhere.
- Assign roles to mandatory destinations, optional authored destinations, and generated minor bodies; a large asteroid field is not a checklist requiring the player to visit every asteroid.
- Reconcile the intended asteroid automation model with the current domain distinction: generated asteroid assets allow `AUTOMATED_OUTPOST`, reject `AUTOMATED_STATION`, and allow miners only on automated outposts.
- Define the authoritative celestial parameters and thresholds that determine outpost eligibility, station eligibility, solar behavior, mining capability, and transport-route feasibility.
- Decide whether transport eligibility is evaluated directionally and whether one-way spaceship routes into a gravity well are ever useful or supported.
- Specify the Alpha responsibilities and progression relationship of rockets, spaceships, and Hammers without collapsing them into interchangeable logistics methods.
- Decide which flight constraints are physical feasibility calculations and which are explicit progression or economic constraints.
- Define the smallest vehicle-capability and route-requirement model that supports modular construction without turning Galaxia into a literal aerospace simulator. Candidate inputs include delta-v, thrust-to-weight behavior, atmosphere or entry constraints, travel time, fuel, and endpoint infrastructure.
- Establish balance invariants that prevent early-tier modular vehicles from bypassing the intended Ore Tier 1–10 progression even when a physically valid trajectory can be computed.
- Define what `destination access` means by separating at least reconnaissance, crew arrival, landing, resource extraction, sustained operation, cargo export, and safe return. These actions may require different capability envelopes and need not unlock together.
- Determine how long but delta-v-cheap outer-system transfers are balanced for crewed missions, uncrewed missions, and recurring logistics without disguising every balance adjustment as literal physics.
- Define the reward boundary for early reconnaissance. The current narrow candidate reveals planning information such as discovery, environment, orbit, or resource potential but cannot extract or export resources and cannot produce research that satisfies a later Tier Gate.
- Decide whether an exceptionally demanding off-sequence mission may provide later resources when its prerequisites and cost preserve the intended progression rather than bypassing it.
- Define how player observation capabilities, object observability, scan scope, and scan duration combine to discover hidden celestial objects.
- Define the knowledge layers revealed after object discovery, including when environment, orbit, resource signature, and full resource profile become known.
- Decide which registered objects remain naturally visible by default and which authored destinations should override the default to begin hidden.
- Define the pre-Star-Map local-orbit launch flow, team ownership of activation, and initial map contents.
- Define the respective Alpha roles, unlock points, payloads, and endpoint requirements of rockets and Hammers.
- Determine whether the no-teleportation rule has any explicitly supported boundary cases; do not assume exceptions by default.
- Define the player-facing objective, decision structure, consequence, and continuation path for every included cycle.
- Determine how optional destinations and alternative progression routes interact with mandatory tier gates.
- Decide which research, satellite-data, and advanced production mechanics are required somewhere in Alpha and which remain post-Alpha depth.
- Define Alpha Galaxia-Specific Capability Floor — provisionally prefer a capability-based Alpha floor over a quota of redesigned planets, but do not accept a mandatory capability list until the relevant planet and mechanic proposals have been reviewed and validated with their designers.
- Determine which parts of the existing concept map are alpha requirements, later-scope ambitions, or obsolete assumptions.

## Deferred Implementation Follow-ups

- Define Prospecting Satellite Range Feedback — a preserved, non-blocking implementation handoff for a global localized coverage overlay. Remaining presentation and rendering-technique choices are intentionally deferred and do not belong to the active Galaxia Alpha Wayfinder frontier.

## Out of Scope for Galaxia Alpha

- Multiple discovery strength tiers and multiple hidden-object detection requirements. Revisit them only with a player-feedback model that communicates sensor limitations without directly revealing undiscovered objects.
- Observation-satellite maintenance, failure, destruction, replacement pressure, and other lifecycle interactions.

## Next Wayfinder Step

Continue from Galaxia Alpha Wayfinder. Choose one open, unblocked, unclaimed ticket from its area graph; do not continue operating from this archived staging note.

## Provenance

- [[Audit Galaxia Concept Map]]
