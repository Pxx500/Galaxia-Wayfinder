---
type: wayfinder-guide
status: active
tags:
  - galaxia/alpha
  - wayfinder/guide
---

# Editing Guide

## Decision Notes

Write about the game directly: “Each cluster has its own power input”, not “The owner selected separate power inputs”.

- Start with a descriptive system heading and one sentence of purpose.
- Use domain sections, short rules and tables. Avoid a mandatory template of empty headings.
- Mark proposals, working tuning, deferred ideas and open questions explicitly. A note can contain settled rules while its overall question remains open.
- Keep rationale when it explains a non-obvious tradeoff.
- End gameplay notes with **Gameplay Flow**: concrete, connected prose showing what the player does, what changes and why the mechanics fit together. Restate the rules in human terms without inventing behavior or promising results not established by the design.
- Do not append gameplay prose to indexes, glossaries, raw sources or historical engineering records.
- Remove repeated caveats, chat narration, task coordination, workstation details and discarded proposal inventories. Preserve meaningful constraints, numbers, exceptions, uncertainty and source attribution.
- Keep one authoritative home for each rule. Link to it elsewhere instead of copying the specification.
- Do not retain deferred implementation plans. Derive implementation details when execution starts.

## Navigation And Metadata

The home page and area hubs organize notes by topic. Their link labels can be shorter than the filenames. Metadata retains planning status and dependencies.

| Type | Purpose |
| --- | --- |
| `wayfinder-map` | Destination, design packages and navigation |
| `wayfinder-area` | Topic index |
| `wayfinder-ticket` | Decision or investigation and its result |
| `implementation-issue` | Implementation work outside the planning frontier |
| `source` | Original input or evidence, not automatic design approval |
| `glossary` | Canonical terminology in [[CONTEXT]] |

Ticket properties:

| Field | Meaning |
| --- | --- |
| `status` | `open`, `resolved`, `blocked` or `deferred` |
| `ticket_type` | `research`, `grilling`, `prototype` or `task` |
| `parent` | Map name as plain metadata |
| `areas` | One primary area wikilink |
| `secondary_areas` | Optional plain-text classifications |
| `blocked_by` | Concrete prerequisite notes |
| `claimed_by` | Current person or session, empty when unclaimed |

Resolved means the question is answered, not that implementation or verification is complete. A nonempty dependency list does not imply blockage if every prerequisite is already closed.

## Workflow

1. Find a topic through [[00 - Galaxia Alpha Command Center]] and its current package in [[Galaxia Alpha Wayfinder]].
2. Choose an open, unclaimed question with no unresolved blockers. Claim it before work.
3. Check settled decisions before asking new questions. Group independent consequential choices in a discussion round.
4. Record accepted answers in their owning notes. Resolve only answered questions.
5. Create newly precise questions, then wire dependencies. Leave imprecise future work as such.
6. Continue to the next unblocked question. Pause for a required answer, evidence or authorization, not after each isolated answer.

Grouped rounds override the generic skill's one-ticket-per-session limit. Do not invent questions to fill a round or reopen deferred systems without a change in scope.

## Sources And Evidence

New material is unreviewed intake linked only through [[Sources]]. Later review classifies it. Original external proposals and reusable research retain their provenance and source meaning.

Temporary agent inputs are an inbox, not permanent project documentation. After review, move accepted rules and genuine open proposals into their owning notes with concise provenance. Remove consumed wrappers and one-off task, device, branch and test-session instructions. Archive originals locally when needed for recovery. Do not promote suggestions or implementation tuning into accepted design during cleanup.

Dated code observations and execution results describe the inspected revision, not current runtime behavior. Keep useful evidence concise and separate from rules. Consolidation can reconcile explicit decisions and metadata, but cannot approve new gameplay.

## Links And Names

Keep existing filenames and incoming heading anchors unless all affected links are updated. Use readable link labels in navigation. Windows filenames cannot contain a colon, so implementation notes may use `Issue - Title`.

Each ticket has one primary-area link. Other hard links represent concrete dependencies or useful navigation, not arbitrary graph decoration. Keep loose related topics as plain text. Sources remain separate from the active decision map until classified.
