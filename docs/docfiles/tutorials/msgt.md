---
sidebar_position: 2
description: Integrate the Foliage Plugin with the Multiplayer Survival Game Template (MSGT).
---

# Multiplayer Survival Game Template (MSGT)

:::caution Outdated
This tutorial was made for an older version of the Multiplayer Survival Game Template and may need changes for newer versions.
:::

## Step 1: Create the Data Table
Create a Data Table with **FoliageData** as the row structure.

![Create the Data Table](../../../static/img/legacy/1_DT.gif)

## Step 2: Create the Foliage Actor
Create a Blueprint class with **FoliagePluginActor** as the parent class.

![Create the Foliage Actor](../../../static/img/legacy/2.gif)

## Step 3: Assign the Data Table in the Project Settings
Set the Data Table in **Project Settings → Game → Foliage Plugin**. In newer plugin versions, the Foliage Actor is set per resource with **Foliage Actor Class** in the Data Table.

![Project Settings](../../../static/img/legacy/3-1024x694.png)

## Step 4: Change the component class
Set **Component Class** to **FoliagePluginComponent** on your foliage types.

![Change the component class](../../../static/img/legacy/4-1024x645.png)

## Step 5: Add a tree resource

![Tree resource](../../../static/img/legacy/5-1024x747.png)

## Step 6: Implement the interface in SurvivalController
Add the **Foliage Plugin Interface** to the **SurvivalController** Blueprint.

![Add the interface](../../../static/img/legacy/6-1024x670.png)

Right-click in the SurvivalController Event Graph and add the interface event. This example adds the foliage rewards to the inventory:

![Add the rewards to the inventory](../../../static/img/legacy/7-1024x328.png)

## Step 7: Create the harvest event
In the SurvivalController Event Graph, create a new event as below:

![Harvest event](../../../static/img/legacy/11-1024x571.png)

## Step 8: Output the hit result from the interaction trace
Open the **C_Manager-HUD** component and change the **InteractiveTrace** function to output the **Hit Result**:

![InteractiveTrace](../../../static/img/legacy/8-1024x634.png)

In the **GetActionType** function (SurvivalController), add an input of type **Hit Result**:

![GetActionType input](../../../static/img/legacy/10-1024x590.png)

Connect the new Hit Result in the **InteractAction** function (SurvivalController):

![InteractAction](../../../static/img/legacy/9-1024x557.png)

## Step 9: Call the harvest event
Change **GetActionType** to call the event you created in Step 7, as shown in yellow:

![Call the harvest event](../../../static/img/legacy/12-1024x464.png)
