---
type: execution-tracker
status: delivered-local
date: 2026-10-23
tags:
  - galaxia/alpha
  - galaxia/execution
---

# Recipe Environment Implementation Handoff

This historical handoff records the local 2026-10-23 delivery and its verification limits. Current requirements belong to [[Define Celestial Capability Rules]] and [[Define Alpha Research and Production Floor#Native GT Machine Failure Semantics]].

## Scope

The Galaxia-only delivery used GT metadata, a builder helper and temporary late mixins. It covered EBF, ordinary Fluid Solidifier and Extruder, with environment checks before consumption, native GT failure when conditions are lost, translated NEI requirements, and conditions observed at the multiblock controller. Existing heat, caching, locking, parallel processing, unrestricted recipes and housekeeping remained in scope. It did not promise extra progress or output retention.

Galaxia owns environment definitions, celestial classification and room pressure. Rooms require controllers. Removing a controller removes the modeled room and its atmosphere data even if the shell remains closed. The earlier controllerless-room blocker was withdrawn, not resolved by a room-detection redesign. Unresolved conditions while Galaxia is loaded are not satisfied.

The local authoring entry was `RecipeEnvironments.requiresEnvironment(MICROGRAVITY, NO_ATMOSPHERE)`, returning a normal `GTRecipeBuilder`. Tags are conjunctive and independent of `mSpecialValue`. Extensions register through `RecipeEnvironments.register(...)`. Temporary integration under `com.gtnewhorizons.galaxia.mixin.gt` was intended for removal after equivalent native GT hooks exist. Direct GT authoring and absent-Galaxia handling belong to the later API transfer, not this local delivery.

Full production chains, blueprints, knowledge gates, vacuum pumps, connectivity redesign and global replacement of GT cleanroom or LOW_GRAVITY behavior were excluded. The microgravity threshold remains tuning. Zero gravity was a positive fixture, Luna at 0.25 and Overworld at 1.0 negative fixtures. Those fixtures do not establish a reachable early orbital workshop.

## Local Delivery And Evidence

The implementation was reported on local branch `recipe-environments` in `~/Documents/GitHub/Galaxia/worktrees/recipe-environments`, uncommitted at the time. A patch checked against base `092ad1800bbbaa96dc8f2bac6d6ccfa45e32e852` was saved at `~/.agents/docs/Galaxia/worktrees/recipe-environments/docs/integration/recipe-environments.patch`. This dated report does not establish the branch's current state.

The 2026-10-23 Horizon-QA run `build/horizonqa/environment-copy` passed three selected scenarios and exited normally. Coverage included recipe rejection and native failure, EBF heat and processing, pressure decay, airlock equalization, oxygenation, breach venting, controller GUI and ordinary and shallow recipe copies. The copy constructor required a fourth narrow mixin because the checked GT version drops metadata in native copies.

The ordinary build reported 961 passing JUnit tests, Spotless and Checkstyle. `agentVerify` was absent in that checkout. PMD completed, but IntelliJ reported internal inspection errors, so the combined audit was incomplete. Detailed evidence and dispositions are in `~/.agents/docs/Galaxia/worktrees/recipe-environments/docs/reviews/recipe-environments-verification.md`.

The 2026-10-10 retained-work pause checkpoint and built development JAR are superseded experiments. Their pause and automatic-resume results do not verify the selected native GT failure contract. The controllerless-room diagnostic likewise tested an expectation that is no longer required.
