---
type: source
status: routed
origin: "Repository docs/architecture/2026-07-21-celestial-discovery-checklist-design.md"
imported: 2026-08-01
tags:
  - galaxia/alpha
  - wayfinder/source
  - galaxia/observation
---

# Repo Source - Celestial Discovery Concept

Source: repository design document `docs/architecture/2026-07-21-celestial-discovery-checklist-design.md`
Imported: 2026-08-01

The implementation sequence and code ownership proposal were intentionally discarded. This snapshot preserves the universal discovery concept, durable requirements, and remaining product decisions.

## Source Snapshot

### Concept

All celestial bodies participate in one knowledge and discovery model. Different starting states are authored data, not separate discovery architectures. An asteroid belt may generate child asteroids by belt-specific rules, but once those bodies exist they should use the same identity, facts, and discovery language as planets and moons.

### Candidate Knowledge Checkpoints

1. `DETECTION`: the body is known to exist.
2. `SIGNATURE`: coarse resource information is known.
3. `PROFILE`: detailed resource information is known.

The final Alpha knowledge layers remain an open decision in Define Alpha Celestial Knowledge Layers.

### Requirements

- Starting knowledge is declarative per body or generation rule.
- Team knowledge overrides definition-level starting knowledge.
- Scanning selects the next incomplete checkpoint for eligible bodies in range.
- Detection work completes before deeper prospecting within the same scope.
- Finished checkpoints are skipped without placing a category of body outside the model.
- Candidate selection uses a shared spatial interpretation for all addressable body identities.
- Ordering should use a common physical or authored property rather than asteroid-only size categories.
- Belt-specific generation may decide what asteroids exist and their initial facts, but it must not own a parallel team knowledge system.

### Remaining Decisions

- Which knowledge layers and facts Alpha actually exposes.
- Which bodies begin hidden, detected, or partially profiled.
- Which physical property controls discovery order.
- Which scan sources and activities can complete each checkpoint.
- How authored planets and generated minor bodies share one range model.


## Wayfinder Integration

- The universal discovery model is input to [[Define Alpha Celestial Knowledge Layers]].
- The opening boundary remains governed by Define Alpha Observation Opening.
- Candidate checkpoints and remaining decisions are not yet accepted.
