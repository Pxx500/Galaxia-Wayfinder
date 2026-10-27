---
type: source
status: unreviewed
tags:
  - galaxia/alpha
  - wayfinder/source
---

# Android Dock Door Access Input

Source: Project lead report during manual android laboratory gameplay
Imported: 2026-10-20

## Source Snapshot

After the dock finishes manufacturing an android, the inactive body causes its airlock to stay closed even when the player is nearby
The owner requested that inactive androids must not lock the dock entrance
The control capsule should retain its protective locking behavior while it contains an inactive body

The owner also asked whether the two multiblocks share their door logic
The implementation currently shares the station lifecycle and door controller in TileEntityBodyStation
This input requests a difference in occupied-station access behavior, not separate duplicate door implementations

[[Sources]]
