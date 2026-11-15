---
sidebar_position: 5
description: What changed in each version of the Foliage Plugin.
---

# Changelog

## 2.1.0

:::warning Check this when you upgrade
- **On Foliage Harvested** is now sent to one target only: the first of the Instigator, the Instigator's Pawn and the Damage Causer that implements the [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface). Before, both the Instigator and the Damage Causer could receive it, so a player could get the reward twice.
- **Save File Per Level** is on by default. The first time a level loads without its own save file, it reads the shared file once and moves its data over. Turn the setting off to keep one file for all levels. See [One save file per level](/docfiles/concepts/saving-and-loading#one-save-file-per-level).
- A Foliage Actor that runs out of time without being depleted no longer counts as depleted. **BPE On Foliage Depleted** and the physics only run when the uses reach 0, so loot you drop in that event is no longer given for free.
- The save finds instances by their mesh and original location instead of their index. Saves from older versions still load.
- The default **Field System Actor** is now **FoliagePluginFieldSystemActor** instead of the engine's `FS_MasterField`. If your Plugin Settings still point to `FS_MasterField`, reset the setting. See [Field System Actor](/docfiles/guides/destructible-meshes#field-system-actor).
:::

### New
- **Interaction and pickups.** **Interact With Foliage** harvests without damage, for example to pick berries. **Harvest Without Actor** gives the rewards and hides the instance without spawning a Foliage Actor. See [Interaction and Pickups](/docfiles/guides/interaction-and-pickups).
- **Respawn Delay** per Data Table row, instead of a fixed 20 seconds. The delay is real time and is saved, so it continues while the server is offline.
- **Stumps and regrowth.** A **Stump Mesh** shows where a harvested instance stood, and **Regrow Duration** lets it grow back when it respawns. See [Stumps and Regrowth](/docfiles/guides/stumps-and-regrowth).
- **Idle Reset Time** per row: a Foliage Actor that is not depleted turns back into the instance, with full uses, after this many seconds without hits.
- **Actor pooling.** Foliage Actors can be reused instead of spawned and destroyed. See [Actor pooling](/docfiles/reference/foliage-actor#actor-pooling).
- **PCG and Instanced Static Meshes.** Instances spawned by PCG or added to your own components can be harvested, and keep their state when PCG generates them again. See [PCG and Instanced Static Meshes](/docfiles/guides/pcg-and-instanced-meshes).
- **Auto Convert Instanced Meshes** converts painted foliage, or all instanced meshes, when a level loads, so you don't have to change the **Component Class**. See [Automatic conversion](/docfiles/guides/pcg-and-instanced-meshes#automatic-conversion).
- A [Blueprint function library](/docfiles/reference/blueprint-functions): **Is Harvestable Foliage**, **Get Foliage Data From Hit**, **Get Foliage Actor From Hit** and **Get Foliage Manager**.
- **Remove Foliage Instance** on the Foliage Plugin Component, and **Restore All Foliage Instances**, **Get Num Harvested Instances** and the save functions on the Foliage Manager.
- New Foliage Actor events: **BPE On Foliage Interacted** and **BPE On Foliage Returned To Pool**.

### Improved
- Faster lookups and smaller network messages in levels with a lot of harvested foliage.
- Respawn checks are spread over several frames, limited by the new **Max Respawn Checks Per Frame** setting.

### Fixed
- Foliage with **Enable Respawning** off disappeared for good after a single hit, even when the Foliage Actor was never depleted.
- Respawn timers restarted when the server restarted, so every saved instance respawned at the first check.
- Clients got an extra, empty Geometry Collection Actor for every destructible mesh.
- Destructible meshes could fail to break in packaged builds, because the default Field System Actor was an editor asset.
- Material overrides on the foliage were lost when it turned into a Foliage Actor.
- Trees fell in a different direction on the server and on each client.
- The damage handler was not bound if something else had already bound the instance damage event.
- Remaining uses on clients could be lost when they arrived before the Foliage Actor's data.
- Harvested foliage from one level was loaded and replicated in every other level.
