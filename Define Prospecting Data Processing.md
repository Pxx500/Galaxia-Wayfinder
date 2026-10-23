---
type: wayfinder-ticket
ticket_type: grilling
status: open
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
secondary_areas:
  - Area - Automation and Infrastructure
blocked_by: []
claimed_by: wayfinder
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/grilling
---

# Define Prospecting Data Processing

## Accepted Decision

Prospecting is a sustained network pipeline: `Prospecting Satellites -> Data Processing -> originating celestial object`. It is not permanent accumulated survey progress. Processing may be centralized or distributed anywhere a complete communication route exists. These requirements do not certify an implemented bonus pipeline.

## Reopened Service Economy

The owner wants computation and, where appropriate, communication throughput to provide the meaningful investment and operating limits. Cheap permanent satellites producing free input must not make a trivial computer an unlimited extraction upgrade. Diminishing returns are accepted as the benefit-scaling direction. The exact curve and computer specification remain open. This supersedes linear bonus scaling as the target economy.

Recommended Alpha model, awaiting approval: raw generation, transport and processing have finite throughput. Computing sections provide installed capacity, and higher operating intensity trades worse EU efficiency for more throughput. Apply a diminishing-return curve once to aggregate successfully returned data for the same team and origin. Splitting processing across machines must not repeatedly grant the cheap beginning of the curve.

Tier progression can increase production capacity faster than nominal voltage. A fixed cost in obsolete components must not be mistaken for a durable progression barrier. Linear capacity additions may still be useful inside a tier, but the useful benefit and higher-tier equipment economy must be considered together.

A logarithmic benefit curve is one candidate. Equal additional bonus steps would require illustrative relative data rates of 1, 3, 7 and 15. These are examples, not chosen rates, bonus percentages or an accepted formula. Costs need not also grow exponentially at every pipeline stage.

This can create choices between more computing capacity and higher EU use, between serving another origin and increasing an existing bonus, and between central power-rich processing and local processing with lower transmission burden. The modular Computer direction adds a closed coolant loop and radiator infrastructure under [[Define Data Processor Machine Topology]]. Exact coolant identities and thermal calibration remain open. A near-star data center is a possible strategy, not an Alpha location requirement. No minigame or new satellite tier is approved by this proposal.

The remaining major choice is whether sustaining a given percentage bonus requires more data as the baseline extraction workload at that origin grows. Shared workload normalization is proposed, but its consumer accounting is not yet selected. Satellite generation and capacity progression must be balanced against actual processor and mining value.

## Data And Processing Ownership

- Each satellite produces a fixed Raw Prospecting Data rate for its orbital body. Raw and processed data are typed network state in small bounded buffers, never physical items or freight.
- Pool data by `SatelliteDataType + origin CelestialObjectKey`, not individual satellite. All satellites at one origin contribute to its shared raw pool. Processing and successfully returned output aggregate for that origin, without satellite-to-satellite pairing.
- Data from one object cannot benefit another. Planetary bonus consumers must request exact-origin processed data. Any-origin demand may serve other consumers.
- Use the Computer's general data-processing capability, not a separate Prospecting-only machine/path. It accepts typed jobs with finite shared throughput and per-job conversion, costs and output rules. Generic producer A and consumer B need not be at the same location. Prospecting specifically preserves its origin constraint. Alpha first needs Raw-to-Processed Prospecting conversion.
- [[Define Data Processor Machine Topology]] owns the powered controller multiblock, bounded independently powered/cooled clusters and single-block EV/IV/LuV rack hardware. It owns structural capacity, tiers and installation-local configuration. Multiple installations are allowed. No inserted processor-item requirement is implied.
- Jobs are keyed by type and origin. Active jobs share throughput by default. Players may disable jobs and change priority. Higher priority is served first, while equal-priority jobs share the remainder rather than using insertion order.

## Previous Linear Working Baseline, Under Review

The previous working baseline normalized sustained processed-and-returned throughput into fractional satellite-equivalent streams and scaled effects linearly. The reopened service-economy decision may replace this mapping. The following values preserve the prior proposal, not a final instruction to implement linear scaling.

| Previous working setting, under review | Value |
| --- | --- |
| Miner speed per sustained satellite-equivalent | +10% |
| Expected ore output per sustained satellite-equivalent | +5% |
| Floor increment for each effect | One percentage point, configurable |
| Measurement window | 20 ticks, one second at 20 TPS |

Floor speed and expected output independently. For example, 0.5 satellite-equivalent gives raw +5% speed and +2.5% output, applied as +5% and +2% with the one-point increment. Below-increment effects become zero, never round up.

Expected output uses uncapped stochastic rounding. The multiplier's integer part guarantees that many batches, while the fractional part is the chance of one extra batch.

Network transfer, buffering and processing remain tick-granular. Accumulate successfully returned exact-origin processed data over a complete window, calculate/floor effects at its boundary and hold them for the following window. No interpolation is required. Using the previous full window prevents full bonuses from enabling processing only on an extraction work tick.

[[Define Prospecting Effects by Extraction System]] owns how this applies to all Galaxia extraction and relevant GT5 integrations. Specific machine behavior is deferred there, not inferred from generic miner wording.

## Bounded Flow And Delivery Accounting

- Small local buffers absorb short timing differences, not long-term data storage. Every stage applies backpressure before downstream overflow.
- Do not consume raw input unless the processed result fits the bounded output path. When downstream capacity is absent, do not start new work or build unbounded queues. This is pre-start backpressure, not retained-progress failure recovery. Running GT-like operations follow [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]].
- Backlog must not create bonuses above the actual bounded pipeline rate.
- Credit delivered amounts only once. Several matching consumers cannot each receive one transfer's full amount.
- A concrete consumer's finite demand is shared across all sources, including local delivery that consumes no satellite bandwidth.
- Only accepted data leaves source buffers. Other data remains subject to bounded storage/backpressure.
- Disable/remove/reconfigure updates eligible demand. Data and deliveries remain team-isolated.

## Presentation And Open Tuning

The body's satellite hover shows pooled raw generation, processed data successfully returned and currently applied bonuses. It does not assume one processor or diagnose the global bottleneck. Players inspect routing, bandwidth, processing and local configuration themselves.

Buffer sizes, work scheduling, throughput/tier/EU curves, measurement-window length and rounding increment remain tuning. Failure behavior is not an open custom-pause design. The table preserves the previous linear baseline for comparison, not current instructions to implement it unchanged.

## Implementation Evidence And Provenance

Read-only inspection on 2026-09-12 found typed origin keys and concrete-sink delivery in `registry/satellite/SatelliteDataJobService.java:114,151`, under `src/main/java/com/gtnewhorizons/galaxia/`. Only accepted data was drained and exact-origin demand was prioritized. `SatelliteDataKey` carried type and optional origin. `SatelliteDataType` contained COMMUNICATION, PROSPECTING and RESEARCH.

Those debug-oriented transport paths do not establish Raw-to-Processed conversion, production machinery, returned-throughput windows or extraction bonuses. Discovery workers are a separate path.

The flow-accounting rules originate in September 2026 satellite-runtime decisions. The 2026-09-16 machine-topology direction supersedes inserted-processor assumptions.

## Related Decisions

- [[Define Alpha Research and Production Floor]]
- [[Define Alpha Celestial Knowledge Layers]]
