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

# Computer

The Computer processes Galaxia network data using powered and cooled equipment.

## Structure

| Part | Role |
| --- | --- |
| Main controller | A multiblock with one controller block and its own energy hatch. It consumes modest EU, coordinates clusters and supplies no processing capacity. |
| Computing Cluster | A bounded multiblock with rack blocks, its own GT power input, chilled-coolant input, ordinary-coolant output and information connection. |
| Computing Rack | An individually craftable single block inside a cluster. Initial tiers are EV, IV and LuV. Operable racks supply processing capacity. |
| Radiator | A multiblock that restores ordinary coolant to its chilled state through a real pipe loop. |

Dedicated point-to-point information cables connect clusters to the controller. Spray paint controls neighboring cable connections, not a globally unique identity or a limit of one cluster per color. The cables carry neither power nor coolant. Clusters may share upstream utilities but retain individual connections.

A cluster should have one active controller and its capacity must not be counted twice. Ownership, endpoint layout and packet handling remain open. Disconnected, unloaded, unpowered or cooling-limited clusters cannot provide unavailable work. The Computer can operate on a planet or in orbit, without a vacuum or microgravity requirement.

## Data Processing

The initial Computer receives typed Galaxia data, performs an enabled job and supplies typed output to a requesting consumer. Producer, Computer and consumer may be at different locations. The existing team-owned satellite network transports input and output. The Computer owns conversion, local job selection and bounded processing state, not a second routing service.

Prospecting can be the first job. Its output retains celestial origin and benefits the correct object under [[Define Prospecting Data Processing]]. This is a job-specific restriction, not a requirement for every output to return to its producer. Automatic discovery of arbitrary processing chains and extra jobs are not required.

Jobs have installation-local priorities. An unapproved accounting proposal uses ordinary network input demands and output supplies for enabled jobs instead of a network-wide transformation planner. The Computer would advertise only demand it can service, with bounded storage. Exact allocation remains open.

## Initial Scaling And Deferred Specialization

Installed racks add capacity, but grouping them in a larger cluster grants no extra size-based efficiency multiplier. Exact cluster geometry, rack limits, tier mixing, processing rates and operating intensity remain open.

Specialized modules are deferred. A future module could replace racks in its own cluster, trading general capacity for better processing of one data type. Revisit this when enough useful jobs make the choice meaningful.

## Deferred TecTech Computation

TecTech-compatible computation may be reconsidered at the end of Alpha or later. Its Alpha inclusion is not committed. Cost and performance need assessment against Quantum Computer progression and other consumers. The initial Computer has no native computation service, mode selector or dual-mode allocation.

## Cooling

The closed loop is chilled coolant → cluster → ordinary coolant → radiator or powered chiller → chilled coolant. Cluster work consumes EU and cooling capacity. A radiator rejects heat where conditions permit, while a chiller spends electricity to restore coolant where passive cooling is unsuitable. Ordinary fluid is not lost. Equal input and output volumes are proposed, not finalized.

Cooling, power and hardware jointly limit throughput. Loss of operating requirements during work follows [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]], not a custom paused-work state. Resource and output checks apply before work starts. Tanks buffer briefly but cannot replace sustained heat disposal. No recurring chip replacement or additional random destruction is selected.

Operating intensity may trade efficiency for output and greater heat per useful work. Electrical work, transported heat and radiator rejection must remain consistent. The chosen coolant pair needs checks against existing heating, cooling and generator recipes to prevent unintended net energy. The returned fluid is not a new power source.

Radiator throughput depends on environmental temperature through [[Define Celestial Capability Rules]], not a location whitelist. Space is a 100% reference, not a ceiling. A warm environment may prevent passive restoration, while a sufficiently cold atmosphere may outperform the space reference. The Overworld is an intended warm example, not a dimension ban. [[Define Space Factory Power Supply]] owns sunlight and exposure direction.

Fluid identities, temperatures, heat capacity, circulation cost, rates, environmental factors and exposure checks remain open. Numerical fluid or pressure simulation is not required.

## Manufacture And Interfaces

The delivery includes craftable controller, cluster, racks, casing, radiator, connectors and cable. [[Design Early Orbital Production Recipe Chain]] owns CLC and fluoride feedstocks. [[Design Lunar Crater Processing Recipe Chain#Material Integration Contract]] owns the Space-Grade Alloy forms used by the hardware. Integrate with registered content rather than duplicating it. Solar generation is optional, not a prerequisite for operation.

Fluoride-glass-derived transmission cables and early connectors are supported. Whether to reuse the existing Optical Fiber Cable through another recipe or introduce a separate cable remains open. Cheap recipes for existing ZPM optical connectors need care because those items are Assembly Line connector ingredients. Reusing a cable class does not establish support for Galaxia's protocol. Ordinary GT power and fluid infrastructure remains the baseline.

Source inspection on 2026-10-22 at GT5 revision `6eac02935d42b3ab13d341e4fe090b4403e15f60` found painted, point-to-point optical cable paths and distinct computation and recipe-data endpoints. Neither carries arbitrary typed Galaxia data unchanged. Local research under `~/.agents/docs/Galaxia/docs/research` records the checked machinery and recipes.

## Initial Control Panel

One prospecting rule applies to all planets, with an enable switch and statistics. The initial panel has no separate per-planet rules or local priority controls. Data still retains its celestial origin and returns to the corresponding object. This limits the first UI, not the general job-priority model.

Source: Computer implementation discussion, 2026-10-27, conversation `01a16558-5f99-7223-85ff-43cfb63ffd79`.

## Proposed Extended Controls

The controller GUI shows connected clusters, installed and usable capacity, EU demand, cooling limits and job queues. Jobs show data type, origin, output demand, actual returned service and reasons for waiting. Each cluster exposes its own power and cooling state. Normal operation should not need repeated manual tuning or disposable processor insertion.

## Open Decisions

- Finalize controller and cluster structures, ports, rack limits and tier mixing.
- Select coolant fluids, radiator capacity and exposure rules.
- Choose cable and connector identities, communication protocol and hardware recipes.
- Calibrate capacity, electricity and cooling against real consumers.
- Resolve prospecting workload and bonuses in [[Define Prospecting Data Processing]].

## Gameplay Flow

Players build a controller and one or more clusters, fill the clusters with craftable racks, then connect each cluster to information, power and coolant. The controller coordinates the installation while racks process data. More operable racks provide more capacity, without a bonus merely for packing them into a larger cluster.

The network brings data to an enabled job and carries the processed result to a consumer. Prospecting keeps the celestial origin so the result benefits the right object. Processing depends on power and chilled coolant, so players can expand the relevant infrastructure when it becomes the constraint.

Location changes the supporting infrastructure rather than eligibility to build the Computer. An orbital installation can combine continuous solar power with passive radiator cooling, but needs materials transported to orbit. A surface installation can use the base's existing power and logistics. Warm environments need powered chilling, while a sufficiently cold planet can support passive cooling and may outperform the orbital reference. Adding processing hardware therefore also means providing enough power and cooling to use it.
