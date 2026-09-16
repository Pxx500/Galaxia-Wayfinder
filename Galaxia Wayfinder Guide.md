---
type: wayfinder-guide
status: active
tags:
  - galaxia/alpha
  - wayfinder/guide
---

# Galaxia Wayfinder Guide

## Node Types

- `wayfinder-map` — the canonical low-resolution route toward a destination.
- `wayfinder-area` — a graph hub grouping related tickets and decisions without owning their detail.
- `wayfinder-ticket` — one planning question resolved through research, grilling, prototyping, or a prerequisite task.
- `implementation-issue` — implementation work preserved outside the active planning frontier.
- `source` — imported or authoritative material; unreviewed source snapshots do not become accepted design merely by existing in the Vault.
- `glossary` — canonical domain language in [[CONTEXT]].

## Ticket Properties

- `status`: `open`, `resolved`, `blocked`, or `deferred`.
- `ticket_type`: `research`, `grilling`, `prototype`, or `task`.
- `parent`: the owning Wayfinder map as plain metadata, not a wikilink.
- `areas`: exactly one primary area hub wikilink.
- `secondary_areas`: optional plain-text classifications that do not create graph edges.
- `blocked_by`: concrete prerequisites. A ticket is unblocked when every listed prerequisite is resolved, completed, or explicitly closed. Historical dependencies may remain for provenance.
- `claimed_by`: the person or session currently working the ticket; empty means unclaimed.

## Workflow

1. Open [[00 - Galaxia Alpha Command Center|Galaxia Alpha Command Center]].
2. Follow the Wayfinder to one area and choose an actionable ticket there.
3. Choose an open, unclaimed ticket whose listed prerequisites are resolved, completed, or explicitly closed. A populated dependency list alone is not a blocker.
4. Claim it before work by setting `claimed_by`.
5. Resolve only that ticket, record the answer in the ticket, and set `status: resolved`.
6. Move the resolved ticket under its primary area's resolved decisions.
7. Create newly visible tickets and wire their `blocked_by` links; leave imprecise future work in Not Yet Specified.

## Naming

Windows filenames cannot contain `:`, so implementation notes use `Issue - Title` when a visible prefix is helpful. The canonical distinction is the `type: implementation-issue` property and `#wayfinder/issue` tag, not the filename prefix.

## Graph Links

- Command Center links to the Wayfinder; the Wayfinder links to area hubs and intake indexes.
- Each ticket has one hard primary-area link.
- Use hard links between tickets only for blockers or concrete domain dependencies.
- Keep secondary areas and loose related topics as plain text.
- Sources form short intake or provenance chains instead of linking to every routed ticket.

## Related Topics

- Galaxia Alpha Wayfinder
- CONTEXT

## Authority and Record Status

Frontmatter is the navigation status. Accepted decisions belong in their owning tickets. Historical source labels and chronological log entries describe their recorded time, not the current frontier or a current implementation certificate. Unreviewed sources remain intake only. Completed execution records are evidence, not instructions to restart their old plans.

Consolidation may repair metadata and reconcile explicit decisions across notes without resolving new gameplay questions. Reports and historical records do not override the owning decision.
