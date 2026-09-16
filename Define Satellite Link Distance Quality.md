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

## Goal

Make satellite-link distance a meaningful network constraint without making long links unusable or nondeterministic.

Long direct links should remain valid fallback connections, but an efficient relay network should deliver more data with the same satellite bandwidth. This creates a reason to build relay nodes without introducing a hard range limit.

## Distance Quality

Every link receives one deterministic quality class from the orbital-space distance between its endpoints:

| Quality | Efficiency | Airtime cost | Star Map line |
| --- | ---: | ---: | --- |
| Local | 100% | 1x | Solid |
| Long-range | 50% | 2x | Regularly interrupted |
| Deep-space | 25% | 4x | More strongly interrupted, visually distinct from long-range |

The two distance boundaries are shared balance constants. They do not depend on screen zoom, team, input order, or client state. Their exact values are intentionally left for balance tuning during implementation and can change later without changing the model.

Boundary behavior is explicit and deterministic:

```text
distance <= local threshold       -> Local
distance <= long-range threshold  -> Long-range
otherwise                         -> Deep-space
```

Quality represents transmission time, not packet loss:

```text
raw bandwidth used = delivered data rate x airtime cost
```

For example, a `1000 Kbps` satellite can deliver `1000 Kbps` over a local link, `500 Kbps` over a long-range link, or `250 Kbps` over a deep-space link. Quality does not randomly destroy packets. This is not a promise to retain unlimited excess generation. Prospecting data still obeys its bounded-buffer and sustained-throughput contract.

## Routing Behavior

- Preserve the existing demand priority and fairness rules.
- Prefer local routes, then long-range routes, and use deep-space routes last.
- Within one quality class, prefer available routes with greater remaining bottleneck capacity and allocate overflow where capacity remains. Choose the concrete routing algorithm against the current network implementation.
- Route selection must scale without enumerating every possible path.
- Allow weaker direct links to carry overflow after better relay routes are saturated.
- Charge a source and destination using the airtime cost of their adjacent route link.
- Charge a relay node once for forwarded traffic, using the worse airtime cost of its incoming and outgoing links. Passing through a relay must not consume the relay's bandwidth twice.

Example: if a local relay route can deliver most of a transfer, it is filled first. Any remaining demand may still use the direct deep-space link at `4x` airtime cost. The direct connection is therefore useful, but adding good relay nodes increases total throughput.

## Star Map Communication

Each visual channel should keep one meaning:

- **Color** remains the current green-to-red load indicator.
- **Line pattern** communicates distance quality: solid for local, one fixed interruption rhythm for long-range, and a clearly stronger or double-interruption rhythm for deep-space. Exact dash lengths are presentation tuning, but the three classes must remain distinguishable without color.
- **Width and glow** continue to distinguish idle and active links.
- **Animated signals** continue to show traffic direction and activity.

Line-pattern rendering must have bounded practical cost rather than scaling unnecessarily with on-screen line length.

Hovering a link should explain the calculation directly, for example:

```text
Deep-space link
Endpoint bandwidth: 1,000 Kbps
Distance efficiency: 25%
Airtime cost: 4x
Effective data rate: 250 Kbps
Current delivered load: 180 / 250 Kbps
Raw endpoint bandwidth used: 720 Kbps
```

Hovering a body in the satellite-link view should temporarily show the local and long-range distance boundaries as orbital-space range rings. This is an inspection overlay, not hierarchy selection, so it must not restrict zoom or enter a body-focused view. A compact legend should explicitly state that line pattern means distance quality while color means current load.

## Determinism and Performance

- Calculate quality from canonical orbital positions and named thresholds with exact integer `1x`, `2x`, and `4x` multipliers.
- Process only the fixed three quality classes; do not enumerate every possible path.
- Re-evaluate moving orbital geometry on the existing sampled network schedule, not every frame or tick. Crossing a boundary changes the class at the next sample.
- Do not persist a previous quality class and do not add hysteresis. Quality is a pure result of the sampled canonical positions and thresholds.
- The same orbital time, endpoint capacities, demand, and body keys must produce the same quality classes and routing decisions.

## Ownership Contract

- The existing satellite-network domain owner must be the single source of truth for distance classification, efficiency, and airtime cost.
- Topology, routing, synchronization, and presentation consume that same authoritative result rather than maintaining parallel calculations.
- The client receives the authoritative quality class needed for presentation and only maps it to line style and explanatory text. It must not independently recalculate gameplay quality from rendered positions.
- Implementation should discover and deepen the current owners, scheduler, snapshots, and network messages in the codebase. This note intentionally does not freeze current class names or file structure.

## Deferred Tuning and Implementation

Read-only inspection on 2026-09-12 found topology candidates ordered by endpoint capacity and geometric distance in `registry/satellite/SatelliteNetworkCalculator.java:258`. Transfer usage in `SatelliteDataJobService.java:126` records delivered rate, not the accepted 1x/2x/4x airtime costs. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`. The inspected network paths do not implement the accepted distance-quality contract. Keep it as implementation work, not a fresh gameplay question.

Distance thresholds and exact line styling remain tuning choices. The example tooltip illustrates the quantities to explain, not mandatory copy or layout. Verify routing fairness and actual runtime cost when implementing this contract. Historical algorithm suggestions do not prescribe a new parallel routing system.
