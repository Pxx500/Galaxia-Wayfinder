---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Remote Android Implementation Findings

## Classification

Reviewed for reconciliation on 2026-10-22. Explicit owner decisions on portal retreat, cold and activity energy costs, low pressure, selection and player feedback are incorporated into Define Remote Android Body Lifecycle. The separate global transfer-enforcement scope is reflected in Issue - Enforce Interplanetary Resource Transfer Restrictions. Implementation details, test counts and local branch status below remain dated evidence. Laboratory settings and cosmetic tuning are not new Alpha capability requirements. Historical intake labels below describe their original recording time.

Source: Galaxia implementation conversation and local `remote-android-bodies` branch, based on `a9128e9ef21ff05254648190b4f79f94bdc9669d`
Imported: 2026-10-18

## Source Snapshot

### User Direction

Focus this implementation on androids and the loopholes created by using a normal connected player as the controlled body. Prevent ordinary Ender Chest access by androids. Defer global EnderStorage and other interplanetary transfer integrations. Per-destination EnderStorage channels are the user's preference for that future work, not behavior implemented by this branch.

The requested destruction presentation is a short countdown, a visual explosion, a very short viewing interval, return to the biological body, then removal of the android. The visual explosion must not kill the connected operator. Architecture should have clear ownership and avoid parallel state stores or temporary workarounds.

### Implementation Findings

1. One connected `EntityPlayerMP` can execute distinct physical bodies while preserving the operator's account UUID, connection, team and progression. Physical state must be selected explicitly. Copying whole-player NBT would also copy unrelated account and mod state.
2. Biological and android inventories, armor, Baubles, health, food state, effects and motion need one canonical body checkpoint. Vanilla player and Baubles files save independently, so event ordering alone cannot make them an authoritative coherent body transition.
3. Managed player and Baubles files are physical projections. Early native player loading overlays the acknowledged canonical body state before initial world selection and packets. Recovery ends active control and never automatically resumes it. Armed destruction survives recovery.
4. A biological body needs an entity identity distinct from its operator UUID. Otherwise an inactive biological projection and the connected operator can collide as entities in the same dimension.
5. Equipment transitions need actual lifecycle operations. Settle containers, cursor, crafting, pending mining and tether use, detach source equipment in the source world, transfer an empty locked player, then equip the selected destination body there.
6. Native mining cancellation leaves a separate pending-finish flag. Without clearing it, an old body's completed gesture can harvest matching coordinates after a world change. The integration regression exercises the native public mining path.
7. The existing satellite service can own real reservations shared with ordinary data jobs. Android control does not need another routing service. Capacity loss ends control without automatic reacquisition.
8. A powered capsule maintains a vulnerable physical biological body. Capsule loss returns the latest biological state. A dock owns physical GT processing, material repairs and charging. Charging changes battery alone. Manufacture operation identity must survive replay to prevent duplicate chassis production.
9. Ordinary hazards remain relevant to androids. Actual Mars testing captured `galaxia.temperature` damage to an unprotected chassis. Androids skip biological breathing, food metabolism and unapproved health increases. Thermal protection and RCS remain real equipment requirements.
10. Forbidden dimension departure must be rejected before native transfer mutation and durably arm destruction. The branch uses client-only explosion presentation followed by biological return and local chassis item settlement. It does not run a damaging world explosion.
11. Terminal item settlement must explicitly load the actual source chunk. Minecraft's provide-chunk path can return an inert `EmptyChunk` for an unloaded dimension and is insufficient for real drops.
12. Team merges need durable ownership ancestry for unloaded stations. Merely changing loaded runtime objects does not preserve ownership when an old station later loads.
13. Ender Chest denial belongs at native and confirmed portable entry points, before opening a personal inventory or paying an item cost. It must not substitute a temporary inventory that discards items. Optional adapters are selected only when their host mods are present.
14. The body checkpoint guarantees coherent committed body selection. It does not create an arbitrary-crash transaction across external containers, world drops and independently saved chunks. Those retain Minecraft's ordinary save semantics.

### Verification And Limits

The implementation passed final `agentVerify`, including 945 unit tests with no failures or skips. Focused Horizon runs `android-bodies-9` and `android-bodies-10` each passed all five scenarios with no infrastructure errors or skips. The scenarios cover real capsule GUI activation, distinct belongings, native restrictions, return, chassis death without operator death, biological damage, capsule loss, native early-load recovery, Mars departure destruction, local cargo settlement, charging without healing and paid GT production or repair.

Both station previews use the real production GUI builder. Third-person robot rendering was also inspected in the actual game. The Horizon key test drives the native key binding and FML input event because the pinned helper cannot inject gameplay hardware keys.

Galacticraft, Botania and Thaumic Tinkerer optional hooks were checked against dependency source or bytecode. Their live runtime behavior was not verified in the tested mod configuration because those optional hosts were absent. Baubles and the native player paths were present in the tested game.

Final manufacturing and repair ingredients, EV introduction and tuning values remain content or balance decisions. Production exposes real GT recipe maps. Integration tests install explicit fixture recipes rather than making arbitrary test costs into accepted progression.

Local technical evidence is maintained at `~/.agents/docs/Galaxia/worktrees/remote-android-bodies/docs/reviews/2026-10-18-remote-android-bodies.md`. The branch is local and uncommitted. This input has not been published or classified into the Wayfinder decision graph.

### Manual Gameplay Follow-Up, 2026-10-18

Source: direct user feedback and subsequent implementation and native client verification in the same conversation

The latest accepted interaction is: enter the remote control capsule, choose Change selection, use a specialized starmap context menu to show androids on a planet, optionally name an android, select it, then return to capsule controls with only Change selection and Connect. Selecting an android does not connect automatically. Names belong to team-owned android records and are durable.

The user requires every starmap opening to replace other GUIs and close their child windows, including ordinary map items. Native testing exposed a lifecycle hazard: client close-all can invalidate an already created server container. The implementation closes old server sessions before opening the replacement and disposes old client state without echoing that request. A native regression covers both visual disposal and the new container remaining active.

Both stations need a standing-height entrance and interior. Their revised geometry validates two clear air blocks and passed collision sweeps with the real player bounds. The robot has no ear details. Android control has subtle blue circuit accents and a short boot presentation. Biological return uses an eye-opening presentation. Biological projections retain the operator's skin profile and display nickname's Body. Standard cape access is hidden for the android and restored on return. No resource pack is used.

Final follow-up verification passed 948 unit tests and eight native client scenarios, with no failures, skips, timeouts or infrastructure issues. The native GUI journey covered destination filtering, renaming, passive selection, explicit connection, cape suppression and restoration. The production capsule preview has two visible buttons with no clipping or warnings. Authenticated texture downloads and third-party cosmetic cape renderers were not established by the offline fixture.

Names intentionally introduce checkpoint format 2 for developer scratch data. The next manual session needs a fresh scratch world. No migration or dual loader was added.

The user chose Horizon-QA as the default home for prepared developer gameplay laboratories. Such a session should supply actual powered machines and materials and stay open until the developer ends it, without an automated success condition. This policy was added to the main checkout's local AGENTS.md. Existing Horizon-QA supports interactive launches and template loading, but its GameTests still have finite timeouts. A reusable programmatic manual-session lifecycle was not implemented during this task.

This remains local source intake. It has not been published or classified into the Wayfinder decision graph.

### Direct Context Dropdown And Skin Test, 2026-10-18

Source: direct developer feedback, supplied robotv1.png and native verification in this conversation

Right-clicking a planet in the capsule starmap must show that planet's androids directly inside the existing context menu at the click position. The detached lower-right chooser and intermediate Show Androids action were rejected and removed. The menu retains naming and passive selection, followed by the capsule's Change selection and Connect actions. Clicking outside closes the list. A rename popup must own its input without the map underneath dismissing the context menu.

The developer supplied a 64 by 64 RGBA robot skin. It replaces the production texture verbatim, including all source layers. The developer observed that skin layers do not render correctly in the current game and assigned their backport to another agent. That rendering bug is outside this task. No installed-mod code search or layer-renderer workaround was added here.

Both focused native GUI scenarios passed, including the ordinary map context menu. The latest agentVerify passed all 948 tests. A fresh manual laboratory reached its ready marker with the supplied texture and paper already in the powered dock. The developer explicitly requested that existing game processes neither be inspected nor terminated. This work followed that instruction.

The developer also requested thicker blue circuit accents that originate directly at both side edges of the screen. The original path, opacity and vertical placement should remain recognizable.

### ClankOS Presentation Feedback, 2026-10-18

Source: direct developer feedback and native capture inspection in this conversation

The android boot presentation is branded ClankOS SYSTEM ONLINE. A rapidly scrolling pseudo-terminal is a cosmetic easter egg. The developer explicitly kept the short 0.85-second boot rather than a longer loading sequence. One boot duration value controls the log progression, bar and fade. The biological eye-opening effect is slightly faster at 0.65 seconds, with its own independent duration value. Neither presentation waits for fake startup tasks or delays gameplay control. Messages are localized at the rendering boundary.

The existing native control journey passed with captures of multiple terminal states and biological eye opening. This remains source intake, without Wayfinder graph classification or publication.

### Manual Feedback And Skin Integration, 2026-10-18

Source: direct developer feedback, authorized peer task 01a14ef0-3972-7cb2-afe1-e75659b4bd7f and native verification in this conversation

Every prepared manual Horizon-QA client should start with GUI Scale 2, Quake Pro FOV and disabled clouds. The explicit Galaxia manual launch profile owns these defaults.

Actual health loss of the biological capsule occupant warns only its remote operator through a short red full-display glitch. The warning does not inflict damage on the android. Self-destruction uses a warm alarm console headed ROGUE ANDROID DETECTED. Its progress follows the server countdown. The developer rejected Rogue chassis detected as unnatural wording. The row is Unauthorized android activity detected.

The peer supplied the skin-layer backport. Galaxia initializes its own inactive body model through the published optional SimpleSkinBackport API. Native inactive, controlled third-person and first-person views show the supplied robot skin layers. The targeted integration and injury/self-destruct scenarios passed. The inspected robot did not reveal a mod defect requiring peer changes. This establishes the supplied classic robot rendering, not every third-party cosmetic renderer or SSB compatibility mode.

This remains unsorted source intake, without Wayfinder graph classification or publication.

### Portal Retreat And Ready Mars Laboratory, 2026-10-18

Source: direct developer reports and explicit clarification in this conversation

The developer reported that portal escape attempts froze android movement and caused unavoidable destruction. The accepted behavior is that walking away from a portal cancels its countdown. A warning during portal contact allows ordinary movement, blocks dimension transfer and cancels once contact ends. Staying until zero still causes destruction. The implementation keeps one canonical countdown and records its portal origin. The native regression passed for both End and Nether portals. A generic non-portal transfer attempt remains irreversible.

The developer approved the existing ClankOS boot and permanent self-destruct console copy without edits. A portal cancellation instruction may replace the irreversibility claim for the reversible warning.

The manual android laboratory should include one ready Mars android and communication satellites on Earth and Mars. Their actual satellite link and bandwidth reservation should permit remote control from the Earth capsule. Mars Scout starts with cold protection and RCS so it is usable on arrival. This is laboratory setup through production behavior, without a gameplay bypass.

### Energy, Mars Hazards And Test Portals, 2026-10-18

Source: direct developer feedback and native integration verification in this conversation

Android cold exposure should use more battery for heating instead of biological damage or freezing debuffs. Low pressure should have no penalty. Connected androids consume a base idle load, more when walking, more again when sprinting, and a separate cost per jump. Existing zero-gravity load remains. The initial configurable costs are provisional tuning, not accepted final balance. Normal biological hazard behavior remains separate.

Large center warnings are LOW BATTERY at 10 percent or less and CRITICAL BATTERY at 5 percent or less. Return to the associated dock and disconnect to use its existing charging behavior. Self-destruction should produce one positional explosion sound audible near the physical android. Its local particle presentation should not duplicate audio.

The laboratory should have active End and Nether portals near the Overworld machines. The new isolated session includes them, a ready Mars Scout and actual Earth-Mars communication bandwidth. Native verification covers Mars survival, real activity battery consumption and one server sound at the android position. A fresh manual client reached readiness with the requested display defaults and all prepared fixtures.

The repeated Length chat output in QA screenshots comes from GregTech LINAC construct messages invoked during BlockRenderer multiblock variant scanning. StructureLib writes them to the real chat even when construction uses a preview world. This diagnosis is not an accepted scope expansion to patch those dependencies.

[[Sources]]


## Satellite Visibility And Reserved Bandwidth

Source: developer showcase feedback and native regression, 2026-10-18

Android control reserves communication bandwidth without consuming satellites. Satellite assets and network mirrors belong to the server connection, so switching dimensions must preserve them. They are cleared on disconnect or an authoritative server reset. The previous world-load cleanup discarded the client mirror while server publication cursors prevented unchanged assets from being resent.

Only operational communication satellites contribute usable capacity. Disabled satellites remain deployed and visible. If normal route revalidation cannot retain an android reservation, the operator returns to the biological body and receives one localized connection-loss message. A native regression covers Mars transfer, visible satellites, reserved endpoint/link bandwidth and a real satellite shutdown. The updated skin-layer runtime also passed the focused native renderer smoke. This note remains unreviewed source intake.


## Desktop Closure Review Findings

Source: developer laptop-transfer request and Astra review,2026-10-18

The remote-android-bodies branch is pushed with reviewed corrections for native riding relationships, biological residence inside upright capsules and server denial of unsupported personal Galacticraft equipment access. Robot hurt/death audio reuses vanilla iron-golem assets. No new media was generated. Existing global EnderStorage transfer work remains deferred. Fullpack Galacticraft runtime coverage is unavailable in the isolated laboratory. Two StarMap verification scenarios remain unresolved and are recorded in the local handoff. The developer froze further desktop work for a move to the laptop. This remains unreviewed source intake.
