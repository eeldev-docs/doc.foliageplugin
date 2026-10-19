---
sidebar_position: 4
description: Set up simple collision on a tree mesh for interaction and physics.
---

# Collision Setup

Good collision matters for every game, and especially when meshes simulate physics: complex collision is **very expensive** to simulate. This example sets up a simple capsule collision on a tree. It will not fit every mesh, but it is a good starting point.

## Step 1: Open the mesh
Open the static mesh in the Static Mesh Editor.

![Static Mesh Editor](../../../static/img/legacy/1-3-1024x721.jpg)

## Step 2: Remove the existing collision
Remove all collision on the mesh, so you can add your own simple collision. Do not use complex collision here.

![Remove collision](../../../static/img/legacy/2-4-1024x719.jpg)

Turn on **Simple Collision** and **Complex Collision** in the viewport's **Show** menu. The mesh should show no collision outlines.

![No collision outlines](../../../static/img/legacy/3-1-1024x723.jpg)

## Step 3: Add a simple collision
Add a capsule collision from the **Collision** menu.

![Add a capsule collision](../../../static/img/legacy/4-1024x309.jpg)

The capsule is usually too big at first:

![The new capsule collision](../../../static/img/legacy/5-1024x846.jpg)

Use the transform tools to scale and move the capsule so it fits the trunk. Simple is better than exact.

![Capsule fitted to the trunk](../../../static/img/legacy/6-1024x721.jpg)

Save the mesh. It now has collision that works for both interaction and physics.
