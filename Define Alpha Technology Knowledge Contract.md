---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Alpha Technology Knowledge Contract

Technology Knowledge lets a team produce selected recipes after a player consumes a crafted Technology Blueprint.

## Blueprints and Production

Craft a Technology Blueprint from the relevant processed progression material, then right-click it as a player to grant knowledge to the current team. Successful acquisition consumes the blueprint. The ingredients are ingots rather than raw ores.

Planetary experiments, research minigames and a research tree are not prerequisites. Later research may change how blueprints are obtained without changing team knowledge. Crafting on the planet is not required unless a recipe has an independently accepted environmental condition.

Rocket Blueprints are separate reusable assembly designs. They do not grant Technology Knowledge. Satellite discovery and resource profiling are also distinct.

The initial technology groups are:

| Technology | Gated production |
| --- | --- |
| Rocket Automation | Rocket Automation Controller |
| Functional Satellites | Basic Communication Satellite and Prospecting Satellite |

Material processing, SiGe, fluoride-glass production, frames, dishes and Primitive Telescope production do not require these two technologies. Neither technology gates manual Rocket dispatch or manual Luna travel.

- One blueprint may unlock a coherent technology group of recipes, components and part variants. Neither one blueprint per item nor one bundle per planet is required.
- Production checks the relevant team's knowledge before executing a gated recipe. Automated machines use their owner's team.
- Knowledge does not replace ongoing material consumption in parts whose properties depend on that material. Not every unlocked recipe must use the same material.

## Catalog Visibility

Unknown entries are hidden in the normal catalog. View mode exposes all entries, with unknown ones greyed out and locked.

An eye control lets the player mark a module obsolete. This hides it from the normal list but keeps it in View mode. It is a manual visibility preference, not automatic tier-based obsolescence or a rule disabling existing modules, Rocket designs or production.

Apply these rules to the relevant technology/module selection surface when defined. They do not establish global NEI hiding.

## Open Decisions and Implementation Boundary

- Exact blueprint quantities, recipes and later technologies remain open. [[Design Early Orbital Production Recipe Chain]] owns proposed costs for the initial groups.
- Redundant activation is undecided. Consumption on successful acquisition does not imply item loss when the team already knows the technology.
- GT enforcement remains unresolved. Silo assembly, Module Assembler production and external recipe processing need distinct treatment. Do not infer that the Silo already crafts recipe parts or checks knowledge.

Environment Tags in [[Define Celestial Capability Rules]] describe local conditions, not team knowledge, and do not resolve technology enforcement.

Inspection on 2026-09-12 found reusable designs in `registry/items/special/ItemRocketSchematic.java` and `registry/rocketmodules/rocket/blueprint/RocketBlueprint.java`. `registry/celestial/knowledge/CelestialKnowledgeFacts.java` held discovery/resource facts, not Technology Knowledge. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. This does not establish implementation of the accepted blueprint contract.

The 2026-09-11 decisions selected the mechanism, groups, material use and catalog rules. GT enforcement was still unresolved on 2026-10-08. [[Project Lead Technology Knowledge Direction]] preserves earlier research preference, [[Define Alpha Research and Production Floor]] owns the broader floor, and [[Define Non-Material Tier Gate Role]] excludes mandatory boss and dungeon gates.

## Gameplay Flow

The player crafts a Technology Blueprint from processed progression materials and uses it to grant the current team knowledge. A successful acquisition consumes the blueprint. The team can then produce recipes gated by that technology, while still supplying their required materials.

Unknown catalog entries are hidden in the normal view and shown locked in View mode. The player can also hide obsolete modules from the normal list without disabling them.
