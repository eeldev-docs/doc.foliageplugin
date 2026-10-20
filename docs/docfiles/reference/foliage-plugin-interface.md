---
sidebar_position: 4
description: The Foliage Plugin Interface that receives rewards and error messages when foliage is harvested.
---

# Foliage Plugin Interface

Implement the **Foliage Plugin Interface** to receive rewards and error messages. The plugin calls it on:

- the **Instigator**, the Controller you pass to **Apply Point Damage** or **Apply Radial Damage**, and
- the **Damage Causer**, the Actor you pass as Damage Causer, for example your Character or a weapon.

Implement it on whichever of them should handle the reward. If both implement it, both receive the events.

## Events
| Event | Parameters | Called when |
|---|---|---|
| **On Foliage Harvested** | **Foliage Actor**, **Rewards** | A Foliage Actor was harvested. |
| **On Foliage Error Message** | **Foliage Error Type** | A hit did not harvest the foliage. |

Both events run on the **server**.

## Error types
| Error | Sent when |
|---|---|
| **Wrong Damage Type** | **Require Damage Type** is on and the hit used a damage type that is not in **Valid Damage Types**. See [Damage Types](/docfiles/guides/damage-types). |
| **Not Enough Damage** | **Require Damage Type** is on and the hit did less than **Damage Amount**. |
| **No Uses Left** | The Foliage Actor is already depleted. |

## If nothing receives the reward
If neither the Instigator nor the Damage Causer implements the interface, the foliage is still harvested, and with **Enable Debugging** on you see:

```
Foliage successfully harvested, but Instigator or DamageCauser does not implement the FoliageInterface!
```
