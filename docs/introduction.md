---
sidebar_position: 1
slug: /
description: Foliage Plugin converts Unreal Engine foliage instances into interactive, harvestable Actors with replication, saving and respawning.
---

# Introduction

## What is the Foliage Plugin?
The Foliage Plugin lets players interact with the foliage you paint in your levels: trees, rocks, bushes or any other static mesh. When a foliage instance takes damage, the plugin replaces it with an Actor that you control. That Actor can be harvested, give rewards, simulate physics, break apart, and later respawn as foliage again.

```
Foliage Instance  →  (takes damage)  →  Foliage Actor  →  (harvested / depleted)  →  despawns  →  instance respawns
```

You keep using Unreal Engine's normal foliage workflow. You only change the foliage type's component class, or let the plugin convert it for you, and describe each resource in a Data Table.

## Features
- **Convert foliage instances into Actors** when they take point or radial damage.
- **Harvest without damage**, for example to pick berries, and **pickups** that give rewards without spawning an Actor. See [Interaction and Pickups](/docfiles/guides/interaction-and-pickups).
- **Resources defined in a Data Table**: meshes, rewards, number of uses, lifetimes, respawning and physics per resource. See [Data Table Settings](/docfiles/reference/data-table-settings).
- **Rewards on harvest** sent to the player through the [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface).
- **Damage types**, for example requiring an axe for trees and a pickaxe for rocks. See [Damage Types](/docfiles/guides/damage-types).
- **Respawning and removing** instances, with a respawn delay per resource and blocking checks so foliage never pops up in front of a player. See [Lifecycle of a Foliage Instance](/docfiles/concepts/lifecycle).
- **Stumps and regrowth**: show a stump while a tree is gone, and let it grow back when it respawns. See [Stumps and Regrowth](/docfiles/guides/stumps-and-regrowth).
- **Saving and loading** of every modified instance between sessions, with one save file per level. See [Saving and Loading](/docfiles/concepts/saving-and-loading).
- **Full replication** on listen and dedicated servers, including players who join later. See [Multiplayer](/docfiles/concepts/multiplayer).
- **Destructible meshes** with Chaos Geometry Collections. See [Destructible Meshes](/docfiles/guides/destructible-meshes).
- **Physics on depletion**, for example trees that fall over. See [Simulating Physics](/docfiles/guides/simulating-physics).
- **PCG and Instanced Static Meshes**, with optional automatic conversion of existing foliage. See [PCG and Instanced Static Meshes](/docfiles/guides/pcg-and-instanced-meshes).
- **Actor pooling** for games where players harvest a lot. See [Foliage Actor](/docfiles/reference/foliage-actor#actor-pooling).
- **Blueprint overridable** damage, reward and depletion logic, and a [Blueprint function library](/docfiles/reference/blueprint-functions). See [Foliage Actor](/docfiles/reference/foliage-actor).
- Works with **level streaming**, World Partition, World Composition and tiled landscapes.

## Common use cases
Harvestable trees, mineable rocks, berry bushes, resource nodes and other interactive environment objects in survival, crafting and open-world games.

## Requirements
| | |
|---|---|
| Unreal Engine | 5.1 – 5.8 on [Fab](https://www.fab.com/listings/de03e7a7-aefe-4290-8fb3-8cde3a34fbf9) |
| Target platforms | Windows, Linux, Mac, Android, iOS |
| Networking | Listen servers and dedicated servers. Damage must be applied on the server. |

## Where to go next
1. [Install the plugin](/docfiles/getting_started/installing)
2. [Set up your foliage and Data Table](/docfiles/getting_started/setup)
3. [Set up your character to harvest foliage](/docfiles/getting_started/harvesting)
4. Read [Lifecycle of a Foliage Instance](/docfiles/concepts/lifecycle) to understand when Actors despawn and instances respawn.
