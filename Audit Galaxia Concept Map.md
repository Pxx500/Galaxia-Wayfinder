---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Alpha Scope]]"
source_file: "[[Galaxia Concept Map Extracted Claims]]"
source_inventory: "[[Galaxia Concept Map Inventory]]"
source_conversation: "codex://threads/019f89d3-71d2-7c02-9b25-7c034707e20f"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Audit Galaxia Concept Map

## Resolution

The archived 37-page concept map is a low-priority gap inventory, not design authority. Current owner decisions and accepted Wayfinder notes override it. Other developer documents outrank it. Product claims need accepted support, and implementation claims need direct code evidence.

Unsupported connective text, space-grade-alloy ambitions, generic facility heat or utility networks, AE2 boundaries, recovery flows and advanced transport claims do not become Alpha requirements merely by appearing in the map.

## Accepted Decisions Retained Here

### Shared Team Assets

The GTNH team owns shared Galaxia infrastructure and strategic assets. All team members have equal access. Galaxia adds no roles, ranks or configurable permission layer above team membership. The map's role-based permission design is rejected.

[[Issue - Preserve Assets Across Team Disband]] owns the accepted asset-successor rules and the missing disband integration.

### Prospecting Satellite Role

One Prospecting Satellite both contributes discovery work for eligible hidden objects in scope and independently generates Raw Prospecting Data about the object it orbits. Discovery progress and the ongoing data pipeline are separate processes.

[[Define Prospecting Data Processing]] owns the round-trip pipeline, bounded buffers, returned-throughput bonuses and provisional tuning. [[Define Prospecting Effects by Extraction System]] owns machine-specific effects. The opening payload's identity belongs to [[Specify Alpha Opening Mission Flow]].

### Automated Miner Controls

Retain focus tier, selected focus ore and blacklist/voiding controls as meaningful specialization and logistics safeguards. Parallel capacity derives from module tier and upgrades, not a freely adjustable operational slider.

Automatic miner response to `network demand` is rejected from Alpha. A future concrete demand system needs its own design decision.

## Decision Owners

- [[Define Celestial Object and Gameplay Space Mapping]] and [[Require Star Map Object Actionability]] own object representation and useful map actions
- [[Define Asteroid Belt Physical Travel and Beacons]] and [[Define Asteroid Automation Contract]] own physical belt travel and generated asteroid infrastructure
- [[Define Alpha Transport Roles]], [[Define Vehicle Capability and Route Requirements]] and [[Define Flight Progression Balance Invariants]] own transport, explainable route checks and progression protection
- [[Define Minimum Galacticraft-Equivalent Destination Contract]], [[Define Destination Access Levels]] and [[Define Destination Role Taxonomy]] own destination completeness
- [[Define Alpha Celestial Knowledge Layers]] and [[Define Alpha Research and Production Floor]] own knowledge and required research or production
- [[Define First Physical Station Contract]] owns the first Station role and current progression placement. Its later decisions supersede this audit's provisional Luna, Station, Mars ordering
- [[Review Crater Nodes Proposal]] owns specialized deposits, drilling, fracking and the later accepted Space-Grade Alloy direction

## Historical Implementation Inventory

The audit found foundations for celestial identity, generated asteroids, the Star Map, Rocket construction, physical environments, discovery, satellites, communication, Automated Facilities, GT recipe processing and HAMMER logistics. It did not establish complete journeys, a coherent exploration loop, a research progression or the accepted prospecting gameplay pipeline.

Those observations are historical, not a current feature-completion certificate. Recheck the relevant owner and code when implementation begins. The imported claims remain in [[Galaxia Concept Map Extracted Claims]] and [[Galaxia Concept Map Inventory]].
