---
sidebar_position: 1
description: What happens to a foliage instance from the first hit until it respawns, including uses, lifetimes and blocking checks.
---

# Lifecycle of a Foliage Instance

```
Instance  →  hit  →  Foliage Actor spawned, instance hidden
                         │
                         ├─ harvested Max Uses times  →  depleted  →  destroyed after Depleted Life Time
                         └─ not depleted              →  destroyed after Max Life Time
                                                              │
                         instance respawns (if Enable Respawning)  ←┘
```

## 1. The instance takes damage
When a foliage instance that uses the **FoliagePluginComponent** takes point or radial damage on the server, the plugin:

1. Looks up the instance's mesh in the [Foliage Data Table](/docfiles/reference/data-table-settings). Instances whose mesh is not in any row are ignored.
2. If **Require Damage Type** is on, checks the [damage type and amount](/docfiles/guides/damage-types). If the check fails, the player gets **On Foliage Error Message** and nothing else happens.
3. Spawns the row's **Foliage Actor Class** at the instance's transform, with the instance's mesh.
4. Applies the same damage to the new Foliage Actor, so the first hit counts as a harvest.
5. Hides the instance by moving it down by **Hidden Foliage Move Distance**.

## 2. The Foliage Actor is harvested
Each point or radial damage hit on the Foliage Actor with more than 0 damage:

1. Sends the row's **Rewards on Harvest** to the player with **On Foliage Harvested**. See [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface).
2. Reduces **Remaining Uses** by 1 and calls **BPE On Foliage Damaged**.

A new Foliage Actor starts with **Max Uses** remaining uses. Hitting an actor with no uses left sends **On Foliage Error Message** with **No Uses Left**.

You can change all of this by overriding **Handle Foliage Damage** and **Handle Foliage Reward**. See [Foliage Actor](/docfiles/reference/foliage-actor) and the [Health example](/docfiles/guides/health).

## 3. The Foliage Actor is depleted
When **Remaining Uses** reaches 0:

- **On Foliage Depleted** and **BPE On Foliage Depleted** are called on the server and every client.
- If **Simulate Physics on Depletion** is on, the mesh starts simulating physics. See [Simulating Physics](/docfiles/guides/simulating-physics).
- The actor's lifetime is set to **Depleted Foliage Actor Life Time**.

## 4. The Foliage Actor despawns
A Foliage Actor is destroyed when its lifetime runs out:

- **Foliage Actor Max Life Time** after it was spawned, if it was never depleted.
- **Depleted Foliage Actor Life Time** after it was depleted.

If an object of one of the **Blocked Respawn Object Types** (by default Pawns) is within **Block Foliage Despawn Radius**, the actor is not destroyed yet. Its lifetime is extended by another **Foliage Actor Max Life Time**. This stops actors from disappearing in front of players.

## 5. The instance respawns
If **Enable Respawning** is on for the row, the server tries to respawn hidden instances every **Foliage Respawn Rate** seconds. An instance respawns when all of these are true:

- It has been hidden for at least 20 seconds.
- The Foliage Actor spawned from it has been destroyed.
- No object of the **Blocked Respawn Object Types** is within **Block Foliage Respawn Radius** of it.

If **Enable Respawning** is off, the instance is **removed** instead and never comes back. Removed instances are still [saved](/docfiles/concepts/saving-and-loading) and [replicated](/docfiles/concepts/multiplayer).

:::tip Seeing the blocking checks
With **Enable Debugging** on, each blocking check draws a sphere for 10 seconds: green when an object blocks, red when it does not.
:::
