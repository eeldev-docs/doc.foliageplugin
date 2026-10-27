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
- Every **Auto Saving Rate** seconds, the data is **saved** if something changed since the last save. If nothing changed, nothing is written.
- Automatic and manual saves are written to disk on a background thread, so the game does not stall. The data is captured when the save starts.
- When the Foliage Manager ends play, for example when the game quits or travels to another map, unsaved changes are saved right away. This save waits until it is written.
- To save right away, call **Save Foliage Data to Disk** on the Foliage Manager. Use **Get Actor of Class** with **FoliagePluginManager** to find it. It always saves, even if nothing changed.

| Function | Description |
|---|---|
| **Is Foliage Data Dirty** | True if something changed since the last save. |
| **Is Saving Foliage Data** | True while a background save is being written. |
| **Mark Foliage Data Dirty** | Makes the next automatic save write the data. Server only. Available in a [Custom Foliage Manager](/docfiles/guides/custom-foliage-manager). |
| **Is Saving Synchronously** | True during the save made when the manager ends play. Available in a Custom Foliage Manager. |

:::note
**Save Foliage Data to Disk** returns true when the background save has started. The result is shown as a debug message and logged when the write is done. If a save fails, the data stays dirty and is saved again on the next automatic save.
:::

## What is saved
For every hidden or removed instance, the plugin saves which foliage component it belongs to, its instance index and its mesh, together with its original and hidden transform.

The respawn timers are not saved. After loading, hidden instances respawn according to the normal [respawn rules](/docfiles/concepts/lifecycle#5-the-instance-respawns).

:::info Editing foliage after release
When a component starts, the plugin finds every saved instance again by its mesh and original location. This means saved data still works when:

- Foliage is painted or erased in the level, which changes the instance indices.
- A component is replaced by a new one, for example when PCG generates again or foliage ends up in another World Partition cell.

If no instance of the same mesh is left at that location in the component the entry belongs to, the saved entry is dropped and a warning is logged.

Instances that you moved in the editor cannot be found again. Increase **Save Game Version** if you move a lot of foliage in a released level.
:::

:::note Saves from version 2.0
Saves from 2.0 do not include the mesh. These entries are still found by component and instance index, and get the mesh the first time their component starts.
:::

## Per-player or per-world save names
All maps share the same save slot by default. To use a different slot, for example per map or per save file, override **Get Save Game Name** in a [Custom Foliage Manager](/docfiles/guides/custom-foliage-manager). You can also override **Save Foliage Data to Disk** to save the data your own way.
