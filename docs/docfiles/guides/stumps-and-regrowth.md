---
sidebar_position: 13
description: Show a stump where a tree was cut down and let respawned foliage grow back over time.
---

# Stumps and Regrowth

By default a harvested instance disappears completely and comes back at full size. Two settings in the [Data Table](/docfiles/reference/data-table-settings) make this look more natural.

## Stump Mesh
Set **Stump Mesh** to a static mesh, for example a tree stump or an empty bush. While the instance is harvested, the stump is shown at its location, with the same rotation and scale as the instance.

- The stump appears as soon as the instance is hidden, also while the Foliage Actor still stands or lies there.
- It is removed when the instance respawns or the actor turns back into the instance.
- Removed instances, with **Enable Respawning** off, keep their stump for good.
- Stumps are shown on every client, to players who join later, and after [loading a save](/docfiles/concepts/saving-and-loading).

The stumps of a foliage component are drawn as instances of one extra instanced mesh component, so even thousands of stumps are cheap. They use the collision profile and shadow setting of the foliage component, so players collide with them like with the foliage.

:::note
The stump uses the instance's pivot. Make sure the stump mesh has its pivot at the same place as the full mesh, usually at the bottom.
:::

## Regrow Duration
Set **Regrow Duration** to the number of seconds a respawned instance takes to grow from 5% to its full size. `0` respawns it at full size right away.

- The growth only plays when the instance respawns after **Respawn Delay**. When a Foliage Actor that was not depleted turns back into the instance, or when you call **Restore All Foliage Instances**, it comes back at full size.
- The growth plays on each machine on its own, and nothing extra is sent over the network.
- The instance can be harvested while it is growing.

:::tip
Combine both for trees: a stump while the tree is gone, and a young tree that grows into a full one when it respawns.
:::
