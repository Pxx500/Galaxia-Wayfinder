---
type: wayfinder-ticket
ticket_type: research
status: resolved
parent: Galaxia Alpha Wayfinder
areas:
  - "[[Area - Progression]]"
blocked_by: []
claimed_by:
tags:
  - galaxia/alpha
  - wayfinder/ticket
  - wayfinder/research
---

# GTNH Ore Progression Baseline

## Authority

Source: [GTNH Spreadsheet](https://docs.google.com/spreadsheets/d/1EIZtJU5eBbnUlrg7fD_ZyIzsr9sn4l4no9ek6M_iSVM/edit?gid=955235406#gid=955235406)

Inspected tab and range: `Ore Sheet (2.8.0)!A1:AV953`

The spreadsheet is maintained by the GTNH development team and by Pxx500 directly. It is the authoritative starting source for current ore-vein placement and destination tier grouping. A live public workbook export was inspected on 2026-07-31, including cell formatting.

## Table Semantics

- Each ore-vein row defines its `Primary`, `Secondary`, `Between`, and `Sporadic` ores, plus `Height`, `Density`, `Size`, and `Weight`.
- An `X` in a destination column means the vein occurs at that destination.
- Destination-header fill colors group destinations into Ore Tiers.
- A filled `X` marks a Highlighted First Occurrence along a progression route.
- A highlighted first occurrence is evidence that the vein may matter to progression, but it is not proof that it is a mandatory Tier Gate.
- An unfilled repeated `X` means the vein remains available later. Repeated availability is not automatically progression-critical, but its economic and gameplay role must not be discarded without review.
- Some routes require more than one highlighted occurrence. Naquadah is the confirmed example: End Asteroids are optional, while Galacticraft Asteroids are an expected destination.

## Destination Ore Tiers

The sheet currently groups destinations by header color as follows:

1. `OW`, `Nether`, `TF`, `End`, `End A.`
2. `Moon`
3. `Deimos`, `Mars`, `Phobos`
4. `Asteroids`, `Callisto`, `Ceres`, `Europa`, `Ganymede`
5. `Io`, `Mercury`, `Venus`
6. `Enceladus`, `Miranda`, `Oberon`, `Titan`
7. `Proteus`, `Triton`
8. `Haumea`, `Kuiper Belt`, `Makemake`, `Pluto`
9. `Barnarda C`, `Barnarda E`, `Barnarda F`, `A Centauri Bb`, `T Ceti E`, `Vega B`
10. `Anubis`, `Horus`, `Maahes`, `Mehen Belt`, `Neper`, `Seth`

The numeric list records ordering only. It does not yet assert final Galaxia rocket-tier numbers or GTNH voltage-tier assignments.

## Verified Examples

The following veins have a highlighted first occurrence on the Moon:

- `Galena`
- `Ilmenite`
- `Bauxite`
- `Monazite`
- `Quartz`

Each also occurs at later destinations through unfilled repeated marks.

`Naquadah` has two highlighted occurrences:

- `End A.` in the pre-rocket destination group;
- `Asteroids` in the later mandatory space route.

It also recurs without first-occurrence highlighting at later destinations including `Mercury`, `Venus`, `Oberon`, `Titan`, `Haumea`, `Kuiper Belt`, `Pluto`, `Barnarda E`, `Barnarda F`, `Vega B`, and `Maahes`.

## Accepted Compatibility Rule

Galaxia Alpha should preserve the earliest accessible Ore Tier of every progression-relevant vein and preserve meaningful route exceptions. It does not need to copy every destination `X` or every vein parameter literally. Repeated placements may change only after their economic, destination-identity, and gameplay roles are evaluated.

Accepted during Galaxia Alpha Wayfinder charting on 2026-07-31. A highlighted first occurrence is evidence that a vein may matter to progression, not proof that it is automatically a Tier Gate; exact progression relevance still requires source-backed verification.

## Accepted Early Progression Baseline

- The player starts on the Overworld, progresses to the Moon, and reaches Mars only after completing the Moon stage.
- This `Overworld -> Moon -> Mars` order must be preserved while Galaxia redesigns the surrounding mechanics.
- An orbital station between the Overworld and the Moon remains a candidate addition, not a confirmed progression requirement.

## Research Still Required

- Identify which highlighted first occurrences are actual GTNH progression gates.
- Identify important gates not represented by ore distribution, including research, machines, recipes, infrastructure, and non-ore materials.
- Determine which repeated ore placements are important to destination identity or resource economics.
- Decide whether `Weight`, `Size`, `Density`, height, and vein composition require parity, deliberate redesign, or later balancing.
- Record the exact GTNH version and source evidence used when turning a candidate into an accepted Tier Gate.

## Related Topics

- Galaxia Alpha Charting Notes
- Galaxia Alpha Wayfinder
