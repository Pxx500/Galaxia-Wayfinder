---
type: source
status: deferred
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Factorio Signal System Research

This note preserves external research and historical Galaxia proposals for future signal-system discussion. It is not an accepted Alpha implementation specification. Current source-identity and Station-availability requirements are maintained in the active logistics decision notes. Detailed logical-network, port, and combinator proposals below require a later product review before use.

> Historical or reference record. Read dated outcomes and later corrections before using earlier proposals. This record is not an active instruction to execute its plan, and its code or verification claims have not been revalidated by the 2026-09-10 vault consolidation.

Imported: 2026-09-01

## Terminology and ambiguity

Factorio uses two related but distinct systems. A logistic network moves items with logistic and construction robots between roboports and logistics chests. A circuit network broadcasts signals over red and green wires so connected receivers can be controlled. The phrase “logistic signals” is therefore ambiguous. It may mean logistic-network contents and requests, or circuit-network signals sourced from logistic entities. Sources: [Logistic network](https://wiki.factorio.com/Logistic_network), [Circuit network](https://wiki.factorio.com/Circuit_network).

## Logistic networks

- A logistic network is a set of logistics chests and logistic robots covered by one or more connected roboports. Roboport logistic coverage defines which entities belong to the network and which robots can service them. Separate networks do not share robots or inventory. Source: [Logistic network](https://wiki.factorio.com/Logistic_network).
- Chests have distinct roles. Active and passive providers offer items, storage receives items without another destination, requester chests request up to configured amounts, and buffer chests combine requesting and providing behavior. These are logistics state and robot work orders, not circuit signal channels. Source: [Logistic network](https://wiki.factorio.com/Logistic_network).
- A roboport can expose logistic-network contents and robot statistics to the circuit network. This is the bridge where “logistic contents” become circuit signals. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).

## Circuit networks and transmission

- Circuit networks are built with red or green wire. Connected senders broadcast amounts or other data on named signal channels, and receivers use those values for control. Every network has channels for item and fluid signals plus virtual signals. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).
- Red and green are separate wire colors and channels. A device reading both colors sums the values from both inputs. A device can have separate red and green connections, so color is part of the circuit topology and input semantics. Sources: [Red wire](https://wiki.factorio.com/Red_wire), [Green wire](https://wiki.factorio.com/Green_wire), [Circuit network](https://wiki.factorio.com/Circuit_network).
- Circuit connectivity is physical. Wires connect entities and combinators into networks. Logistic coverage is a different spatial relation defined by roboport areas. This distinction is essential if Galaxia intends persistent machine-to-machine control rather than a global projection of inventory. Sources: [Circuit network](https://wiki.factorio.com/Circuit_network), [Logistic network](https://wiki.factorio.com/Logistic_network).
- Factorio’s circuit page documents one tick, equal to 1/60 second, of latency from arithmetic and decider combinator input to output. This timing is a Factorio implementation detail, but explicit signal update timing is an essential design concern for any Galaxia control network. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).

## Signals and virtual signals

- Item and fluid signals represent typed channels. Virtual signals provide user-defined channels that are not tied to an item or fluid. The circuit network also provides wildcard selectors such as Everything, Anything, and Each for combinator conditions. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).
- The exact count of virtual signals and the names available are Factorio-specific UI/data details. The portable architectural idea is a typed signal key space with optional user-defined keys, not the specific Factorio signal catalogue. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).

## Conditions, combinators, and machine behavior

- Receivers can be configured with circuit conditions. Logistic-network conditions and circuit conditions can both apply, and the documented behavior is logical AND between them. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).
- A constant combinator continuously emits configured signal values to connected wire networks and can be enabled or disabled in its GUI. This is the canonical persistent source of machine-control signals. Source: [Constant combinator](https://wiki.factorio.com/Constant_combinator).
- An arithmetic combinator reads signals from red and green inputs, applies one arithmetic or bitwise operation, and emits the result. Source: [Arithmetic combinator](https://wiki.factorio.com/Arithmetic_combinator).
- A decider combinator compares an input signal with another signal or constant, supports configurable conditions, and emits normal or else outputs depending on the result. Multiple conditions can be combined with AND or OR. Source: [Decider combinator](https://wiki.factorio.com/Decider_combinator).
- Machines expose selected outputs and control inputs rather than sharing arbitrary global state. The source circuit page lists examples including inserters, belts, lamps, pumps, train stops, roboports, and other devices. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).

## Architectural takeaways for Galaxia

Essential concepts to carry over:

1. Separate logistics state from control signals. Inventory contents and requests are one domain. Signals are a published, typed control surface derived from devices or combinators.
2. Give signals explicit ownership and transmission scope. Factorio’s scope follows physical wire connectivity for circuit networks and roboport coverage for logistics. A Galaxia global signal bus would be a deliberate departure, not an implied consequence of inventory state.
3. Model persistent signal values and update behavior. Sources can emit continuously, receivers read current values, and derived signals can have defined latency. The precise one-tick delay is Factorio-specific, but deterministic update semantics are not.
4. Keep conditions at the receiver or control boundary. A machine can combine logistic and circuit conditions. This supports local authority checks and avoids treating a supply/demand projection as a command.
5. Use typed signal keys and permit user-defined or virtual channels only if the product needs them. Factorio’s item, fluid, and virtual channels are a concrete implementation of this idea.

Factorio-specific details that should not be copied without a product decision include roboport geometry, robot charging and scheduling, exact virtual-signal names, red/green color summation rules, combinator operation sets, and the one-tick combinator latency.

## Sources checked

- [Official Factorio Wiki: Logistic network](https://wiki.factorio.com/Logistic_network), retrieved 2026-09-01. Checked network membership, chest roles, roboport coverage, robot behavior, and logistic-to-circuit exposure.
- [Official Factorio Wiki: Circuit network](https://wiki.factorio.com/Circuit_network), retrieved 2026-09-01. Checked signal channels, virtual signals, physical connectivity, receiver conditions, logistic contents output, machine I/O examples, and combinator latency.
- [Official Factorio Wiki: Red wire](https://wiki.factorio.com/Red_wire), retrieved 2026-09-01. Checked red-wire circuit connection semantics and page identity.
- [Official Factorio Wiki: Green wire](https://wiki.factorio.com/Green_wire), retrieved 2026-09-01. Checked green-wire circuit connection semantics and page identity.
- [Official Factorio Wiki: Constant combinator](https://wiki.factorio.com/Constant_combinator), retrieved 2026-09-01. Checked continuous output behavior.
- [Official Factorio Wiki: Arithmetic combinator](https://wiki.factorio.com/Arithmetic_combinator), retrieved 2026-09-01. Checked input channels, operations, and output behavior.
- [Official Factorio Wiki: Decider combinator](https://wiki.factorio.com/Decider_combinator), retrieved 2026-09-01. Checked conditions, normal and else outputs, and multi-condition behavior.

No Factorio page named “Virtual signal” was found at `https://wiki.factorio.com/Virtual_signal` during retrieval. Virtual-signal behavior was therefore sourced from the virtual-signals section of the official [Circuit network](https://wiki.factorio.com/Circuit_network) page.

## 2026-09-01 clarification: emitter provenance is required in Galaxia

The Galaxia requirement is stronger than the Factorio model: if a station emits a signal contribution, the global system must retain the exact emitting station identity alongside that contribution. This is a binding Galaxia requirement, not an optional Factorio-inspired detail.

- Factorio circuit networks expose signal values on channels. When multiple connected sources emit the same signal, the documented circuit behavior combines values on the network, including summing red and green inputs when a receiver reads both. The exposed value is therefore an aggregate channel value, not a per-emitter contribution list. Source: [Circuit network](https://wiki.factorio.com/Circuit_network).
- Factorio logistic networks similarly expose aggregate logistics state such as network contents and robot statistics when a roboport sends those values to the circuit network. The official description does not expose a stable source identity for each item count in that signal. Source: [Circuit network](https://wiki.factorio.com/Circuit_network), [Logistic network](https://wiki.factorio.com/Logistic_network).
- The official pages describe physical membership, senders, receivers, and channel values, but do not document emitter identity as part of a signal value. This is an evidence boundary, not proof that no internal diagnostic API could exist.

Consequences for Galaxia:

1. A global signal value must be represented as provenance-bearing contributions, for example `(emitterStationId, signalKey, value, update metadata)`, with aggregation as a derived view rather than the only stored state.
2. Removing or changing one station’s output must subtract or replace that station’s contribution without reconstructing the whole network from an anonymous total.
3. Queries and machine conditions may consume an aggregate projection, but diagnostics, authority checks, persistence, and conflict resolution must retain the station identity.
4. A Factorio-like channel sum is useful as a presentation or control projection only after provenance is preserved. It cannot be the canonical Galaxia state.

This provenance requirement changes the architectural comparison: Galaxia may borrow Factorio’s separation of logistics state and control signals, typed channels, explicit scope, and deterministic updates, but it must not copy Factorio’s anonymous aggregate signal representation.

## Durable Galaxia concept

Galaxia's long-term target is not a copy of one isolated Factorio subsystem. It is one coherent automation domain that combines the useful roles of Factorio's logistic network, circuit network, signals, and machine conditions.

The domain should eventually support:

- resource availability and demand
- typed machine and inventory signals
- user-defined control signals
- conditions that control machine behavior
- derived signals and combinator-like behavior
- physical logistics planning and delivery driven by network facts

One coherent domain does not imply one class. Signal state, condition evaluation, logistics planning, and physical delivery have different responsibilities. They should share one canonical model and remain separate internal modules.

## Logical network partitioning

Factorio separates signals through disconnected wire graphs. Galaxia has one global technical system and no equivalent physical cable topology on the star map. It therefore needs user-selectable logical networks that provide the same isolation.

"Global" describes the infrastructure owner. It does not mean that all signals share one aggregate.

Two contributions are eligible to aggregate only when they have:

- the same team
- the same logical network
- the same signal key

Logical network and signal key are distinct concepts:

- logical network identifies the independent signal space, equivalent to one disconnected Factorio wire network
- signal key identifies what a value means inside that network, such as an item, fluid, status, or virtual control signal

The domain permits an unbounded number of logical networks. Only created networks need storage. A logical network has stable identity separate from its display name so renaming does not disconnect participants.

One asset may participate in more than one logical network through explicitly configured input and output ports. No asset publishes to every team network implicitly. A future bridge or combinator may read one network and emit into another without merging the networks themselves.

## Canonical signal contribution

Every contribution must retain these independent facts:

- team
- logical network
- exact source asset or station
- signal key
- numeric value
- celestial location metadata

Conceptually:

```text
team
    logical network
        source asset
            signal key
                value
```

Location is not network identity. One logical network may span several bodies, while several isolated networks may exist on one body.

The source contribution is canonical. Values grouped globally, by system, by body, or by signal key are derived views. Removing a source removes only that source's contributions. Renaming, moving, or changing one source must not require reconstructing an anonymous total.

## Resource logistics as one consumer

Resource availability and demand are the first obvious use of the signal system, but they do not define the complete signal model.

Using the sign of one generic item value to mean supply or demand would make arbitrary arithmetic and machine conditions ambiguous. A future model should make the meaning explicit, for example through distinct resource fact, offer, and request signal meanings. The exact key representation remains a later design decision.

The logistics planner consumes offer and request views from the same network facts. It preserves the concrete supplier and requester, chooses a route, and creates a physical delivery. Delivery execution changes real inventories. A later signal snapshot reflects those inventory changes. Signal state does not directly pretend that resources moved.

## Deterministic update model

A stable snapshot per simulation step is the preferred conceptual model.

```text
snapshot N
    -> machines and conditions read one stable state
    -> facilities perform work
    -> sources expose their new contributions
    -> snapshot N+1 is published
```

This avoids order-dependent reads on Minecraft's primarily single-threaded simulation. All consumers in one step observe the same network state. Factorio's exact combinator latency is not binding, but Galaxia needs explicit and deterministic visibility timing.

## Conditions and derived emitters

A condition selects a logical network, a signal key, an aggregation or source filter, a comparison, and a threshold. The machine owns what happens when its condition is true. The network owns evaluating the signal query consistently.

A combinator-like module is both a receiver and an emitter. It reads one stable snapshot, applies an operation, and publishes its result into a later snapshot. It may publish into the same logical network or an explicitly selected different network.

## Current cleanup boundary

The current codebase simplification work does not implement this future system. It must not add logical-network management, conditions, virtual signals, combinators, new machine behavior, or new GUI.

The current work may simplify existing logistics signal code only when it preserves:

- exact source asset identity
- current resource signal behavior
- celestial location facts needed by routing and presentation
- a clean path to future logical-network identity
- the distinction between canonical source contributions and derived aggregates

The existing signal cache may be replaced by a complete snapshot only if that snapshot remains source-addressed. A body, system, or global aggregate cannot become the canonical replacement.

## Open future decisions

- whether interplanetary signal visibility is immediate or depends on satellite connectivity
- the exact stable identity and ownership model for logical networks
- the signal key space for resources, status, and user-defined signals
- the condition expression model and supported aggregation filters
- which source contributions and aggregates are synchronized to clients
- permissions for reading, publishing, bridging, and configuring networks

These questions are intentionally deferred. They do not belong to the current simplification-only stack.

[[Sources]]
