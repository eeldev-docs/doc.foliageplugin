---
sidebar_position: 3
description: How the Foliage Plugin saves harvested and removed foliage between game sessions.
---

# Saving and Loading

The plugin can save which foliage instances are hidden or removed, so harvested trees stay gone after the game restarts.

## Enabling persistent data
In **Project Settings → Game → Foliage Plugin → Saving and Loading**:

| Setting | Default | Description |
|---|---|---|
| **Enable Persistent Data** | Off | Turns saving and loading on. |
| **Auto Saving Rate** | `60` | Seconds between automatic saves. Minimum 5. |
| **Save Game Name** | `FoliageData` | Name of the save slot. |
| **Save Game Version** | `1` | A save with a different version is not loaded and is overwritten on the next save. |

## When data is loaded and saved
- The save is **loaded** on the server when the Foliage Manager is spawned, that is when the first foliage component starts in a world.
- The data is **saved** every **Auto Saving Rate** seconds.
- To save right away, for example before quitting, call **Save Foliage Data to Disk** on the Foliage Manager. Use **Get Actor of Class** with **FoliagePluginManager** to find it.

:::warning Save before quitting
Changes since the last automatic save are lost if the game is closed without saving. Call **Save Foliage Data to Disk** before you quit or travel to another map.
:::

## What is saved
For every hidden or removed instance, the plugin saves which foliage component it belongs to and its instance index, together with its original and hidden transform.

The respawn timers are not saved. After loading, hidden instances respawn according to the normal [respawn rules](/docfiles/concepts/lifecycle#5-the-instance-respawns).

:::info Editing foliage after release
Painting or erasing foliage in a level changes the instance indices. When a component starts, the plugin checks every saved instance against its original location. If the index has changed, the instance is found again by its location. If no instance is left at that location, the saved entry is dropped and a warning is logged.

Instances that you moved in the editor cannot be found again. Increase **Save Game Version** if you move a lot of foliage in a released level.
:::

## Per-player or per-world save names
All maps share the same save slot by default. To use a different slot, for example per map or per save file, override **Get Save Game Name** in a [Custom Foliage Manager](/docfiles/guides/custom-foliage-manager). You can also override **Save Foliage Data to Disk** to save the data your own way.
