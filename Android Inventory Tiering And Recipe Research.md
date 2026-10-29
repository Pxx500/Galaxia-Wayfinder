---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Android Inventory Tiering And Recipe Research

Source: Read-only Galaxia and dependency investigation requested in the remote android implementation chat
Imported: 2026-10-21

## Source Snapshot

The complete local report is `~/.agents/docs/Galaxia/worktrees/remote-android-bodies/docs/research/2026-10-21-android-pr-readiness-report.md`

Its adjacent inventory, integration and battery evidence notes preserve source versions, code references, arithmetic and limits

Observed facts:

- Minecraft 1.7.10 and several inspected mod integrations depend on the vanilla 36-slot player inventory shape. Changing the backing array also changes armor index boundaries. A graphical disabled state does not globally enforce fewer usable slots
- Portable storage makes player slot count different from total freight capacity
- Android bodies already own persistent capacity and charge. BodyState already carries maximum health. Removable batteries and chassis model identities are not implemented
- The dock already has six item inputs, a fluid tank, energy interfaces and manufacture and repair maps. Its recipe query is limited to EV. Production registrations for these maps are missing in the inspected checkout
- Manual laboratory recipes already have an isolated fixture source. They can remain separate from ordinary production content
- The inspected existing HV rechargeable batteries hold 800,000 EU for Sodium, 1,200,000 for Cadmium and 1,600,000 for Lithium. Native higher-tier stores can be much larger than the current android operating cost warrants
- Current manufacture creates a fully charged body, so the source of initial stored energy needs an explicit production decision
- Live control already reserves shared satellite bandwidth and ends when its reservation is lost. Exact per-reservation route telemetry and network latency are not exposed by the inspected read model
- Charging and repair require the exact original dock and physical containment. There is no current service reassignment or autonomous recovery operation
- The inspected runtime and canonical GTNH data snapshot use different GT versions. Source findings do not establish full-pack compatibility or a complete playable recipe progression

Historical recommendations and open choices, not accepted design. The EV/IV/LuV sequence and custom-pack suggestions below predate the later EV/LuV/UV and native-battery decisions:

- Retain 36 usable player slots for this PR
- Start with EV, IV and LuV chassis and fixed integrated batteries. Prefer endurance, modest health and maintenance progression over new mining, combat or hazard-immunity bonuses
- Existing battery chemistries offer a conservative option. Larger custom packs are feasible but require explicit content and recipe work
- Prefer deterministic tier-matched repairs over uniformly random component consumption
- Use ordinary GT recipes and the existing dock job owner. Keep the universal dock's final recipes within its electrical capability
- Consider paid dock charging after manufacture instead of silently granting a full battery
- Useful integration candidates are preflight information, last-known body beacons, dock readiness signals and better bandwidth efficiency on higher chassis tiers
- Field surveys and physical dock reassignment have plausible owners but larger missing contracts. Autonomous return and interplanetary live-body transport conflict with current lifecycle assumptions

These findings have not been promoted into accepted Wayfinder decisions or an implementation plan

[[Sources]]
