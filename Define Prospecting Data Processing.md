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

## Accepted Decision

Prospecting is a sustained network pipeline: `Prospecting Satellites -> Data Processing -> originating celestial object`. It is not permanent accumulated survey progress. Processing may be centralized or distributed anywhere a complete communication route exists. These requirements do not certify an implemented bonus pipeline.

## Data And Processing Ownership

- Each satellite produces a fixed Raw Prospecting Data rate for its orbital body. Raw and processed data are typed network state in small bounded buffers, never physical items or freight.
- Pool data by `SatelliteDataType + origin CelestialObjectKey`, not individual satellite. All satellites at one origin contribute to its shared raw pool. Processing and successfully returned output aggregate for that origin, without satellite-to-satellite pairing.
- Data from one object cannot benefit another. Planetary bonus consumers must request exact-origin processed data. Any-origin demand may serve other consumers.
- Use the general Data Processor capability, not a separate Prospecting-only machine/path. It accepts typed jobs with finite shared throughput and per-job conversion, costs and output rules. Alpha first needs Raw-to-Processed Prospecting conversion.
- [[Define Data Processor Machine Topology]] owns expandable EU-powered multiblocks, structural capacity, tiers, operating intensity and installation-local configuration. Multiple installations are allowed. No inserted processor-item requirement is implied.
- Jobs are keyed by type and origin. Active jobs share throughput by default. Players may disable jobs and change priority. Higher priority is served first, while equal-priority jobs share the remainder rather than using insertion order.

## Working Effects And Measurement

Sustained processed-and-returned throughput is normalized into fractional satellite-equivalent streams. All effects scale linearly.

| Working Alpha setting | Value |
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
- Do not consume raw input unless the processed result fits the bounded output path. When downstream capacity is absent, pause or skip new work rather than building unbounded queues.
- Backlog must not create bonuses above the actual bounded pipeline rate.
- Credit delivered amounts only once. Several matching consumers cannot each receive one transfer's full amount.
- A concrete consumer's finite demand is shared across all sources, including local delivery that consumes no satellite bandwidth.
- Only accepted data leaves source buffers. Other data remains subject to bounded storage/backpressure.
- Disable/remove/reconfigure updates eligible demand. Data and deliveries remain team-isolated.

## Presentation And Open Tuning

The body's satellite hover shows pooled raw generation, processed data successfully returned and currently applied bonuses. It does not assume one processor or diagnose the global bottleneck. Players inspect routing, bandwidth, processing and local configuration themselves.

Buffer sizes, exact pause mechanics, throughput/tier/EU curves, measurement-window length and rounding increment remain tuning. The table records working Alpha values, not immutable balance.

## Implementation Evidence And Provenance

Read-only inspection on 2026-09-12 found typed origin keys and concrete-sink delivery in `registry/satellite/SatelliteDataJobService.java:114,151`, under `src/main/java/com/gtnewhorizons/galaxia/`. Only accepted data was drained and exact-origin demand was prioritized. `SatelliteDataKey` carried type and optional origin. `SatelliteDataType` contained COMMUNICATION, PROSPECTING and RESEARCH.

Those debug-oriented transport paths do not establish Raw-to-Processed conversion, production machinery, returned-throughput windows or extraction bonuses. Discovery workers are a separate path.

The flow-accounting rules originate in September 2026 satellite-runtime decisions. The 2026-09-16 machine-topology direction supersedes inserted-processor assumptions.

## Related Decisions

- [[Define Alpha Research and Production Floor]]
- [[Define Alpha Celestial Knowledge Layers]]
