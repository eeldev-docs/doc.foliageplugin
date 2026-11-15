---
sidebar_position: 2
description: Every column of a row in the Foliage Data Table.
---

# Data Table Settings

Each row in the Foliage Data Table (row structure **FoliageData**) describes one resource, such as a tree or a rock.

![A row in the Foliage Data Table](../../../static/img/settings/data-table-row.png)

## Settings
| Column | Default | Description |
|---|---|---|
| **Resource Name** | | A display name for the resource, for example *Tree*. |
| **Rewards on Harvest** | | The rewards given on each harvest. Each reward has a **Reward Name** and a **Number of Rewards** with **Min** and **Max**. You pick the actual amount when you receive the reward, see [Harvesting Foliage](/docfiles/getting_started/harvesting#step-2-add-the-rewards-to-your-inventory). |
| **Foliage Meshes** | | The static meshes that belong to this resource. A foliage instance uses this row when its mesh is in this list. A mesh should only be in one row. |
| **Destructible Meshes** | | Optional destructible versions of the meshes, at the **same index** as in **Foliage Meshes**. Use Geometry Collections. See [Destructible Meshes](/docfiles/guides/destructible-meshes). |
| **Foliage Actor Class** | None | The Foliage Actor spawned when an instance takes damage. **Required**, unless **Harvest Without Actor** is on. |
| **Max Uses** | `3` | How many times the resource can be harvested before it is depleted. |
| **Foliage Actor Max Life Time** | `120` | Seconds before a Foliage Actor that was not depleted turns back into the foliage instance. Extended while a player is nearby. |
| **Depleted Foliage Actor Life Time** | `30` | Seconds a depleted Foliage Actor stays before it is destroyed. |
| **Enable Respawning** | On | When on, the instance respawns after the actor is gone. When off, it is removed for good. |
| **Respawn Delay** | `20` | Minimum seconds after the first hit before the instance respawns. It never respawns while its Foliage Actor still exists. The delay is real time, so it also runs while the server is offline. |
| **Regrow Duration** | `0` | Seconds a respawned instance takes to grow from small to full size. `0` respawns it at full size right away. See [Stumps and Regrowth](/docfiles/guides/stumps-and-regrowth). |
| **Stump Mesh** | None | A mesh shown where the instance stood while it is harvested, for example a tree stump. Leave empty to show nothing. See [Stumps and Regrowth](/docfiles/guides/stumps-and-regrowth). |
| **Idle Reset Time** | `0` | Seconds without hits before a Foliage Actor that is not depleted turns back into the foliage instance with full uses. Every hit starts the time again. `0` uses **Foliage Actor Max Life Time** instead. |

See [Lifecycle of a Foliage Instance](/docfiles/concepts/lifecycle) for how uses and lifetimes work together.

## Interaction
| Column | Default | Description |
|---|---|---|
| **Allow Interaction** | On | Allows harvesting without damage with **Interact With Foliage**, for example to pick berries. |
| **Harvest Without Actor** | Off | Gives the rewards and removes the instance on the first hit or interaction, without spawning a Foliage Actor. Use it for pickups such as berries, mushrooms and stones. **Foliage Actor Class** is not needed. |

See [Interaction and Pickups](/docfiles/guides/interaction-and-pickups).

## Damage
| Column | Default | Description |
|---|---|---|
| **Require Damage Type** | Off | Only accept hits that pass the damage check below. Interactions skip this check. |
| **Valid Damage Types** | | The damage types that can harvest this resource. |
| **Damage Amount** | `1` | The minimum damage per hit. |

See [Damage Types](/docfiles/guides/damage-types).

## Physics
| Column | Default | Description |
|---|---|---|
| **Simulate Physics on Depletion** | Off | Simulate physics when depleted, for example a falling tree. Ignored if the resource has a destructible mesh. |
| **Apply Impulse on Depletion** | Off | Push the mesh with an impulse when it starts simulating. |
| **Physics Impulse Multiplier** | `10` | Strength of the impulse. |
| **Physics Collision Profile Name** | `None` | Collision profile to use while simulating. `None` keeps the current profile. |

See [Simulating Physics](/docfiles/guides/simulating-physics).
