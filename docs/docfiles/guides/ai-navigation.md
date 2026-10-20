---
sidebar_position: 7
description: Let AI walk where harvested foliage used to stand by rebuilding the navigation mesh at runtime.
---

# AI Navigation

By default the navigation mesh is built in the editor and never changes. AI then keeps walking around trees that were already harvested. With dynamic navigation, the plugin rebuilds the navigation mesh where an instance was harvested, removed or respawned.

## Step 1: Make the navigation mesh dynamic
In **Project Settings → Engine → Navigation Mesh**, set **Runtime Generation** to **Dynamic**. You can also set it on the **RecastNavMesh** actor in your level.

## Step 2: Let the foliage affect navigation
Open the foliage type you paint with and make sure **Can Ever Affect Navigation** is on. Without it, the foliage never cuts holes in the navigation mesh.

## How it works
- When an instance is harvested or removed, the area around both its old and its hidden location is rebuilt, so AI can walk where it stood.
- When an instance respawns, the same area is rebuilt again, so AI walks around it.

The navigation mesh is normally only used on the server, where AI runs.

:::note
Rebuilding the navigation mesh costs CPU time. If you harvest a lot of foliage at once, for example with large radial damage, check the cost with **Unreal Insights** or `stat navigation`.
:::
