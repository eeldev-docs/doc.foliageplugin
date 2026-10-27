---
sidebar_position: 2
description: How the Foliage Plugin replicates foliage on listen and dedicated servers.
---

# Multiplayer

The Foliage Plugin is server authoritative and works on both listen servers and dedicated servers.

## Damage must be applied on the server
Foliage instances and Foliage Actors only react to damage on the server. Damage applied on a client is ignored. Send a Server RPC from the client, and apply the damage from there:

```
Client: Input → Server RPC "Harvest"  →  Server: Line Trace → Apply Point Damage
```

See [Multiplayer Harvesting](/docfiles/guides/multiplayer-harvesting) for the Blueprint.

The [Foliage Plugin Interface](/docfiles/reference/foliage-plugin-interface) events also run on the server.

## What is replicated
| What | How |
|---|---|
| Hidden and removed instances | Sent to every client when they change. |
| Instances changed before a player joined | Sent to the player in chunks once their world has loaded. Changes made while the chunks are being sent follow right after, so the player ends up with the same state as the server. |
| Players already connected when the manager spawns, or after seamless travel | Get the same initial sync as a player who just joined. |
| Foliage Actors | Normal replicated Actors. Mesh, remaining uses and depletion are replicated. |
| Physics movement of depleted actors | Only when **Replicate Physics Movement** is on. See below. |

The **Foliage Manager** that keeps track of the instances is spawned automatically on the server and is always relevant. You never place it in the level yourself. See [Custom Foliage Manager](/docfiles/guides/custom-foliage-manager) if you want to extend it.

## Events on clients
| Event | Server | Clients |
|---|---|---|
| BPE On Foliage Damaged | ✓ | |
| BPE On Foliage Remaining Uses Updated | ✓ | ✓ |
| BPE On Foliage Mesh Updated | ✓ | ✓ |
| BPE On Foliage Depleted | ✓ | ✓ |
| On Foliage Harvested / On Foliage Error Message | ✓ | |

Play effects and sounds from the replicated events, and gameplay logic from the server-only ones.

## Physics movement
**Replicate Physics Movement** in the [Plugin Settings](/docfiles/reference/plugin-settings) is off by default to save bandwidth. Each machine then simulates a falling tree on its own, so the end positions can differ slightly. Turn it on only if the position of depleted actors matters for gameplay.
