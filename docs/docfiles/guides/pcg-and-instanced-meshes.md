---
sidebar_position: 8
description: Harvest instances spawned by PCG or added to your own Instanced Static Mesh components.
---

# PCG and Instanced Static Meshes

The plugin is not limited to foliage painted with the Foliage tool. Any instances in a **FoliagePluginComponent** can be harvested, also when they are spawned by PCG or added to a component in your own Actor.

The rest works the same as for painted foliage. The mesh must be in the [Foliage Data Table](/docfiles/reference/data-table-settings), and the instances must block the trace or projectile that applies the damage.

## PCG
In the **Static Mesh Spawner** node, open the **Descriptor** of every mesh entry you want to harvest and set **Component Class** to **FoliagePluginComponent**.

In the same Descriptor, set the collision so the instances block your traces, for example **BlockAll** or your own profile.

PCG can generate the instances in the editor or at runtime:

- **Generated in the editor:** the instances are saved in the level and work like painted foliage.
- **Generated at runtime:** generation must run on the server and on every client, so all of them have the instances. When PCG adds or removes instances, for example when a partition is generated again, the plugin waits until the instances have stopped changing for 0.5 seconds and then hides the harvested instances again.

:::tip
When you switch a PCG component to **Generate At Runtime**, PCG removes the instances that were generated in the editor. They are generated again around the player when you play. To see them in the editor too, select the **PCGWorldActor** and turn on **Treat Editor Viewport As Generation Source**.
:::

## Your own Actor
Add a **FoliagePluginComponent** to an Actor, set its static mesh and add instances to it, in the editor or at runtime with **Add Instance**. Make sure **Can Be Damaged** is on for the Actor.

## How instances are found again
A harvested instance is stored with its mesh and its original location. When a component starts or its instances change, the plugin finds the instance again by that mesh and location, even if the component is a new one. A regenerated PCG component therefore keeps the harvested and removed state of the old one, also after [saving and loading](/docfiles/concepts/saving-and-loading).

:::note
Two instances of the same mesh at the same location count as the same instance.
:::
