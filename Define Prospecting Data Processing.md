---
type: wayfinder-ticket
ticket_type: grilling
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Prospecting Data Processing

## Question

What Alpha capability converts Raw Prospecting Data into Processed Prospecting Data, which facilities may host it, and which costs and throughput constraints make local versus centralized processing a meaningful player choice?

## Established Input

- A Prospecting Satellite generates Raw Prospecting Data about the celestial object it orbits.
- Raw data travels through the communication network to a processing capability.
- Processed Prospecting Data must return through the network to the originating celestial object before mining there receives an efficiency benefit.
- The processing implementation may be a computer, dedicated Data Processor, facility module, or another concept selected by this ticket.
- Each satellite produces a fixed Raw Prospecting Data rate. Sustained processed-and-returned throughput is measured in satellite-equivalent streams.
- Working Alpha tuning grants `+10%` planet-wide miner speed and `+5%` expected ore output per sustained satellite-equivalent stream.
- Expected ore output uses uncapped stochastic rounding: the integer part of the multiplier is guaranteed and its fractional part is the chance for one additional output batch.
- Satellite Raw Prospecting Data buffers are bounded. Prospecting is an ongoing scan and computation pipeline whose sustained end-to-end uptime determines the active bonus; it is not permanent accumulated survey progress.
- Prospecting is intended to affect all Galaxia extraction systems and relevant GT5 integrations, but machine-specific effects are deferred to [[Define Prospecting Effects by Extraction System]].

## Decisions in Progress

- Prospecting processing is a network-wide capability rather than a local requirement at the scanned celestial object.
- Any eligible processor connected through a complete communication route may process incoming Raw Prospecting Data, allowing centralized or distributed processing layouts.
- The complete active route is `Prospecting Satellite -> processing capability -> originating celestial object`.
- Raw and processed Prospecting Data are origin-bound. Data generated about one celestial object may only contribute to the prospecting bonus on that same object.
- A Prospecting Satellite therefore cannot consume or apply Prospecting Data originating from another planet, moon, asteroid, or other celestial object.
- Raw and processed Prospecting Data exist only as typed network state in bounded buffers. They cannot be extracted, transported, or stored as physical items.
- Planetary prospecting bonuses require exact-origin data consumption. A generic any-origin demand may exist for other data consumers, but it cannot apply a prospecting bonus to a different celestial object.
- Processing belongs to a general Data Processor capability rather than a Prospecting-only machine or parallel processing path.
- A Data Processor accepts typed data jobs and exposes finite shared processing throughput. Each data-job type may define its own conversion rule, processing cost, and output behavior.
- Alpha initially requires the Prospecting job that converts Raw Prospecting Data into Processed Prospecting Data. Future Research or other data jobs may reuse the same processing owner without inheriting Prospecting-specific rules.
- Data Processing requires player-built, network-connected machine infrastructure, but its physical topology is not selected by this ticket.
- The processing infrastructure consumes EU while working and contains player-installed processor hardware.
- Total processing throughput derives from both the number of installed processors and their technology tiers.
- Installed processors are persistent capital hardware rather than per-job consumables.
- Whether processor hardware belongs to an expandable modular multiblock, a pool of smaller cooperating machines, or another topology is deferred to [[Define Data Processor Machine Topology]] after [[Collect Data Processor Topology Feedback]].
- Exact slot counts, tier values, throughput curves, EU tuning, and the configuration scope for job priorities depend on that topology and remain open.
- Regardless of physical topology, only successfully returned output aggregates in the shared origin pool.
- Processing work is scheduled by jobs keyed by `SatelliteDataType + origin CelestialObjectKey`.
- By default, active jobs share available processing throughput. The player may disable a job or change its priority.
- Higher-priority jobs receive available throughput before lower-priority jobs. Jobs at the same priority share the remaining throughput rather than depending on insertion order.
- Returned exact-origin Prospecting throughput is normalized into fractional satellite-equivalent streams and every prospecting effect scales linearly from that value.
- Each resulting effect percentage is rounded down to a configurable sensible increment before application and display. The working Alpha increment is one percentage point.
- Rounding is applied independently to miner speed and expected output. For example, `0.5` satellite-equivalent produces raw effects of `+5%` speed and `+2.5%` expected output, which become `+5%` and `+2%` with a one-point increment.
- A raw effect below the configured increment contributes `0%`; rounding never increases the benefit above sustained returned throughput.
- Network transfer, buffering, and processing continue at tick granularity, while applied Prospecting effects use a working measurement window of `20` ticks.
- During each window, the system accumulates Processed Prospecting Data successfully returned to each exact origin object. At the boundary it computes and floors that object's effects, then holds them constant for the following window.
- No additional interpolation is required. The window length remains a tuning value, with one second as the Alpha default.
- Windowed evaluation prevents pulse exploitation: enabling processing only on an extraction machine's work tick cannot grant the full bonus because the machine uses the result of the preceding complete measurement window.
- Satellite data is pooled by `SatelliteDataType + origin CelestialObjectKey`, not tracked per producing satellite.
- All Prospecting Satellites orbiting the same celestial object contribute Raw Prospecting Data to one shared origin pool. Processing demand and returned Processed Prospecting Data are likewise aggregated for that origin.
- Planet-wide effects depend on the origin pool's total successfully processed-and-returned throughput; no source-satellite-to-receiver-satellite pairing exists.
- The data ecosystem must remain a bounded-flow pipeline rather than a storage system. Satellites, Data Processors, and relevant network endpoints expose only small local buffers sized to absorb short timing differences.
- Every stage applies backpressure before its downstream buffer overflows. A Data Processor does not consume Raw Prospecting Data unless it can place its result into the bounded processed-output path.
- When a producing stage has no downstream capacity, new work pauses or is skipped rather than growing an unbounded queue. Exact buffer sizes and pause mechanics are implementation and balance tuning.
- Buffered backlog must never create a returned-throughput bonus above the actual bounded pipeline rate; data storage is not a source of burst prospecting power.
- The satellite hover widget for a celestial object presents the pooled Prospecting result: Raw Data generated by its satellites, Processed Data successfully received back, and the currently applied planet-wide bonuses.
- The UI does not diagnose a global bottleneck or assume one Data Processor. When returned data is below generated data, the player determines whether the limitation is network bandwidth, processing capacity, routing, or local machine configuration by inspecting those systems.

## Resolution

- Prospecting uses the network path `Prospecting Satellites -> Data Processing -> originating celestial object`; processing may occur anywhere reachable by a complete communication route.
- Raw and Processed Prospecting Data are non-item, origin-bound network state pooled by `SatelliteDataType + origin CelestialObjectKey`. Data from one object cannot buff another.
- Prospecting is the first typed job of a general Data Processing capability rather than a separate processing stack.
- Data Processing consumes EU and scales through persistent processor hardware, but the physical machine topology is split into [[Collect Data Processor Topology Feedback]] and [[Define Data Processor Machine Topology]].
- Small bounded buffers and backpressure prevent the pipeline from becoming data storage or producing backlog bursts.
- Successfully returned throughput scales both Prospecting effects linearly, floors each to a working one-percentage-point increment, and is evaluated in `20`-tick windows to prevent pulse exploitation.
- The satellite hover widget shows pooled generated data, successfully returned data, and active bonuses. It does not automatically diagnose the limiting processor, route, or bandwidth.
- `SatelliteDataKey` already provides the required data-type and origin-object identity; planetary bonus demand must use the exact origin.

## Data Delivery Accounting

Retained from the September 2026 satellite-runtime decisions during the 2026-09-11 cleanup:

- A delivered amount is credited only once. Several matching consumers must not each receive the full amount of one transfer.
- Each concrete consumer's finite demand is shared across all sources serving it. Local delivery obeys the same accounting even when it uses no satellite bandwidth.
- Only accepted data leaves a source buffer. Unaccepted produced data stays within the bounded-buffer and backpressure rules above.
- Disabling, removing, or reconfiguring a consumer updates its eligible demand. Data and delivery state remain isolated between teams.

These are flow-accounting requirements, not a new persistent demand store or a replacement for the accepted origin pools.

## Verified Implementation Alignment

Inspection on 2026-09-12 confirms typed origin keys and concrete-sink delivery in the existing debug-oriented data pipeline. `registry/satellite/SatelliteDataJobService.java:114` drains only accepted data, and `matchingConsumers` at line 151 prioritizes exact-origin consumers. These paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

`SatelliteDataType.java:3` currently contains COMMUNICATION, PROSPECTING, and RESEARCH. The inspected service does not establish the accepted Raw-to-Processed conversion, installed processor hardware, returned-throughput windows, or extraction bonuses. Discovery workers are a separate path. Data Processor topology therefore remains genuinely open, and the full prospecting gameplay pipeline must not be marked implemented merely because data transport exists.

- `SatelliteDataKey` already identifies satellite data by `SatelliteDataType` and an optional `CelestialObjectKey origin`.
- Produced data retains its real origin, while consumers may request either a specific origin or any origin; exact-origin demand is prioritized when both match.
- This existing origin key supports the decided same-object bonus contract, but the bonus consumer must use exact-origin demand.

## Related Topics

- Audit Galaxia Concept Map
- Define Alpha Research and Production Floor
- Define Alpha Celestial Knowledge Layers
