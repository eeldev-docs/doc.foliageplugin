---
sidebar_position: 4
description: The Foliage Plugin Interface that receives rewards and error messages when foliage is harvested.
---

# Foliage Plugin Interface

Implement the **Foliage Plugin Interface** to receive rewards and error messages. The plugin calls it on the first of these that implements the interface:

1. the **Instigator**, the Controller you pass to **Apply Point Damage**, **Apply Radial Damage** or **Interact With Foliage**,
2. the **Pawn** of the Instigator, for example your Character,
3. the **Damage Causer**, the Actor you pass as Damage Causer or Causer, for example a weapon.

Only one of them receives each event, so a reward is never given twice. Implement the interface on whichever of them should handle the reward.

## Events
| Event | Parameters | Called when |
|---|---|---|
| **On Foliage Harvested** | **Foliage Actor**, **Rewards** | The foliage was harvested by damage or [interaction](/docfiles/guides/interaction-and-pickups). |
| **On Foliage Error Message** | **Foliage Error Type** | A hit did not harvest the foliage. |

Both events run on the **server**.

:::note
For a resource with **Harvest Without Actor** on, no Foliage Actor is spawned, so **Foliage Actor** is none. Use the **Rewards** instead. See [Interaction and Pickups](/docfiles/guides/interaction-and-pickups#pickups-without-a-foliage-actor).
:::

## Error types
| Error | Sent when |
|---|---|
| **Wrong Damage Type** | **Require Damage Type** is on and the hit used a damage type that is not in **Valid Damage Types**. See [Damage Types](/docfiles/guides/damage-types). |
| **Not Enough Damage** | **Require Damage Type** is on and the hit did less than **Damage Amount**. |
| **No Uses Left** | The Foliage Actor is already depleted. |

## If nothing receives the reward
If none of them implements the interface, the foliage is still harvested, and with **Enable Debugging** on you see:

```
Foliage successfully harvested, but Instigator or DamageCauser does not implement the FoliageInterface!
```
