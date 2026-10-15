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

# Define Alpha Technology Knowledge Contract


## Question

How does Alpha acquire team Technology Knowledge, gate production and present module choices?

## Resolution

Craft a Technology Blueprint from the relevant processed progression material, then right-click it as a player to grant knowledge to the current team. Successful acquisition consumes the blueprint. The ingredients are ingots rather than raw ores. Exact quantities, technologies and their recipes remain open.

This is the accepted minimal Alpha mechanism. Planetary experiments, research minigames and a research tree are not prerequisites. Later research may change how blueprints are obtained without changing team knowledge. Crafting on the planet is not required unless a recipe has an independently accepted environmental condition.

Rocket Blueprints are separate reusable assembly designs. They do not grant Technology Knowledge. Satellite discovery and resource profiling are also distinct.

## Knowledge-Gated Production

- One blueprint may unlock a coherent technology group of recipes, components and part variants. Neither one blueprint per item nor one bundle per planet is required.
- Production checks the relevant team's knowledge before executing a gated recipe. Automated machines use their owner's team.
- Knowledge does not replace ongoing material consumption in parts whose properties depend on that material. Not every unlocked recipe must use the same material.
- Redundant activation behavior remains undecided. Consumption on successful acquisition does not imply item loss when the team already knows the technology.

## Catalog Visibility

Unknown entries are hidden in the normal catalog. View mode exposes all entries, with unknown ones greyed out and locked.

An eye control lets the player mark a module obsolete. This hides it from the normal list but keeps it in View mode. It is a manual visibility preference, not automatic tier-based obsolescence or a rule disabling existing modules, Rocket designs or production.

Apply these rules to the relevant technology/module selection surface when defined. They do not establish global NEI hiding.

## Implementation Boundary and Open Content

The exact gated set and GT5 enforcement integration remain unresolved. Silo assembly, Module Assembler production and external recipe processing need distinct treatment. Do not infer that the Silo already crafts recipe parts or checks knowledge.

[[Design Early Orbital Production Recipe Chain]] retains Rocket Automation and Functional Satellites as unapproved blueprint proposals. Environment Tags in [[Define Celestial Capability Rules]] describe local conditions, not team knowledge, and do not resolve technology enforcement.

Inspection on 2026-09-12 found reusable designs in `registry/items/special/ItemRocketSchematic.java` and `registry/rocketmodules/rocket/blueprint/RocketBlueprint.java`. `registry/celestial/knowledge/CelestialKnowledgeFacts.java` held discovery/resource facts, not Technology Knowledge. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. This does not establish implementation of the accepted blueprint contract.

## Provenance

Owner decisions on 2026-09-11 selected the Alpha mechanism, technology grouping, ongoing material use and catalog rules. GT enforcement remained unresolved on 2026-10-08. [[Project Lead Technology Knowledge Direction]] preserves the earlier research preference. [[Define Alpha Research and Production Floor]] owns the broader capability floor. [[Define Non-Material Tier Gate Role]] excludes mandatory boss and dungeon gates.
