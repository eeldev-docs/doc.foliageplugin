---
sidebar_position: 5
description: Changes in each version of the Foliage Plugin.
---

# Changelog

## 1.7.9
- Fixed clients restoring the wrong foliage instance when foliage respawned.
- Fixed hidden instances being skipped when several respawned at the same time.
- Instances no longer respawn while the Foliage Actor spawned from them still exists.
- Fixed radial damage converting the wrong instances.
- **BPE On Foliage Damaged** and **Handle Foliage Reward** now receive the actual damage type instead of the base **DamageType** class.
- Fixed duplicate instance data on clients that joined while foliage was changing.
- Fixed several crashes: when a player disconnected while loading, when foliage data arrived before the Foliage Manager on a client, and when a damage type or mesh index was missing.
- Fixed a Foliage Manager being spawned while a level was being unloaded.
- Fixed compiling for Unreal Engine 4.

## 1.7.8
- The Foliage Data Table is now loaded by a Game Instance subsystem.
- The **Foliage Data Table** and **Foliage Manager Class** settings now use proper asset pickers.
- Changed the plugin LoadingPhase to Default.

## 1.7.7
- Fixed foliage instances not being replicated correctly with the new replication system.

## 1.7.5
- Reworked replication: hidden and removed instances are sent to each player in chunks after they join.
- Fixed removed instances not being sent to players who joined later.

## 1.7.4
- Added support for Unreal Engine 5.2.

## 1.7.3
- Fixed a race condition where the plugin initialized before engine modules.
- Fixed delegates not being unbound in the foliage component on EndPlay.

## 1.7.2
- Fixed respawning foliage when auto saving was disabled.

## 1.7.1
- Added support for Unreal Engine 5.1.

## 1.7.0
- Changed the plugin LoadingPhase from PreDefault to Default.

## 1.6.9
- Added support for Chaos Geometry Collections in Unreal Engine 5, in favor of the deprecated Destructible Meshes. The same **Destructible Meshes** array is used for both. See [Destructible Meshes](/docfiles/guides/destructible-meshes).

## 1.6.8
- Added Unreal Engine 5 support.

## 1.6.7
- A missing Data Table is now logged as a warning instead of an error, so it no longer breaks compiling projects without one.
- Fixed compiling non-unity builds.

## 1.6.6
- **Save Foliage Data to Disk** is exposed to Blueprints, so you can force a save.
- Added **Foliage Manager Class** to the Project Settings. See [Custom Foliage Manager](/docfiles/guides/custom-foliage-manager).
- Added the overridable **Get Save Game Name** and **Save Foliage Data to Disk** functions to the Foliage Manager.

## 1.6.5
- The plugin compiles for Unreal Engine 5 Early Access.
- Added Unreal Engine 4.27 support.
- Fixed **BPE On Foliage Depleted** being called twice.

## 1.6.4
- Fixed a CoreTicker that was not cleared when a Foliage Component was destroyed.

## 1.6.3
- Fixed respawning foliage that was deleted with remaining uses above 0.
- Added class and struct exports.
- Fixed an error message when client and server were started at the same time in the editor.

## 1.6.0
- Added Mac and Android support.
- Fixed a crash caused by the Data Table being garbage collected.
- Added more debug messages related to the Data Table.

## 1.5.4
- Added Unreal Engine 4.26 support.

## 1.5.3
- **Handle Foliage Damage** can be overridden in Foliage Actors. See [Health](/docfiles/guides/health).
- Added **Reduce Remaining Uses**, **Set Remaining Uses** and **Add Remaining Uses** to Foliage Actors.

## 1.5.2
- Fixed loading the Data Table in packaged projects.
- Added more debugging output. See [Logging and Debugging](/docfiles/reference/logging).

## 1.5.1
- Network optimizations.

## 1.5
- Added Unreal Engine 4.25 support.

## 1.4.1
- Changed the signature of **Handle Foliage Reward**.
- Reward data can now be modified in Blueprint events.
- **On Foliage Harvested** is now Blueprint callable.
- Optimized replication.
- Fixed blocking object types not always blocking respawns and despawns.

## 1.4
- Moved the Foliage Actor class from the Project Settings to the Data Table, so each resource can have its own Foliage Actor.
- **Rewards on Harvest** now has a Min and Max value.
- **Valid Damage Types** is now a list, so a resource can accept several damage types.

## 1.2
- Added the overridable **Handle Destructible Damage**, **Handle Foliage Reward** and **Handle Foliage Impulse on Depletion** functions to the Foliage Actor.
- Added Linux support.
- Added Unreal Engine 4.22 support.
