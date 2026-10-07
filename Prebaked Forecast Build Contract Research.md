---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Prebaked Forecast Build Contract Research

Source: Owner discussion on 2026-10-07, local Galaxia checkout, Gradle 9.4.0 documentation, and GTNHGradle 2.0.26 source
Imported: 2026-10-07

## Source Snapshot

The owner selected a fully prebaked route forecast generator. Ordinary builds should cheaply detect changes to calculation inputs rather than always regenerate forecasts. A stale dataset should produce a console warning and offer a yes or no regeneration choice. A build argument should supply a no answer without prompting. The generator and publication workflow remain unimplemented.

This note records research and recommendations. It does not itself establish new accepted decisions. Its only Vault link is [[Sources]].

## Verified Build Environment

The local checkout was inspected at commit `a9128e9ef21ff05254648190b4f79f94bdc9669d`. `gradle/wrapper/gradle-wrapper.properties` selects Gradle 9.4.0. `settings.gradle.kts` selects `com.gtnewhorizons.gtnhsettingsconvention` version 2.0.26. `build.gradle.kts` applies `com.gtnewhorizons.gtnhconvention`. `gradle.properties` enables configuration cache and parallel execution.

The convention plugin applies GTNHGradlePlugin. At the matching version, GTNHGradlePlugin applies JavaLibraryPlugin and RetroFuturaGradle UserDevPlugin. Standard Java compilation and resource tasks are therefore relevant integration points. The exact RFG transformed artifact path should be verified when implementation starts. Sources: [GTNHConventionPlugin at 2.0.26](https://github.com/GTNewHorizons/GTNHGradle/blob/d6fe75bf0c1d56b292e8e3f2bb266f6e710b974c/src/main/java/com/gtnewhorizons/gtnhgradle/GTNHConventionPlugin.java), [GTNHGradlePlugin at 2.0.26](https://github.com/GTNewHorizons/GTNHGradle/blob/d6fe75bf0c1d56b292e8e3f2bb266f6e710b974c/src/main/java/com/gtnewhorizons/gtnhgradle/GTNHGradlePlugin.java).

Gradle's `classes` task depends on compilation and resource processing. `jar` depends on classes and packages their output. This permits a forecast verification gate before artifact creation. Gradle supports declared task inputs and outputs for incremental checks. A cheap verification task should perform validation in its execution action or declare inputs and a reproducible verification result. A check performed only during configuration would not run again when configuration cache is reused. Sources: [Java plugin tasks](https://docs.gradle.org/9.4.0/userguide/java_plugin.html#sec:java_tasks), [incremental builds](https://docs.gradle.org/9.4.0/userguide/incremental_build.html), [configuration cache requirements](https://docs.gradle.org/9.4.0/userguide/configuration_cache_requirements.html).

No Gradle command, build, benchmark, or test was run for this investigation.

## Canonical Input And Change Detection

Proposed contract: the baked dataset records a cryptographic digest of a deterministic numerical input document. SHA-256 is sufficient for change detection. Comparing digests does not require running the transfer solver. Digesting a small document is proportional to its byte size, rather than to the number of transfer candidates.

The input document must cover every effective input consumed by the generator. It should include:

- The complete eligible body set with stable identities and parent relationships.
- Orbital and gravitational parameters consumed by the selected route model, including initial phases if the table depends on them.
- Surface or endpoint terms included in universal dV. Rocket inventory and engine-specific Isp stay outside a universal dV dataset unless the chosen solver actually depends on them.
- Belt representative radius definitions and their shared angular motion, rather than a separate entry for every generated asteroid.
- Units, simulation time scaling, eligible route types, route constraints, and model constants.
- Generator and solver implementation identity, sampling resolution and strategy, numerical tolerances, and dataset format identity.

Sorting bodies by stable identity and sorting named properties prevents registration order from changing the digest. Use a fixed field order, explicit units, and deterministic numeric encoding. Reject non-finite input. Decide once whether equivalent values such as positive and negative zero are normalized. Filesystem paths, build timestamps, map iteration order, texture names, translations, and GUI layout are not route inputs.

Only hashing planetary values misses a changed solver or changed sampling policy. An explicit model version is readable but requires developers to remember to change it. A content digest of the relevant numerical solver and generator sources provides automated coverage. It can cause harmless rebakes after numerical-code formatting changes. Hashing the entire mod instead would cause unnecessary rebakes after unrelated work. This is a proposed tradeoff, not an implemented versioning scheme.

The build check should compare the current input fingerprint with the fingerprint stored alongside the baked result, not with an unrelated previous-build timestamp. Otherwise a stale result can become accidentally accepted after an ordinary rebuild.

## Obtaining Inputs Without Starting Minecraft

The present `CelestialRegistry.registerDefaults()` combines numerical orbit definitions with textures, materials, Forge fluids, dimension builders, and planetary feature registration. The registry is therefore not already a standalone numerical catalog. Calling it from a new Gradle fingerprint task would need substantial mod initialization and would not meet the intended cheap check. Relevant local source: `src/main/java/com/gtnewhorizons/galaxia/registry/celestial/CelestialRegistry.java`, particularly registration from line 96 and its Forge and GregTech imports.

Proposed requirement: keep one authoritative, headless numerical catalog that both game registration and the generator consume. A small declarative resource is one possible form. Shared pure Java definitions are another. Do not maintain a second handwritten planet list for the baker or attempt to extract arbitrary Java expressions using regex.

The ordinary build can then hash the effective catalog, model inputs, and relevant generator implementation. If numerical inputs are computed from Java, the headless export should itself be incremental, with its dependency closure tracked by Gradle. A fresh Java process has startup cost even if hashing is cheap. Avoid launching it for unchanged inputs. Measure this overhead before choosing an export mechanism.

If route inputs can also be changed by server configuration or an external registration integration, the packaged table cannot silently claim to describe those altered inputs. The design must either constrain supported inputs to the authored catalog or verify the effective fingerprint when loading the table. This is validation of prebaked data, not a runtime regeneration path.

## Interactive And Noninteractive Builds

Gradle supports project properties through `-Pname=value`, which can be read through the provider API. A proposed property such as `-ProuteForecastRebake=no` could mean: retain the stale or missing status, emit the warning, do not prompt, and do not run the expensive generator. `yes` could explicitly approve regeneration. These names and values are examples, not existing arguments. Source: [Gradle project properties](https://docs.gradle.org/9.4.0/userguide/build_environment.html#sec:project_properties).

For an interactive terminal build, a yes or no question can be offered after detecting stale data. If a child generator is an Exec or JavaExec process, its standard input defaults to an empty stream. Forwarding input must be deliberate. Configuration cache explicitly permits standard streams, including `System.in`, as Exec or JavaExec parameters. Sources: [BaseExecSpec standard input](https://docs.gradle.org/9.4.0/javadoc/org/gradle/process/BaseExecSpec.html#getStandardInput()), [configuration cache and standard streams](https://docs.gradle.org/9.4.0/userguide/configuration_cache_requirements.html#live_jvm_state_types).

The daemon is not itself a reason to ban prompting. The unresolved practical issue is whether the invoking frontend supplies interactive input. IDE task invocations, CI, and redirected terminals cannot be assumed to provide it. Gradle console output mode controls presentation, not approval semantics. Reading a yes or no answer must never hang a headless build. Source for the output distinction: [Gradle console modes](https://docs.gradle.org/9.4.0/userguide/command_line_interface.html#sec:command_line_customizing_log_format).

Proposed behavior: an explicit yes or no property always wins. When stale data is found and no answer was supplied, prompt only in a supported interactive invocation. Noninteractive builds should return a clear actionable failure unless the owner chooses automatic decline. EOF must have a defined outcome. Do not interpret missing input as consent.

The expensive generation should be its own explicit operation, called only by the approved branch of the build workflow or by a manual bake task. Do not add it as an unconditional dependency of ordinary compilation. The normal input check must also run for IDE compile and development launch paths that need forecast resources, not only for release packaging.

## Declining A Stale Bake

A no answer cannot make an old forecast mathematically current. Three distinct outcomes are possible:

- Cancel the build until data is regenerated.
- Produce a runnable artifact with unavailable forecast estimates and retain exact mission validation.
- Produce an artifact that displays stale estimates as current.

The third option is misleading. Even if exact departure validation prevents invalid flights, stale estimates can misrepresent availability and waiting time.

Recommended outcome for local iterative work: the no argument skips regeneration and allows gameplay development, but the produced artifact identifies the forecast as unavailable. Exact route validation still works. This satisfies fully prebaked forecasting without introducing runtime generation. Missing baked data has the same unavailable-estimate behavior. Release policy can separately require a matching baked dataset.

An unavailable estimate is a new explicit development behavior, not a legacy compatibility loader. It still needs owner acceptance because it determines what declining the prompt means for the resulting artifact. Do not silently implement it from this research note.

## Genuine Open Choices

- Does declining regeneration allow a runnable development artifact with estimates disabled, or cancel the build? The current owner request implies a usable pre-decline mode, but does not explicitly define artifact behavior.
- In a noninteractive build without an explicit answer, should the build fail or automatically decline? Recommendation: fail with the accepted argument shown, avoiding an accidental release with no estimates.
- Must publication require current baked data even when a local development build may decline? Recommendation: yes, subject to an explicit owner decision.

Everything else above is a concrete implementation recommendation for later review. No runtime/prebaked dual mode is proposed. The owner selected fully prebaked generation.

## Evidence Limits

The graph query returned older source line ranges for CelestialRegistry than the current checkout. Bounded direct inspection of that known file supplied the current coupling evidence. No index repository tool was available to this agent. Build configuration and pinned plugin source were read directly.

Primary Gradle pages were fetched at their 9.4.0 version and their titles and relevant sections were checked. GTNHGradle tag 2.0.26 resolved to `d6fe75bf0c1d56b292e8e3f2bb266f6e710b974c` before its plugin source was read. No timing claims or promises about interactive IDE behavior were tested.
