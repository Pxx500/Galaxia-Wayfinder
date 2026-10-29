---
type: source
status: reviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Remote Android Body Architecture Feasibility Research

Source: Remote android architecture research and owner discussion on 2026-10-18. Full research report: `~/.agents/docs/Galaxia/docs/research/2026-10-18-remote-android-feasibility.md`. Local code inspected at Galaxia commit `a9128e9ef21ff05254648190b4f79f94bdc9669d`
Imported: 2026-10-18

## Source Snapshot

This investigation compares ways to operate a team-owned android while leaving the biological body and its belongings in a powered capsule.

The research found a technically credible approach. Keep the connected real `EntityPlayerMP` as the execution actor for the currently controlled body, while explicitly separating operator identity from body state. This is an architecture recommendation awaiting review, not an implemented feature or blanket GTNH compatibility claim.

This note preserves research, provenance and the presentation direction approved in the source conversation. Its findings were reviewed for reconciliation on 2026-10-18. The presentation decision was routed to its owner, and the owner subsequently approved the one-player operator/body architecture. The original findings below describe their research-time status. Review does not independently approve every recommendation or certify implementation. Its only Vault link is [[Sources]].

## Evidence And Version Boundary

The project declares Minecraft `1.7.10`, Forge `10.13.4.1614` and stable mappings `12`. The existing generated source at `~/Documents/GitHub/Galaxia/build/rfg/minecraft-src/java` independently confirms the Forge version. This runtime uses `IExtendedEntityProperties`, rather than modern Forge capability APIs.

The saved resolved compile classpath from 2026-10-17 is at `~/Documents/GitHub/Galaxia/AI/Reviews/library-search/a9bb11bc-7c58-45a9-8886-488d27f3c109/gradle-classpath.json`. It contains GT5 `5.09.54.64`, GTNHLib `0.11.48`, ModularUI2 `2.3.84-1.7.10`, Baubles-Expanded `2.2.21-GTNH`, AE2 `rv3-beta-997-GTNH`, EnderIO `2.10.32`, Galacticraft `3.4.25-GTNH` and Thaumcraft `4.2.3.5`. This is compile classpath evidence, not proof of the owner's installed pack or a fresh server runtime resolution.

The primary [GTNH 2.9.0-RC-2 manifest](https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/master/releases/manifests/2.9.0-RC-2.json) and [daily manifest](https://github.com/GTNewHorizons/DreamAssemblerXXL/blob/master/releases/manifests/daily.json) were read on 2026-10-18. They contain newer versions of several relevant mods. For example, RC-2 has Baubles `2.2.25-GTNH`, GTNHLib `0.11.52` and ServerUtilities `2.4.14`. The daily snapshot has ServerUtilities `2.4.21`. These manifests are research references, not a claim that RC-2 is the current stable release. A future compatibility claim needs an explicitly chosen target pack.

## Recommended Ownership Model

The operator retains account UUID, GameProfile, connection, team membership, permissions and account-level progression. Each body has its own identity, physical state, inventory and equipment. An android also has its own battery, owning team, dock identity and immutable dock dimension.

While controlled, the real connected player executes the android's normal movement, combat, block use and machine GUI interactions at the android's location. The biological body remains represented physically by its capsule and stored body state. It does not need to be a second ticking player with the operator's profile.

An inactive android remains a physical world body with its own belongings. Activation and deactivation transfer authority over that body's state between the inactive representation and the connected player. They must not leave two simultaneously usable copies. A cohesive body lifecycle owner should enforce the one-operator-per-body and one-active-body-per-operator rules and own interrupted transition recovery.

Existing owners remain responsible for their domains. GTNHLib teams and Galaxia's `GTTeamsCompat` supply identity and permissions. `SatelliteNetworkService` owns communication capacity. Existing physical multiblock and energy mechanisms supply the capsule and dock infrastructure. Body lifecycle does not require a new team system, parallel satellite graph, universal possession framework, Rocket redesign, Gantry scheduling, modular satellites or a new data-production chain.

## Why Normal Player Execution Is The Strongest Candidate

`NetHandlerPlayServer` binds normal packets to one connected `playerEntity`. Movement, digging, placement, attacks and container transactions use that player's position, world, inventory and permissions. Client `thePlayer` and `renderViewEntity` are separate, so changing the camera alone does not redirect these interactions.

Stock Forge `FakePlayer` disables GUI opening, normal update, death and dimension travel, and reports invulnerability. The exact local GT5 version also explicitly rejects FakePlayer in both its ModularUI2 and legacy GUI entry points. Sources: [GT5 MetaTileEntityGuiHandler.open](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5.09.54.64/src/main/java/gregtech/api/modularui2/MetaTileEntityGuiHandler.java#L28), [legacy GTUIInfos](https://github.com/GTNewHorizons/GT5-Unofficial/blob/5.09.54.64/src/main/java/gregtech/api/gui/modularui/GTUIInfos.java#L93).

A separate custom living android is possible, but would need its own input, interaction, GUI, chunk streaming and player-API integration. A second EntityPlayerMP needs connection and identity routing and introduces additional lifecycle collisions. These remain alternatives, but have a larger integration burden for ordinary GTNH gameplay.

## Body State, Equipment And Resource Findings

Whole-player NBT is not a safe body-swap contract. Minecraft mixes inventory, health, effects and position with UUID, XP, abilities, respawn locations, Ender Chest and mod attachments. The existing living-entity NBT loader also adds effects without first clearing the current map. The body state boundary must be explicit.

Cursor stacks, the personal crafting matrix and open containers are separate from the main inventory arrays. Their close callbacks can drop items at the current player's location. They need to be settled under the departing body's context. Equipment callbacks, attributes, selected slot, effects and client state also need coherent transition handling.

Baubles-Expanded `2.2.21-GTNH` caches equipment by player name and holds a weak reference to one player. Its living-update callback runs for every EntityPlayer. Two same-name player bodies would therefore share equipment storage and could execute the same worn item against two bodies. Drop handling uses the same cache. The relevant cache and lifecycle were also checked in `2.2.25-GTNH`. Sources: [Baubles player cache](https://github.com/GTNewHorizons/Baubles-Expanded/blob/2.2.21-GTNH/src/main/java/baubles/common/lib/PlayerHandler.java#L85), [Baubles tick and drops](https://github.com/GTNewHorizons/Baubles-Expanded/blob/2.2.21-GTNH/src/main/java/baubles/common/event/EventHandlerEntity.java#L27).

Claims are separate from Galaxia team permissions. ServerUtilities classifies FakePlayer and actors without a network handler as fake, then resolves them to its shared fake-player record. Giving a FakePlayer the operator's profile is insufficient. Ordinary Forge interaction events must remain in the path. Sources: [ServerUtilities fake classification](https://github.com/GTNewHorizons/ServerUtilities/blob/2.4.21/src/main/java/serverutils/lib/util/ServerUtils.java#L46), [player resolution](https://github.com/GTNewHorizons/ServerUtilities/blob/2.4.21/src/main/java/serverutils/lib/data/Universe.java#L602), [claim interaction checks](https://github.com/GTNewHorizons/ServerUtilities/blob/2.4.21/src/main/java/serverutils/data/ClaimedChunks.java#L264).

Separate body inventories do not isolate remote resources. Vanilla Ender Chest follows the operator. EnderStorage pouches access shared storage through owner and frequency data in the item. AE2 wireless terminals combine a real stack, player identity and player position, with special range modes. Thaumcraft research, scans and warp live in name-keyed personal stores outside the ordinary inventory. Shared resource stores and progression must retain their existing authority rather than be copied into body snapshots. Sources: [EnderStorage pouch](https://github.com/GTNewHorizons/EnderStorage/blob/1.8.7/src/main/java/codechicken/enderstorage/storage/item/ItemEnderPouch.java#L43), [AE2 wireless terminal](https://github.com/GTNewHorizons/Applied-Energistics-2-Unofficial/blob/rv3-beta-997-GTNH/src/main/java/appeng/helpers/WirelessTerminalGuiObject.java#L78). Thaumcraft evidence comes from the exact local `4.2.3.5` source archive, not an asserted public implementation repository.

## Satellite Reservations And Physical Residency

Galaxia's current `SatelliteNetworkService` has topology, data buffers, endpoint jobs and short-lived usage pulses. Those pulses are presentation state, not durable session reservations. `SatelliteDataTransferPlanner.plan` starts with empty usage maps. Both network rebuilding and actual data-job execution use the planner.

Active remote control needs real reservations in the existing satellite owner. Data traffic and new sessions must see residual capacity after existing reservations, including shared relays and body-level pools. Checking each session's widest path independently can overbook shared resources. Losing a valid route or enough actual capacity ends the affected session. Restored connectivity must not resume it automatically.

Moving the connected player moves normal client chunk subscriptions to the android. It does not keep the remote capsule simulated. ForgeChunkManager supplies bounded tickets and restoration callbacks, but ticket requests can fail. Keeping a capsule controller loaded does not automatically simulate an arbitrarily distant power source. The capsule's actual required simulation must remain valid throughout control.

## Existing Zero-Gravity Movement Owner

Galaxia already has `ItemReactionControlSystem`, the `reaction_control_system` Baubles slot, `GalaxiaAPI.hasZeroGMovementCapability`, `RelativeMovementMixin` and `ZeroGMovementAPI`. Suitable maneuvering equipment can use this existing domain. The findings do not justify requiring an entire suit.

The current RCS stores enabled state on the shared Item object and previous motion in static fields. Its worn tick can drain oxygen. It is therefore not ready to serve several independently powered bodies unchanged. Body or stack state and electrical accounting need to fit the accepted android rules. Androids must not acquire a hidden oxygen requirement through this implementation. Vacuum electrical load is a separate accepted rule in the newer owning decision, described below.

## Destruction, Transfer And Recovery Findings

Canceling LivingDeathEvent alone is insufficient. The player's health has already reached zero, and later death updates or health sync can still trigger game over. Android destruction needs a body lifecycle transition that resolves the android's belongings and returns the operator to a valid biological state without ordinary player death consequences.

Forge `10.13.4.1614` has no EntityTravelToDimensionEvent in the inspected source. PlayerChangedDimensionEvent is not cancelable and fires after transfer. Entity travel, the EntityPlayerMP override and direct ServerConfigurationManager calls are distinct entry paths. Galaxia's `TeleportRequestPacket` directly invokes the manager.

Galacticraft `3.4.25-GTNH` has a concrete additional bypass. Its WorldUtil custom transfer directly changes the player dimension, sends the respawn packet and changes world state. It does not enter the normal player transfer manager. EnderIO's inspected telepad does use that manager. Prevention must cover actual supported paths before mutation, rather than detect an illegal dimension only after arrival. Sources: [Galacticraft WorldUtil](https://github.com/GTNewHorizons/Galacticraft/blob/3.4.25-GTNH/src/main/java/micdoodle8/mods/galacticraft/core/util/WorldUtil.java#L909), [EnderIO telepad](https://github.com/GTNewHorizons/EnderIO/blob/2.10.32/src/main/java/crazypants/enderio/teleport/telepad/TileTelePad.java#L662).

Player data, Baubles files, body state and world chunks save independently. Normal logout fires before the player save, but autosave can capture an active android, and the ordinary login event occurs after initial loading and world setup. Recovery must have a defined authoritative owner for each inventory and resolve interrupted transitions without restoring stale parallel copies. Atomic replacement of one file is not a multi-file transaction. This is protection of newly created data, not a requirement for legacy save migration.

## Owner-Approved Self-Destruct Presentation

The owner proposed and then approved this presentation direction in this conversation:

- Arm irreversible self-destruction and immediately block dimension departure
- Show a short countdown, with approximately three seconds as an initial tuning value
- Play a fake explosion visible from the android's perspective. It does not kill the active player or damage the surroundings
- Keep that view briefly with interaction blocked, initially around two server ticks
- Settle the android's carried items locally on the departure side, restore the operator to the biological body and then finish removing the android body

Three seconds and two ticks are tuning starting points. The gameplay safety condition applies from arming, before the countdown. Logging out or restarting cannot disarm the body. Loss of capsule power or the link still interrupts control immediately, even during this presentation. The remaining armed body must still reach its terminal outcome.

The local report records this direction in section 11. It has not been verified in a running game. Packet order alone does not guarantee a rendered frame before a dimension respawn, so the short presentation interval needs a focused visual check. No real damaging explosion or zero-health cinematic is required. Approval of this presentation direction did not authorize implementation.

## Reconciliation With Newer Owning Decisions

At intake, the current local note titled Define Remote Android Body Lifecycle already contained further owner decisions from the separate Wayfinder conversation. They take precedence over questions left open in the earlier report:

- The powered capsule sustains the biological body without separate food or oxygen input. It does not grant invulnerability. Destruction or power loss immediately returns the player to normal operation at the capsule location
- Androids remain subject to ordinary damage, including combat, falls, fire and lava. Robotic construction does not automatically grant temperature or radiation protection
- Dock repair consumes materials. Charging restores energy, not health. Natural player regeneration does not repair androids. Passive chassis wear and random failures are not part of the direction
- Vacuum adds an electrical load independently of the zero-gravity load. Both apply when both conditions hold
- EV is the provisional introduction target, using orbital electronics, communications and a physically established destination dock. It is not a player-tier permission check
- Explicit interplanetary logistics also applies to androids and shared storage. Ender Chests, Ender Tanks, AE2 and comparable mechanisms must not bypass physical interplanetary item or fluid transport. Ordinary same-destination AE2 remains usable, while Quantum Rings must not bridge celestial destinations

The current note titled Require Explicit Interplanetary Logistics explicitly states that restricting an android GUI alone is insufficient if automatic infrastructure or a biological player can still use the same bypass. This is a cross-system gameplay requirement with concrete integration work still unverified. It must not be silently treated as already enforced by the proposed body architecture.

This source note preserves that reconciliation. It does not modify either owning decision. The earlier report's questions about the capsule baseline, natural repair and whether interplanetary personal storage should be allowed are historical questions where those owners now supply answers. Mod-provided healing interactions, exact equipment, recipe and energy costs, body-versus-operator attachment boundaries and supported-mod enforcement remain subjects for later review or technical validation.

## Independent Architectural References

Historical [iChun Sync](https://github.com/iChun/Sync/commit/6d149933b31ce326762aabd3515fb780c41d5416), commit `6d149933b31ce326762aabd3515fb780c41d5416`, declares Sync `4.0.0` with Forge `1.7.10-10.13.2.1236` in source build metadata. It stores shell state in tiles and restores the selected shell into the connected player. Its LGPL v3 text and accompanying GPL file were recorded as provenance. This supports same-era feasibility, not GTNH compatibility or reuse of whole-player NBT restoration.

[Ladysnake Requiem](https://github.com/Ladysnake/Requiem/tree/54281728d5f78944955a6e7b952ac4e0835129de), commit `54281728d5f78944955a6e7b952ac4e0835129de`, declares `2.0.0-beta.16`, Minecraft `1.19.3` and Quilt. It coordinates a player with a separate possessed entity and explicitly handles equipment, movement and persistence. Its logout policy removes and reconstructs the host, which differs from Galaxia's persistent inactive world body. The inspected license headers and root code license disagree on GPL version, while art reserves all rights. The full report records the exact license sources and uncertainty.

Only ideas and architectural consequences were studied. No code or assets were copied, translated, adapted, installed or added as dependencies. Galaxia implementation should be independent.

## Verification Boundary

No running-pack compatibility, complete crash-safe storage format, universal interception of arbitrary third-party transfers or visible self-destruct frame has been proven. The useful future evidence is behavior and integration coverage: exclusive control, exact inventory ownership after body changes, Baubles and container transitions, reservations under shared relay contention, destruction without operator death, supported transfer entry points, save/logout interruption, capsule residency and claim-aware machine access.

These are findings and verification needs, not a deferred implementation specification. Future execution should derive implementation detail from the current code and owning decisions when explicitly authorized.

