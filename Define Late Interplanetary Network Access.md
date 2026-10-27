---
type: wayfinder-ticket
ticket_type: grilling
status: deferred
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Travel and Logistics]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Late Interplanetary Network Access

## Question

Should any later technology permit cross-destination material or energy networks, and what keeps ordinary early communication satellites from replacing physical freight?

## Accepted Boundary

Early Communication Satellites must not unlock unrestricted interplanetary item, fluid or energy transfer. Increasing the number of cheap early satellites must not substitute for a genuinely later capability. Communication for data and remote control remains useful independently of material transport.

Remote transfer of resources and energy belongs in Alpha. Design its exact access and behavior at the end of Alpha development, after physical logistics can be evaluated. This scheduling decision does not select an in-game technology tier or approve the existing satellite-only Quantum Ring rule. [[Require Explicit Interplanetary Logistics]] remains the restriction until the late-access contract is selected.

Quantum links can replace the need for physical freight between connected destinations. Treat their introduction as a qualitative capability change, not something balanced solely by a fixed ongoing charge or a large quantity of old-tier satellites. Earlier components become cheap quickly relative to later production capacity. A near-star solar installation is not inherently bad gameplay, but early unrestricted energy export would erase meaningful supply choices.

## Current Code Evidence

Read-only inspection on 2026-10-22 found the following in `compat/ae2/QuantumLinkRules.java`, under Galaxia's main Java package:

- Main checkout `f2ccabeb5c90c051ec25be138a7e486dbc0b9136`: cross-body eligibility requires a Communication Satellite at each endpoint. This rule does not allocate bandwidth.
- The inspected `remote-android-bodies` worktree adds a lifetime reservation of 1000 kbps for a cross-body bridge. That fixed allocation is independent of item or fluid traffic through the AE2 connection. It is a connection-capacity cost, not a freight-throughput limit.
- Same-dimension links are allowed. Dimensions mapped to HOME may link without relays. Mapping groups some dimensions together, so the rule is not equivalent to a universal cross-dimension ban.

This is bounded code evidence, not runtime verification or approval of the current behavior. The Quantum Ring's own recipe progression was not audited. Early satellite availability alone does not prove that the complete bridge is craftable at HV.

## Deferred Design Within Alpha

Keep data communication available early while developing and testing physical logistics. Before Alpha completion, select the remote-transfer capability, its progression prerequisites and its transport contract. A fixed bandwidth charge alone cannot limit an unrestricted material network. No final hardware or resource-throughput model is selected.

## Decisions Needed

- What in-game access and operating model permits the selected late remote transfer without making earlier physical logistics irrelevant prematurely?
- Does the restriction include surface-to-orbit links on the same body, and how are unrelated home dimensions treated?
- If an exception is selected, what actual hardware and operating costs provide its progression and what quantity does its capacity limit?

Do not infer that allowing data traffic permits arbitrary items, fluids, EU or every AE2 network function.
