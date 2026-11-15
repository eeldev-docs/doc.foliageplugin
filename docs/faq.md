---
sidebar_position: 4
sidebar_label: FAQ & Troubleshooting
description: Answers to common questions and problems with the Foliage Plugin.
---

# FAQ & Troubleshooting

## Nothing happens when I hit the foliage
Check these in order:

1. **Damage is applied on the server.** Damage on a client is ignored. See [Multiplayer](/docfiles/concepts/multiplayer).
2. **The foliage type uses FoliagePluginComponent** as its **Component Class**, or **Auto Convert Instanced Meshes** is on. See [Setting up Foliage](/docfiles/getting_started/setup#step-4-use-the-foliage-plugin-component-on-your-foliage-types).
3. **The trace or projectile hits the foliage.** The foliage needs collision that blocks your trace channel. See [Collision Setup](/docfiles/guides/collision-setup).
4. **The mesh is in the Data Table.** The painted mesh must be in **Foliage Meshes** in a row, and **Foliage Data Table** must be set in the Project Settings.
5. **The row has a Foliage Actor Class**, or **Harvest Without Actor** is on.
6. **The damage type is valid** if **Require Damage Type** is on. See [Damage Types](/docfiles/guides/damage-types).

Turn on **Enable Debugging** and [verbose logging](/docfiles/reference/logging). The messages tell you which step fails.

## The foliage turns into an Actor, but I get no reward
None of the Instigator, the Instigator's Pawn and the Damage Causer implements the **Foliage Plugin Interface**. Make sure you pass the player's Controller as **Event Instigator**, or the Actor that implements the interface as **Damage Causer**. See [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface).

## The player gets the reward twice
Only one target receives **On Foliage Harvested**, so this does not come from the plugin. Check that you do not apply damage twice, for example from both the client and the server, or from both a trace and a projectile.

## Interact With Foliage does nothing
- It must be called on the server.
- **Allow Interaction** must be on for the row.
- The **Hit** must come from a trace that hit the foliage instance or the Foliage Actor.

See [Interaction and Pickups](/docfiles/guides/interaction-and-pickups).

## The reward amount is always the same
**Min** and **Max** in **Number of Rewards** are only data. Pick the amount yourself, for example with **Random Integer in Range**. See [Harvesting Foliage](/docfiles/getting_started/harvesting#step-2-add-the-rewards-to-your-inventory).

## The player gets a reward on the first hit
That is the default: every hit is a harvest, including the first one. Use a [Health value](/docfiles/guides/health) to require several hits per harvest.

## Foliage does not respawn
- **Enable Respawning** is off for the row, so the instance was removed.
- A player or another blocking object is within **Block Foliage Respawn Radius**.
- The Foliage Actor still exists. It may be kept alive by a player within **Block Foliage Despawn Radius**.
- The row's **Respawn Delay** has not passed yet.
- Respawns are only attempted every **Foliage Respawn Rate** seconds, 60 by default.

See [Lifecycle of a Foliage Instance](/docfiles/concepts/lifecycle).

## Foliage Actors never despawn
A player or another object of the **Blocked Respawn Object Types** is within **Block Foliage Despawn Radius**, so the lifetime keeps being extended. Lower the radius or change the object types in the [Plugin Settings](/docfiles/reference/plugin-settings).

## Trees do not fall over
See [Simulating Physics → Troubleshooting](/docfiles/guides/simulating-physics#troubleshooting).

## Harvested foliage comes back after restarting the game
Turn on **Enable Persistent Data** and save before quitting. See [Saving and Loading](/docfiles/concepts/saving-and-loading).

## After an update, the wrong trees are hidden
The save finds instances by their mesh and original location, so painting or erasing foliage is fine. Trees that you **moved** in the editor cannot be found again. Increase **Save Game Version** when you ship a level where a lot of foliage was moved. See [Saving and Loading](/docfiles/concepts/saving-and-loading#what-is-saved).

## Harvested foliage from one level shows up in another
Turn on **Save File Per Level**, so every level gets its own save file. See [Saving and Loading](/docfiles/concepts/saving-and-loading#one-save-file-per-level).

## Can I use it with World Partition or level streaming?
Yes. Foliage in streamed levels picks up its hidden and removed instances when it is loaded. Respawn timers are real time, so an instance in an unloaded cell respawns on schedule and is shown when the cell loads again.

## My Foliage Actor keeps old state when it is reused
With **Enable Actor Pooling** on, actors are reused and **Begin Play** only runs once. Reset your own state in **BPE On Foliage Returned To Pool**. See [Actor pooling](/docfiles/reference/foliage-actor#actor-pooling).

## I see "Failed initializing foliage component" in the log
A foliage component uses a mesh that is not in your Data Table. This is expected for foliage you do not want to harvest. Switch those foliage types back to the default component class to remove the message, or use **Auto Convert Instanced Meshes**, which only converts meshes that are in the Data Table.
