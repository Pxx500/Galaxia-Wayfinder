---
type: engineering-guide
status: active
tags:
  - galaxia/alpha
---

# GUI Testing Workflow

New GUI behavior and GUI bug fixes should normally add or extend a Horizon QA client scenario in the same change
Cosmetic-only edits use the ModularUI2 Preview workflow in AGENTS.md unless they affect input or lifecycle behavior

## Choose the Test Layer

| Behavior | Verification |
| --- | --- |
| Domain rules, algorithms and codecs | JUnit |
| Gameplay integration, server ticks and synchronization | Horizon QA API scenarios |
| Player interactions and screen lifecycle | Horizon QA GUI scenarios |
| Local layout and styling | ModularUI2 Preview using the production builder |

## Write and Verify

- Exercise the interaction under test through real GUI input, with API setup only for prerequisites
- Assert observable results, including server acceptance and client synchronization when affected
- Cover relevant Save, Cancel, reopening, selection and resize transitions
- Resolve live controls through ClientTarget and actual hit tests, using condition waits instead of fixed delays
- Keep input target resolvers observational, without enqueueing operations that their own readiness depends on
- Restore test-owned state and listeners through cleanup, including after failure
- During implementation, run only the domain groups affected by the change, including relevant integration boundaries. A GUI change does not by itself require every GUI scenario
- Run the full Galaxia test suite before opening a pull request, or when the owner explicitly requests it. Do not repeat the full suite for routine local handoffs
- Inspect the completed report for failures, skips and infrastructure errors, not only the launcher exit
- On Windows, close Overwolf before native window-resize tests, with the user's approval if it is running. Its injected hooks can resize the OS window while LWJGL and Minecraft retain the previous framebuffer dimensions. Restart the test client after closing Overwolf because already injected DLLs remain in that process
- When investigating resize failures, inspect loaded module paths, not just names containing `Overwolf`. Known injected modules include `OWClient.dll`, `OWExplorer.dll`, `GEPPlugin64.dll`, `gep_minecraft.dll`, `libowgameevents64.dll` and `ow-graphics-hook64.dll`
- Screenshots support diagnosis and presentation, not proof of correct behavior

## Repository Entry Points

| Need | Location |
| --- | --- |
| Existing scenarios and shared GUI targeting | `src/gameTest/java/com/gtnewhorizons/galaxia/gametests/` |
| Local domain groups | `scripts/run-tests.ps1 -ListSuites` |
| Focused physical-station checks | `scripts/run-tests.ps1 -Suite physical-stations` |
| Full verification before opening a PR | `scripts/run-tests.ps1 -Suite all` |
| Dependency revision and Linux CI setup | `.github/workflows/horizon-qa.yml` |
| Completed-suite validation | `scripts/check-horizon-qa.py` |

Run the local script through Context Mode with an explicit timeout because it invokes Gradle
Available domain groups are `physical-stations`, `automated-facilities`, `rocket-production`, `starmap` and `satellites`. Each combines the domain's gameplay and GUI scenarios. Select more than one group when a change crosses domains, for example `-Suite starmap,satellites`. Use `-DryRun` to inspect the selection without starting Minecraft or Gradle
Assign new Horizon QA test holders to their owning group in the script. The `all` selector always includes the whole `galaxia` namespace, including newly added holders
Pass `-HorizonQaRoot` and `-HorizonQaJar` for the actual checkout and matching development JAR
Keep the launcher and development JAR on matching report-schema versions. A passing game report can still be rejected by a launcher expecting a different schema
The local script uses Horizon QA's portable Gradle launcher under `scripts/client-tests`
CI builds Horizon QA from its pinned source revision, without requiring a published JAR
The GitHub check reports failures but is not configured as a required merge check

[[Agent Briefing]]
