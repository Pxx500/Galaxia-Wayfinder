---
type: implementation-issue
status: planned
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Observation and Research]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Define Satellite Link Distance Quality

## Accepted Contract

Distance quality makes relays useful without a hard range cutoff. Long direct links remain valid connections but consume more bandwidth per delivered unit. Quality is deterministic transmission airtime, not random packet loss.

| Class | Efficiency | Airtime cost | Star Map pattern |
| --- | --- | --- | --- |
| Local | 100% | 1x | Solid |
| Long-range | 50% | 2x | Regularly interrupted |
| Deep-space | 25% | 4x | More strongly interrupted, distinct from long-range |

Classify canonical orbital-space distance using shared balance thresholds: at or below the local threshold is Local, otherwise at or below the long-range threshold is Long-range, otherwise Deep-space. Exact threshold values remain tuning, independent of zoom, team, input order and client state.

`raw bandwidth used = delivered data rate * airtime cost`

A 1000 Kbps endpoint can therefore deliver 1000, 500 or 250 Kbps respectively. Excess production still obeys bounded-buffer/backpressure rules. Efficiency does not promise unlimited retained generation.

## Routing And Accounting

- Preserve existing demand priority and fairness.
- Prefer Local, then Long-range, then Deep-space routes. Within a class prefer available greater bottleneck capacity, allocating overflow where capacity remains.
- Weaker direct connections may carry overflow after better relay routes saturate.
- Source and destination pay their adjacent link's airtime cost.
- Charge each relay once for forwarded traffic, using the worse cost of its incoming/outgoing links, not twice.
- The concrete algorithm must scale without enumerating all possible paths. Use only the three fixed classes.

## Presentation

- Color retains green-to-red load meaning.
- Line pattern shows quality, with three distinguishable classes without reliance on color.
- Width/glow retain idle/active meaning. Animated signals retain direction/activity meaning.
- Link hover explains class, endpoint bandwidth, efficiency, airtime cost, effective rate, delivered load and raw usage. For example, a 1000 Kbps Deep-space link delivers up to 250 Kbps. A load of 180 Kbps uses 720 Kbps raw bandwidth.
- Body hover in satellite-link view temporarily shows local/long-range orbital-space range rings. This inspection overlay neither selects a hierarchy nor restricts zoom or enters body focus.
- A compact legend distinguishes line-pattern quality from load color. Exact dash lengths and tooltip copy/layout remain presentation tuning.
- Pattern rendering cost must remain bounded rather than unnecessarily scaling with screen line length.

## Authoritative State And Sampling

The existing satellite-network owner supplies classification, efficiency and airtime to topology, routing and synchronization. Clients receive the authoritative class and map it to visual style/text, without recomputing gameplay quality from rendered positions.

Use named thresholds and exact integer 1x/2x/4x multipliers. Re-evaluate moving geometry on the existing sampled network schedule, not each frame/tick. Boundary crossings apply at the next sample. Do not persist prior classes or add hysteresis.

The same orbital time, endpoint capacities, demand and body keys must yield the same classes and routing choices. Verify fairness and runtime cost when implementing. This accepted contract does not prescribe a new parallel network or certify implementation.

## Implementation Evidence

Read-only inspection on 2026-09-12 found topology candidates ordered by endpoint capacity/geometric distance in `registry/satellite/SatelliteNetworkCalculator.java:258`. `SatelliteDataJobService.java:126` recorded delivered rate rather than 1x/2x/4x airtime use. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. These paths did not establish the accepted distance-quality contract.
