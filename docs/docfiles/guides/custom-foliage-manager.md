---
sidebar_position: 6
description: Use your own Foliage Manager class, for example to change the save game name at runtime.
---

# Custom Foliage Manager

The **Foliage Manager** keeps track of hidden and removed instances, respawns them, replicates them and saves them. It is spawned automatically on the server. You can replace it with your own subclass to customize saving.

## Step 1: Create the class
Create a Blueprint class with **FoliagePluginManager** as the parent class, and set it as **Foliage Manager Class** in **Project Settings → Game → Foliage Plugin**.

![Set the Foliage Manager Class](../../../static/img/legacy/customclass-1-1024x519.png)

## Step 2: Override the functions you need
| Function | Use it to |
|---|---|
| **Get Save Game Name** | Return the save slot name to use, for example one per map or per save file. Overrides **Save Game Name** in the Project Settings. |
| **Save Foliage Data to Disk** | Replace how the data is saved. Return true on success. Also called when the manager ends play if there are unsaved changes. Check **Is Saving Synchronously** to finish the save before you return. |

![Override Get Save Game Name](../../../static/img/legacy/implement-1024x714.png)

Return the name you want to use:

![Custom save game name](../../../static/img/legacy/customname-1-1024x572.png)

See [Saving and Loading](/docfiles/concepts/saving-and-loading) for how saving works.
