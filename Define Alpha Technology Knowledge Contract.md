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

How does Alpha acquire team Technology Knowledge and use it to gate production and present module choices?

## Resolution

Craft a Technology Blueprint from the relevant processed material, then consume it through player activation to grant the current team its knowledge. Production checks team knowledge. Catalog controls expose unknown and manually hidden entries without disabling existing designs. These already accepted rules are separated from the broader research-content floor so unresolved imported proposals do not make them appear undecided.

## Planetary Technology Research Direction

On 2026-09-11 the owner proposed a Galaxia-owned system in which players perform research on planets to unlock better technology. This is the working replacement direction for mandatory dungeon or boss schematic acquisition, not a finalized research tree or activity implementation.

Optional bosses and dungeons may remain, but completing them is not required for progression. Define Non-Material Tier Gate Role owns that accepted boundary.

The Alpha acquisition mechanism and team knowledge model are established below. Concrete technology groups, recipes, and their placement across progression remain open. Richer research activities are later work. Satellite discovery and resource profiling are distinct from technology research.

## Alpha Technology Blueprints

For Alpha, acquiring a technology is represented by crafting its blueprint from a quantity of material unlocked through the relevant planet. This is the owner's accepted minimal gameplay mechanism for closing progression without designing advanced research activities now.

The progression-material ingredients are ingots, not raw ores. For the current working titanium, desh, and naquadah direction, acquiring the blueprint therefore requires obtaining the material in ingot form. Exact quantities and technology assignments remain open.

More elaborate planetary experiments or research mechanics may replace or extend this mechanism later, for example during Beta. They are not Alpha prerequisites. Do not introduce an experiment machine, research minigame, or research tree implementation merely to support this initial blueprint contract.

The material recipe creates the connection to planetary progression. This decision does not additionally require crafting the blueprint on the planet unless the specific recipe has an independently accepted environmental requirement. Exact materials, quantities, and technology assignments remain to be determined. The accepted use behavior is described under Team Technology Knowledge below.

## Team Technology Knowledge

Technology knowledge belongs to the team. In the accepted Alpha flow, the player crafts a technology blueprint and uses it with a right-click to add the associated knowledge to their current team. Successful acquisition consumes the blueprint.

The acquisition mechanism and the knowledge requirement are separate. Later research gameplay may change how a blueprint is obtained without changing the meaning of the team knowledge it grants. No advanced research activity is required to implement the initial Alpha acquisition flow.

Rocket Blueprints remain reusable Rocket assembly designs for automated production. They do not confer technology knowledge and must not be confused with technology blueprints.

Some recipes or module-production operations may be knowledge-gated. The owner has not specified the complete gated set or the integration with recipe systems. Current Silo assembly, Module Assembler production, and external recipe processing must be distinguished when choosing the enforcement point. Do not assert that the current Silo already crafts parts from recipes or implements technology checks.

### Knowledge-Gated Production

One Technology Blueprint may unlock a coherent group of related recipes, components, and part variants. Grouping follows a concrete technology rather than requiring one blueprint per item or automatically bundling all technology associated with a planet. Several technologies may use materials from the same planet. Exact groups are assigned when their content is designed.

Owner accepted technology-level grouping on 2026-09-11.

The owner also accepted ongoing material use in production on 2026-09-11. Acquiring Technology Knowledge does not replace the progression material in parts whose properties depend on that material. Such parts continue to consume it when manufactured, sustaining extraction and logistics after the initial blueprint. This does not require every recipe unlocked by a technology to consume the same material.

Executing a knowledge-gated recipe requires checking the relevant team's Technology Knowledge. Automated machines use the knowledge of their owner's team. The production system enforces the requirement before executing the recipe.

Behavior when the team already knows the technology remains to be confirmed. Do not infer item loss on a failed or redundant activation from consumption on successful knowledge acquisition.

### Catalog Visibility

Unknown technology entries are hidden in the normal catalog view. A View mode control exposes all entries, including unknown entries shown greyed out with a lock indicator.

The player may manually mark a module obsolete using an eye control. It disappears from the normal list and remains visible in View mode. This is a player-controlled visibility preference, not automatic obsolescence inferred from tiers or statistics, and not a rule that disables existing modules, Rocket designs, or production.

The owner described technology blueprints and modules together in this catalog discussion. Apply the rule to the relevant technology/module selection UI when its precise surface is defined. This does not establish a global NEI hiding policy.

Owner decisions on 2026-09-11: consumption on successful knowledge acquisition, knowledge checks for production, hidden unknown entries, View mode with greyed locked entries, and manual obsolete-module hiding.

Owner decision on 2026-09-11: craft the blueprint, right-click it as a player, and add the corresponding knowledge to the team. Future mechanics may provide other ways of crafting or obtaining that blueprint.

Owner decision on 2026-09-11. This supersedes the proposed on-site experimental research workflow for the current Alpha scope, without ruling out a richer later system.

## Current Implementation Boundary

On 2026-10-08 the owner reaffirmed that enforcing knowledge-gated production in GT5 machines remains unresolved. The accepted gameplay requirement to check team knowledge does not establish an integration mechanism. [[Design Early Orbital Production Recipe Chain]] retains Rocket Automation and Functional Satellites as likely but unapproved blueprint proposals pending that investigation and later content approval.

The owner's later clarification separates Environment Tags from Technology Knowledge. The accepted Galaxia-defined tags, such as Microgravity and No Atmosphere, concern recipe environment checks, not team membership or technology access. [[Define Celestial Capability Rules]] owns that contract. It does not resolve knowledge-gated production or approve the proposed blueprint groups.

Source inspection on 2026-09-12 found a reusable assembly design in `registry/items/special/ItemRocketSchematic.java:24` and `registry/rocketmodules/rocket/blueprint/RocketBlueprint.java:16`, not the consumed Technology Blueprint described here. `registry/celestial/knowledge/CelestialKnowledgeFacts.java:11` owns discovery and resource facts, not Technology Knowledge. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. The inspected owners do not establish implementation of this contract.

## Provenance

[[Project Lead Technology Knowledge Direction]] records the earlier preference for research. The subsequent owner decisions in this conversation define the accepted Alpha mechanism. The broader required capability set remains in [[Define Alpha Research and Production Floor]].
