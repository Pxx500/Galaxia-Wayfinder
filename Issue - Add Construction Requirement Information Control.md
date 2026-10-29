---
type: implementation-issue
status: planned
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Automation and Infrastructure]]"
source_decision: "[[Require Star Map Object Actionability]]"
tags:
  - galaxia/alpha
  - wayfinder/issue
---

# Issue - Add Construction Requirement Information Control

## Goal

Expose construction requirements without blocking the primary build action or pretending Galaxia can detect the player's GTNH technology tier.

## Accepted Behavior

- An applicable primary construction button immediately creates its Construction Site.
- Missing construction materials do not disable the primary button.
- A smaller `?` information control appears on the right side of the construction action.
- Hovering the information control shows the required materials and relevant advisory information.
- Any tier wording describes the materials, such as `uses LuV-tier materials`; it does not claim whether the player has reached that tier.
- Galaxia does not need a saved `skip preview` preference because no mandatory preview interrupts construction.

## Open Implementation Choices

- Exact hover-widget layout and additional information beyond the material list.
- Whether clicking the `?` control pins or opens a persistent detail view for long lists.
- How the Construction Site exposes the same requirements after creation.

## Related Topics

- Require Star Map Object Actionability
- Area - Automation and Infrastructure
- Galaxia Alpha Wayfinder

## Gameplay Flow

The player can hover the information control to inspect materials before building. Selecting an applicable primary action creates the Construction Site immediately, even when materials are missing, and the requirements remain available from the site.
