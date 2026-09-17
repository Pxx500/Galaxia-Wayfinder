---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Observation and Research
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Data Processor Machine Topology

## Question

Should Alpha Data Processing be owned by an expandable modular multiblock, a pool of smaller cooperating machines, or another physical topology, and where do processor capacity, EU use, job priorities, and local status belong in that model?

## Established Input

- [[Define Prospecting Data Processing]] owns the topology-independent data-flow and bonus contract.
- Processing requires player-built infrastructure and EU. The accepted structural computing sections below determine capacity through their number and tier.
- The design must not assume one global Data Processor or an unbounded data store.

## Owner-Led Design

On 2026-09-16 the owner authorized choosing the topology directly rather than waiting for other developers. The former feedback prerequisite is no longer required. No topology was selected by this instruction.

## Accepted Direction

On 2026-09-16 the owner selected an expandable modular multiblock. Multiple independent installations remain possible. A subsequent round accepted structural capacity, operating intensity and installation-local job configuration, resolving this ticket.

- The desired baseline operates passively using EU, without requiring the player to insert items into the machine. Raw and processed data remain network state, not item inputs.
- Processing capacity increases by adding structural computing sections to the multiblock. Their technology tier comes from the blocks used. This replaces the earlier assumption of inserting processor items into the machine.
- Energy is consumed for processing work, as established in [[Define Prospecting Data Processing]].
- A simpler, lower-tier counterpart to TecTech computing machinery is a candidate to investigate, not a selected dependency or a claim that existing machinery already satisfies this contract. No exact voltage tier was chosen.
- The player can set operating intensity. An economical setting processes less data but uses less EU per unit of data. A faster setting increases throughput at a worse EU cost per unit. The setting supports sustained passive operation rather than repeated manual interaction.
- Each installation owns its enabled jobs and job priorities, using the scheduling rules in [[Define Prospecting Data Processing]]. Different installations may specialize in different origins or job types without reconfiguring all processors.
- Alpha's additional gameplay choice is the tradeoff between expanding infrastructure and spending more EU for throughput. A minigame remains a possible later extension, not an Alpha requirement.

## Resolution

The Data Processor is an expandable modular multiblock whose capacity comes from the number and tier of structural computing sections. It processes network data passively using EU, with configurable throughput-versus-energy efficiency and installation-local job settings. The owner accepted all three recommendations in the follow-up round on 2026-09-16.

Exact geometry, voltage tiers, capacity and energy curves remain implementation and balance choices. Before implementation, evaluate relevant TecTech capabilities for reuse without inheriting unwanted interaction requirements. No reuse target has been selected, and this design resolution is not evidence of implementation.

## Related Topics

- Collect Data Processor Topology Feedback
- Define Prospecting Data Processing
