---
type: wayfinder-research
status: complete
parent: Review Galaxia Main Planning Document
source: "[[Discord Source - Galaxia Main Planning Document]]"
tags:
  - galaxia/alpha
  - wayfinder/research
---

# Galaxia Main Planning Document Review

> Source interpretation, not current design authority. Accepted decision tickets take precedence. Code observations are dated evidence, not current verification.

## Authority

- This source is a mixed planning archive, not an accepted specification.
- Current owner decisions and resolved Wayfinder notes override imported material. Other developer documents outrank the retired agent-generated concept map.
- Sections explicitly labelled `OLD VERSION, WILL BE DEPRECATED` are superseded and contribute no requirements unless independently corroborated.
- Ore and resource placement is excluded. GTNH Ore Progression Baseline and the maintained GTNH Ore Sheet remain authoritative.

## Corroborated Existing Direction

- Galaxia is GTNH's space-progression hub and replaces required Galacticraft capabilities through Galaxia-owned systems rather than literal feature parity.
- Spacecraft are modular and rely on constructed launch infrastructure.
- The first destination order remains Overworld → Moon → Mars; later destination design continues from the current GTNH baseline.
- Progression preserves GTNH's tier backbone and remains primarily material-gated. Galaxia communicates required materials and capabilities rather than attempting to infer an abstract player tier.
- Physical Stations are player-accessible infrastructure distinct from Automated Facilities.
- Interplanetary freight, docking, orbital infrastructure, and surface infrastructure form explicit logistics chains.
- Destination activities should exploit local environmental and physical properties.
- Research may enrich or gate activities but does not replace the current ore-backed material hard-gate default.

## Section Classification

| Section | Classification | Routing |
| --- | --- | --- |
| About | Provenance only | No product requirements retained. |
| Rocket Systems | Partly corroborated | Modular rockets and launch infrastructure are existing direction. Vehicle roles route to Define Alpha Transport Roles; capability and route variables route to Define Vehicle Capability and Route Requirements. Exact tiers, recipes, values, and module lists are not accepted by this review. |
| Rocket System — old version | Superseded | Discarded. |
| Space travelling | Partly routed | Route cost, payload, fuel, mass, and capability concepts route to Define Vehicle Capability and Route Requirements and Define Flight Progression Balance Invariants. The active-flight proposal routes to Define Player Flight Interaction Model. Personal Dimension launch and return behavior routes to Define Personal Dimension Homeworld Integration. |
| Space travelling — old version | Superseded | Discarded. |
| Space stations | Partly routed | The need for at least one physical Alpha station is established. Exact modules, life support, docking, construction, and shipyard behavior remain open in Define First Physical Station Contract, Define Alpha Research and Production Floor, and Define Alpha Transport Roles. |
| Space stations — old version | Superseded | Discarded. |
| The Vael System | Deferred | Named destinations and authored mechanics remain with their inactive owning developer. Alpha planning uses the current GTNH destination baseline until those concepts are deliberately revived. Ore claims are ignored. |
| Replacing Features | Color classifications recovered | The table below preserves the original document's explicit classification, not an Alpha implementation commitment. |
| Equipment | Open design input | Environmental access routes to Define Destination Access Levels. The proposed combined thermal and modular life-support framework is not accepted by this review. |
| Stretch Goals | Outside current Alpha | Interstellar systems, space tractors, and other stretch concepts are not inherited into Alpha. Object-native extraction ideas may be reconsidered under Define Celestial Capability Rules. |
| Development | Reference material only | Links, asset suggestions, and administrative notes create no product requirements. |

## Superseded or Unaccepted Details

- Fixed destination whitelists tied directly to numbered rocket cores are superseded by capability-derived route eligibility.
- Early-MV atmospheric test rockets and the old module-test technology tree are not current direction.
- The document does not establish that every retained destination requires a unique technology line or complete bespoke redesign.
- Exact rocket-versus-spaceship tier boundaries, station modules, vehicle parameters, environmental equipment frameworks, and asteroid extraction designs remain owned by their linked tickets.
- Interstellar destinations, warp drives, space tractors, and the space-pumping rework remain outside current Alpha.

## Replacing Features Color Recovery

Legend from the live document: green = replicated, orange = replaced, red = deprecated. Entries without an explicit color remain unclassified.

### Replicated — Green

- Cryogenic Chamber
- Energy Storage
- Fuel Loader
- Cargo Loader/Unloader
- Landers
- Flag
- Arc Lamps
- Air Lock
- Buggy
- Launchpad
- Asteroid Miner
- Parachute
- Oxygen Tanks
- Thermal Systems/Protection
- Gravity
- Space Stations
- Glowstone Torches

### Replaced — Orange

- Oxygen Bubble Generator → modular oxygen ventilation
- Galacticraft Solar Panels
- Shuttle Rockets → modular rockets
- Mothership, Control, and Components → warp-drive ship
- Rocket Schematics → module tech tree and test-flight missions
- Grappler → zero-G dash

### Deprecated — Red

- Block Scale
- NASA Workbench
- Throwable Meteors

### Unclassified

- Oxygen Collector
- Oxygen Compressor
- Oxygen Decompressor
- Oxygen Sealer
- Oxygen Detector
- Oxygen Storage
- Terraformer
- Hydroponics Unit
- Frequency Module
- Artificial Gravity
- Fluid Manipulator
- Dark Matter
- Nanite Cluster
- Nanite Control Module
- Sensor Lens
- Sensor Glasses
- All listed resources; their placement is ignored in favor of the maintained GTNH Ore Sheet

## Result

- Corroborated concepts were routed to their existing Wayfinder owners instead of duplicated.
- Two uncovered product forks became Define Player Flight Interaction Model and Define Personal Dimension Homeworld Integration.
- Deprecated, deferred, unclassified, and out-of-Alpha material remains provenance only and is not accepted design.
