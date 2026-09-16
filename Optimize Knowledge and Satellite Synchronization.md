---
type: wayfinder-ticket
ticket_type: research
status: deferred
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
  - wayfinder/research
  - wayfinder/deferred
---

# Optimize Knowledge and Satellite Synchronization

## Question

Do periodic knowledge and satellite rebuilds and broadcasts create a measurable cost that justifies revision-driven synchronization, and what is the smallest revision contract that removes the waste without adding more state than it saves?

## Established Input

- This is a future optimization, not current implementation scope.
- Measure rebuild time, packet count, packet size, player and team scaling, and allocation before redesigning the path.
- Compare the existing periodic full-state model with one team-scoped revision and dirty publication.
- Scan progress must not force unrelated full-state publication if it can be represented independently.
- Physical Station data endpoints are a separate product capability and must not be introduced as an optimization side effect.

## Related Topics

- [[Define Satellite Link Distance Quality]]
- [[Define Prospecting Data Processing]]
- [[Area - Observation and Research]]
