---
sidebar_position: 1
description: What happens to a foliage instance from the first hit until it respawns, including uses, lifetimes, stumps, regrowth and blocking checks.
---

# Lifecycle of a Foliage Instance

```
Instance  →  hit or interaction  →  Foliage Actor spawned, instance hidden (stump shown)
                                         │
                                         ├─ harvested Max Uses times  →  depleted  →  destroyed after Depleted Life Time
                                         │                                                   │
                                         │              instance respawns after Respawn Delay  ←┘  (regrows, if Enable Respawning)
                                         │
                                         └─ not depleted, no hits for Idle Reset Time  →  turns back into the instance right away
```

## 1. The instance is hit
When a foliage instance that uses the **FoliagePluginComponent** takes point or radial damage on the server, or a player [interacts](/docfiles/guides/interaction-and-pickups) with it, the plugin:

1. Looks up the instance's mesh in the [Foliage Data Table](/docfiles/reference/data-table-settings). Instances whose mesh is not in any row are ignored.
2. For damage, if **Require Damage Type** is on, checks the [damage type and amount](/docfiles/guides/damage-types). If the check fails, the player gets **On Foliage Error Message** and nothing else happens. For an interaction, checks that **Allow Interaction** is on instead.
3. Spawns the row's **Foliage Actor Class** at the instance's transform, with the instance's mesh, or takes one from the [pool](/docfiles/reference/foliage-actor#actor-pooling).
4. Applies the same damage to the new Foliage Actor, or interacts with it, so the first hit already counts as a harvest.
5. Hides the instance by moving it down by **Hidden Foliage Move Distance**, and shows the **Stump Mesh** if the row has one.

If **Harvest Without Actor** is on for the row, steps 3 and 4 are skipped. The player gets the rewards right away, and the instance is hidden until it respawns, or removed if **Enable Respawning** is off. See [Pickups without a Foliage Actor](/docfiles/guides/interaction-and-pickups#pickups-without-a-foliage-actor).

## 2. The Foliage Actor is harvested
Each point or radial damage hit on the Foliage Actor with more than 0 damage, and each call to **Interact**:

1. Sends the row's **Rewards on Harvest** to the player with **On Foliage Harvested**. See [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface).
2. Reduces **Remaining Uses** by 1 and calls **BPE On Foliage Damaged**, or **BPE On Foliage Interacted** for an interaction.

A new Foliage Actor starts with **Max Uses** remaining uses. Hitting an actor with no uses left sends **On Foliage Error Message** with **No Uses Left**.

You can change all of this by overriding **Handle Foliage Damage** and **Handle Foliage Reward**. See [Foliage Actor](/docfiles/reference/foliage-actor) and the [Health example](/docfiles/guides/health).

## 3. The Foliage Actor is depleted
When **Remaining Uses** reaches 0:

- **On Foliage Depleted** and **BPE On Foliage Depleted** are called on the server and every client.
- If **Simulate Physics on Depletion** is on, the mesh starts simulating physics. See [Simulating Physics](/docfiles/guides/simulating-physics).
- The actor's lifetime is set to **Depleted Foliage Actor Life Time**.

## 4. The Foliage Actor is done
When the actor's lifetime runs out:

- **Depleted:** the actor is destroyed, or returned to the [pool](/docfiles/reference/foliage-actor#actor-pooling). The instance stays hidden until it respawns.
- **Not depleted:** the actor is removed and the instance comes back right away with full uses, as if it was never hit. This happens after **Idle Reset Time** seconds without a hit, or after **Foliage Actor Max Life Time** if **Idle Reset Time** is `0`.

If an object of one of the **Blocked Respawn Object Types** (by default Pawns) is within **Block Foliage Despawn Radius**, this is postponed and the lifetime is extended again. This stops actors from disappearing in front of players.

## 5. While the instance is harvested
The instance stays hidden, and the **Stump Mesh** is shown where it stood. The stump is also shown to players who join later, and after [loading a save](/docfiles/concepts/saving-and-loading). See [Stumps and Regrowth](/docfiles/guides/stumps-and-regrowth).

## 6. The instance respawns
If **Enable Respawning** is on for the row, the server checks every **Foliage Respawn Rate** seconds which hidden instances can respawn. An instance respawns when all of these are true:

- **Respawn Delay** seconds have passed since it was first hit. This is real time, so it also counts while the server is offline.
- The Foliage Actor spawned from it is gone.
- No object of the **Blocked Respawn Object Types** is within **Block Foliage Respawn Radius** of it.

The blocking checks are spread over several frames, at most **Max Respawn Checks Per Frame** per frame, so many respawns at once do not stall the server.

When the instance respawns, the stump is removed. If **Regrow Duration** is more than `0`, the instance grows from small to full size over that time.

If **Enable Respawning** is off, the instance is **removed** instead and never comes back. Removed instances are still [saved](/docfiles/concepts/saving-and-loading) and [replicated](/docfiles/concepts/multiplayer).

:::tip Seeing the blocking checks
With **Enable Debugging** on, each blocking check draws a sphere for 10 seconds: green when an object blocks, red when it does not.
:::

## Restoring everything
Call **Restore All Foliage Instances** on the Foliage Manager to bring back every hidden and removed instance at once, for example when a new round starts. It runs on the server, is spread over several frames, and ignores **Respawn Delay** and the blocking checks. Foliage Actors that still exist are removed first, or returned to the pool. See [Blueprint Functions](/docfiles/reference/blueprint-functions#foliage-manager).
