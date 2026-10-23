---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
secondary_areas:
  - Area - Observation and Research
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Data Processor Machine Topology

## Question

What complete modular Computer supplies Galaxia data processing, including cluster connections, electricity, cooling, structure and manufacture?

## Current Owner Direction

The Computer is a modular data center: a main controller multiblock connects by information cables to separately powered and cooled Computing Clusters. Each cluster is a bounded multiblock assembled from individually craftable Computing Rack blocks. Each rack occupies one block and contributes processing capacity. Electrical supply and a coolant loop with a radiator make operation an infrastructure investment.

The initial delivery supports data processing only: receive Galaxia network data, process a defined job and supply its typed output to a requesting consumer. There is no initial mode selector or native TecTech computation service.

This replaces the previous single elongated structure and EU-only operating proposal. Its 3 by 3 repeating slices, 16-section limit, exact cluster recipes, data rates, 8:1 conversion and tier-power table were unapproved proposals. They are not retained as current requirements.

Structural computing equipment, multiple installations, operating-intensity tradeoffs and installation-local job priorities remain useful accepted inputs. No requirement to insert disposable processor items or repeatedly play a minigame follows from the new direction.

Orbit may be attractive because of local power and network geography. Orbital location, vacuum or microgravity is not a selected requirement for operating the Computer.

## Data Processing Is A General Service

A producer at A emits a data type. A compatible Computer performs a defined conversion. A consumer at B requests the result. A, the Computer and B may be at different locations.

Galaxia's existing team-owned satellite network transports input and output. The computer owns paid conversion, local job selection and bounded processing state. It must not create a second satellite routing service.

Origin restrictions belong to the job. Prospecting retains its celestial origin and must benefit the correct origin under [[Define Prospecting Data Processing]]. That restriction is not generalized into a rule that all processed information must return to its producer.

The first implemented job can remain prospecting. The generic boundary does not require a universal chain solver, automatic discovery of arbitrary processing paths or new jobs invented solely to demonstrate flexibility.

## Accepted Physical Arrangement

| Element | Responsibility |
| --- | --- |
| Main controller multiblock | Contains one controller block and its own energy hatch, coordinates connected clusters and consumes modest EU without contributing processing capacity |
| Computing Cluster | Bounded multiblock containing rack blocks, with local GT energy input, chilled-coolant input, ordinary-coolant output and a dedicated information connection |
| Computing Rack | One craftable hardware block placed within a cluster, initially available in EV, IV and LuV tiers |
| Radiator | Remove heat from returning ordinary coolant and return chilled coolant through a real pipe loop |

Players craft individual rack blocks and place multiple racks in a cluster. The cluster, not the rack block, is the separately connected modular multiblock. Its size remains bounded, but exact geometry and rack-count limits are open. The previous fixed-size rack-multiblock proposal is superseded. Initial rack block tiers are EV, IV and LuV. Mixing rack tiers within a cluster or across one controller's clusters still needs selection.

The main controller is also a multiblock, containing one actual controller block and its own energy hatch. It consumes a modest amount of EU for coordination. It supplies neither data-processing capacity nor TecTech computation. Processing capacity comes exclusively from operable rack blocks in connected clusters. Exact controller EU/t and structure remain open. Failure behavior follows [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]], not a custom retained-work system.

Controller-to-cluster cables carry information only. Every cluster has its own electrical input, chilled-coolant input and neutral ordinary-coolant output. Use ordinary GT electrical and fluid infrastructure for these utilities. The main controller does not distribute power or coolant through its information cables. Clusters can share upstream power and fluid installations while retaining their individual connections.

Recommend one active main controller per cluster, without counting the same capacity twice. The ownership and connection protocol remains to be finalized.

Each cluster has a dedicated point-to-point information cable run to the main controller. The owner selected spray-painted connection matching in the style of TecTech data cables, not a shared branching cluster network. Paint controls which neighboring cable segments connect, not a globally unique cluster identity or an implicit limit of one cluster per color. Exact endpoint layout and packet handling still require design. Reusing a cable block or its appearance does not prove that it supports the required job communication.

## Initial Scaling And Deferred Specialization

Do not add a processing-efficiency bonus merely for making a cluster larger. Such a bonus would encourage maximum-size copies without creating a useful choice. Installed hardware can add processing capacity, but grouping it does not grant an additional size-based multiplier. This does not settle exact cluster geometry, per-tier performance or operating intensity.

Retain specialized processing modules as a future idea, not initial content. A module could replace rack blocks and improve processing of a particular data type only within its own cluster. The tradeoff is lower general capacity for better specialized performance. Revisit this when enough distinct useful data-processing jobs exist to make that choice meaningful. Do not build a generic specialization framework or invent extra data types solely to justify it now.

The hierarchy is Computer -> Computing Cluster -> Computing Rack. A rack is one hardware block, a cluster is a multiblock subsection, and the Computer is the complete controller-managed installation.

## Deferred TecTech Computation

Revisit a TecTech-compatible computation service at the end of Alpha or after Alpha. Its Alpha inclusion is not committed. A cheaper Computer could undermine Quantum Computer progression or other computation consumers, so actual performance, costs and downstream balance must be assessed before adding it.

Do not implement native computation input/output, dual-mode allocation or mode-switching lifecycle for the initial data-processing delivery. Future reuse of the physical equipment does not require those mechanisms now.

## Recommended Work Accounting, Unapproved

The Computer enables typed jobs, optionally filtered by origin. Existing priorities govern allocation. The network delivers matching input to eligible computers and output to actual consumers. The computer advertises only demand it can service, with bounded input and output storage.

Compare two data integration models: a network-wide planner that chooses complete transformation chains, or computers registering ordinary input demands and output supplies for their enabled jobs. Prefer the latter for the concrete one-stage jobs. It keeps routing with the existing network and processing with the machine. Multi-stage automatic planning is not needed by the selected use case.

Only physically available cluster capacity contributes. A disconnected, unloaded, unpowered or cooling-limited cluster cannot provide phantom work. Connection changes should use existing cable/endpoint lifecycle mechanisms rather than scan the world for clusters every tick.

## Cooling Direction And Proposed Operating Rules

Use a closed loop:

Chilled coolant -> cluster -> ordinary coolant -> radiator or active chiller -> chilled coolant.

A cluster operation consumes EU and uses chilled coolant's cooling capacity, returning ordinary coolant. The owner prefers this to producing a hot fluid usable for power generation. A suitably exposed radiator restores the chilled state. An active chiller offers an electricity-consuming alternative when passive rejection cannot achieve the target. Computing on a planet remains valid.

The owner selected a closed coolant loop without ordinary fluid loss. Equal input and output fluid volumes are the proposed implementation. Output-fluid space must exist before committing work. The radiator removes the same authored heat that the fluid absorbed. A small electrical circulation cost is a proposal, not selected tuning. Exact fluid identities, target temperature, heat capacity and machine rates remain open.

Renaming a fluid does not prove energy safety. Audit actual fuel, heating, cooling and generator recipes for the chosen pair. Do not register the returned ordinary coolant as a new steam or hot-coolant power source. The completed cycle must not create unintended net energy through other supported machines.

Cooling capacity, electricity and computing hardware jointly limit throughput. Loss of required power or cooling during a GT-like processing operation follows the native GT failure path. Do not preserve a failed job in a custom paused state. Before an operation starts, ordinary resource and output checks prevent unsupported work. No additional random destruction, evaporation or recurring chip replacement mechanic is selected. Tanks provide short thermal buffering, not unlimited sustained heat disposal.

Operating intensity can trade higher output for worse EU efficiency and correspondingly greater heat per unit of useful work. Final equations must keep electrical work, heat carried by fluid and radiator rejection consistent. No detailed fluid-temperature or computational-fluid-dynamics simulation is required.

The radiator is a multiblock with finite cooling throughput scaled by environmental temperature, not a hardcoded orbital efficiency or location whitelist. Resolve environmental conditions through the shared authority in [[Define Celestial Capability Rules]]. The exact contribution of dimension, biome and local conditions remains an implementation and tuning question.

Use suitable space conditions as the reference efficiency of 100%, not a maximum. An environment that is too warm cannot passively restore the selected chilled coolant. A marginally cold environment can do so slowly. A sufficiently cold atmospheric environment may outperform the space reference, with atmospheric heat transfer considered when defining the model. The owner used Overworld as the intended too-warm example, not as an explicit dimension exclusion. Exact thresholds and atmospheric factors are not selected.

[[Define Space Factory Power Supply]] owns sunlight direction, solar walls and radiator exposure. Precise exposure checks remain open. The intended orbital installation has low ongoing cooling cost, while a warmer surface installation uses active refrigeration. This is an economic advantage, not an orbit-only Computer rule. Do not add per-frame ray tracing or a numerical pressure value used only as a planet identifier.

## Equipment And Recipe Research Boundary

### Production Dependencies

The Computer delivery includes hardware recipes for the controller, cluster, rack tiers, casing, radiator, connector and cable. [[Design Early Orbital Production Recipe Chain]] owns their CLC and fluoride feedstock chains. Concrete recipe composition and verification stay with the Computer delivery, not a parallel recipe assignment. Reuse its registered content rather than adding duplicate registrations.

Integrate recipes against the machine delivery's actual registered hardware and coolant identities. A working data loop without craftable equipment and available feedstocks is not a complete survival-production loop. Solar generation is an optional power source, not a blocker for operating or integrating the Computer. Required recipe-environment enforcement is a dependency of the qualifying feedstock chain.

The selected hardware recipes consume Space-Grade Alloy forms. [[Design Lunar Crater Processing Recipe Chain#Material Integration Contract]] owns their canonical material naming and the outstanding material-delivery dependency. Do not duplicate SGA registration inside Computer content or silently substitute a different metal.

### Checked TecTech Interfaces

Bounded source inspection on 2026-10-22 at GT5 revision 6eac02935d42b3ab13d341e4fe090b4403e15f60 found:

| Existing item | Function | Core recipe |
| --- | --- | --- |
| Optical Fiber Cable | Physical path for separate computation and Assembly Line recipe-data protocols | 8 Glass Fiber circuit parts, 8 Silver foils, 144 mB PTFE, LuV Assembler, 10 s, cleanroom |
| Optical Reception/Transmission Connector | Scalar computation input/output | Computer Casing, matching LuV bus, LuV circuit, 2 optical cables, 1296 mB Iridium, ZPM Assembler, 10 s, cleanroom |
| Assembly Line Reception/Data Bank Transmission Connector | Assembly Line recipe knowledge | EV Data Access Hatch plus the corresponding optical connector, 12000 EU/t, 102.4 s |
| Laser Vacuum Pipe | EU transport, not data | Optical Fiber Cable, Reinforced Glass, 2 Osmiridium foils, UV Assembler, 5 s, cleanroom |

The lowest registered laser endpoints are IV 256A, despite the UV pipe recipe. Each uses an IV hull, Diamond Lens, IV pump, two Tungstensteel wires, selector 1 and an IV emitter or sensor, at IV for 30 s. This does not establish an IV complete laser system. Ordinary GT power cables and energy hatches already support early electrical input.

Optical cables require matching paint, allow bends and stop traversal at junctions with other than two connections. The checked output traversal is bounded to about 1000 steps. Native cable paths are therefore point-to-point rather than a branched cluster network. Computation and recipe-data endpoints are distinct payload consumers even though they use the same cable class. Neither transports arbitrary typed Galaxia data unchanged.

Recipe anchors are tectech/loader/recipe/Assembler.java at lines 59, 1209, 1751, 2654 and 2710. MTEPipeData.getNext owns the two-connection restriction. No per-tier data-throughput limit was found in the inspected native methods. A cheaper recipe or a lower constructor tier does not create a slower interface by itself.

### Proposed Reuse Choice, Unapproved

Use ordinary electrical and fluid transport, separate point-to-point cluster data runs and a deliberate low-stage connection design. The owner supports fluoride-glass-derived transmission cables and matching new early connectors as part of Computer manufacture. Reusing the existing Optical Fiber Cable through an alternate recipe versus introducing a separate cable identity remains open. The former supplies the fully functional existing cable and reduces an ingredient cost elsewhere, while leaving other high-tier requirements intact.

Do not automatically add cheap recipes for the existing ZPM optical connectors. Those exact items are ingredients of Assembly Line connectors whose own recipe needs only 12000 EU/t. Distinct early connector identities can avoid that ingredient substitution, while reusing suitable connection implementation. Their packet support, controller compatibility and limits still need explicit definition. Reuse of classes alone does not prove a complete bidirectional cluster-control protocol.

Dedicated painted cable runs are the selected layout. Branched routing and switches are not required for the initial cluster connections. Native TecTech point-to-point behavior is relevant reuse evidence, but does not establish support for Galaxia's processing protocol.

Investigate actual TecTech data pipes, computation hatches and laser energy infrastructure before choosing reuse. Keep three services distinct:

- Native computation exchanged with TecTech consumers, deferred for this Computer
- Typed Galaxia input/output transported through satellites
- EU delivered through power infrastructure

Recipes for an early Computer must not accidentally require the late Quantum Computer's casing and connector chain. Conversely, cheaply reproducing an existing high-tier interface or packet type requires checking which consumers it unlocks.

The ordinary GT manufacturing baseline remains. Existing CLC electronics and fluoride optical components are candidate ingredients. EV, IV and LuV are the selected initial hardware tiers. Exact recipes, connector tiers, processing rates and cooling coefficients remain open. Earlier speculative cluster recipes must be reassessed for the separate-subsection layout and its power/fluid ports.

## Presentation

The proposed main GUI shows connected clusters, installed versus usable capacity, EU use, cooling-limited capacity and job queues. It shows input origin/type, output demand, actual returned service and concrete reasons for waiting. A cluster should show its own power and cooling state so the player can fix the actual bottleneck. No mode selector is needed for the initial data-processing-only service.

The player loop is build clusters, connect data/power/cooling, configure processing jobs, observe the constraint and expand the relevant infrastructure. It should remain stable in ordinary operation without repeated manual tuning.

## Decisions Still Needed

- Finalize controller and bounded cluster structures, port layouts and rack-tier mixing
- Select exact coolant fluids and radiator capacity/exposure rules, with native GT failure behavior for lost operating requirements
- Choose compatible cables/interfaces and actual early manufacturing recipes from source evidence
- Calibrate EV, IV and LuV processing capacity, electricity and cooling against real data consumers
- Resolve the prospecting workload and bonus questions in their own owner

## Provenance

On 2026-10-22, the owner selected a main controller multiblock with its own energy hatch and modest coordination EU use but no processing capacity. Dedicated information cables connect it to separately powered and cooled bounded cluster multiblocks. Each cluster contains individually craftable single-block racks, initially in EV, IV and LuV tiers. The same discussion narrowed initial delivery to Galaxia data processing and deferred TecTech computation until the end of Alpha or later because of cross-mod balance risk. Chilled-to-ordinary coolant, a closed loop, environment-dependent radiator throughput and directional orbital solar walls remain the cooling and power direction. Exact fluid and thermal settings remain open.

The inspected Galaxia main checkout at f2ccabeb5c90c051ec25be138a7e486dbc0b9136 has typed origin-aware buffers and delivery, but its endpoint record is tied to debug Automated Facility modules. Extend that existing responsibility for real physical machines. This evidence does not certify the current implementation worktrees.

Local research under ~/.agents/docs/Galaxia/docs/research records TecTech machinery and connector evidence. It is not approval of an upstream GT change.

## Related Decisions

- [[Define Prospecting Data Processing]]
- [[Define Satellite Link Distance Quality]]
- Collect Data Processor Topology Feedback
