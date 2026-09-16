---
type: implementation-issue
status: planned
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Decompose Galaxia Persistence Ownership

## Durable Requirement

Saving and loading must preserve domain-owned assets, logistics deliveries, knowledge, and discovery consistently. Shared lifecycle coordination should remain small, while each domain owns the meaning and validation of its saved state. Do not create parallel owners or speculative pre-release migration paths.

## Current Evidence

Source inspection on 2026-09-12 found assets loaded before tasks, followed by knowledge and discovery in `core/persistence/FacilityPersistenceManager.java:118`. The comment at line 127 requires content catalogs before minor-body facts and shared facts before referencing scan progress. Logistics task encoding and decoding still live directly in this manager at lines 195 and 247. Paths are under `src/main/java/com/gtnewhorizons/galaxia/`.

The existing partial delegation does not certify the complete refactor.

## Disposition

Reclassified on 2026-09-12 from an open gameplay decision to non-blocking implementation work. Orchestrator names, nested versus top-level codecs, and file boundaries should be chosen from current code when implementation begins. They do not require another Wayfinder interview or block module-settings gameplay decisions.

Existing accepted endpoint, delivery, settings, and discovery contracts remain authoritative. No implementation is authorized by this note.
