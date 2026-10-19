---
sidebar_position: 4
sidebar_label: FAQ & Troubleshooting
description: Answers to common questions and problems with the Foliage Plugin.
---

# FAQ & Troubleshooting

## Nothing happens when I hit the foliage
Check these in order:

1. **Damage is applied on the server.** Damage on a client is ignored. See [Multiplayer](/docfiles/concepts/multiplayer).
2. **The foliage type uses FoliagePluginComponent** as its **Component Class**. See [Setting up Foliage](/docfiles/getting_started/setup#step-4-use-the-foliage-plugin-component-on-your-foliage-types).
3. **The trace or projectile hits the foliage.** The foliage needs collision that blocks your trace channel. See [Collision Setup](/docfiles/guides/collision-setup).
4. **The mesh is in the Data Table.** The painted mesh must be in **Foliage Meshes** in a row, and **Foliage Data Table** must be set in the Project Settings.
5. **The row has a Foliage Actor Class.**
6. **The damage type is valid** if **Require Damage Type** is on. See [Damage Types](/docfiles/guides/damage-types).

Turn on **Enable Debugging** and [verbose logging](/docfiles/reference/logging). The messages tell you which step fails.

## The foliage turns into an Actor, but I get no reward
Neither the Instigator nor the Damage Causer implements the **Foliage Plugin Interface**. Note that the Instigator is a **Controller**: if you implement the interface on your Character, pass the Character as **Damage Causer**. See [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface).

## The reward amount is always the same
**Min** and **Max** in **Number of Rewards** are only data. Pick the amount yourself, for example with **Random Integer in Range**. See [Harvesting Foliage](/docfiles/getting_started/harvesting#step-2-add-the-rewards-to-your-inventory).

## The player gets a reward on the first hit
That is the default: every hit is a harvest, including the first one. Use a [Health value](/docfiles/guides/health) to require several hits per harvest.

## Foliage does not respawn
- **Enable Respawning** is off for the row, so the instance was removed.
- A player or another blocking object is within **Block Foliage Respawn Radius**.
- The Foliage Actor still exists. It may be kept alive by a player within **Block Foliage Despawn Radius**.
- Respawns are only attempted every **Foliage Respawn Rate** seconds, 60 by default.

See [Lifecycle of a Foliage Instance](/docfiles/concepts/lifecycle).

## Foliage Actors never despawn
A player or another object of the **Blocked Respawn Object Types** is within **Block Foliage Despawn Radius**, so the lifetime keeps being extended. Lower the radius or change the object types in the [Plugin Settings](/docfiles/reference/plugin-settings).

## Trees do not fall over
See [Simulating Physics → Troubleshooting](/docfiles/guides/simulating-physics#troubleshooting).

## Harvested foliage comes back after restarting the game
Turn on **Enable Persistent Data** and save before quitting. See [Saving and Loading](/docfiles/concepts/saving-and-loading).

## After an update, the wrong trees are hidden
The save identifies instances by their index, and painting or erasing foliage changes the indices. Increase **Save Game Version** when you ship a level with changed foliage. See [Saving and Loading](/docfiles/concepts/saving-and-loading#what-is-saved).

## Can I use it with World Partition or level streaming?
Yes. Foliage in streamed levels picks up its hidden and removed instances when it is loaded.

## I see "Failed initializing foliage component" in the log
A foliage component uses a mesh that is not in your Data Table. This is expected for foliage you do not want to harvest. Switch those foliage types back to the default component class to remove the message.
