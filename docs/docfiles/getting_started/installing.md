---
sidebar_position: 1
description: How to install and enable the Foliage Plugin in an Unreal Engine project.
---

# Installing the Plugin

## Install from Fab
1. Add the plugin to your library on [Fab](https://www.fab.com/listings/de03e7a7-aefe-4290-8fb3-8cde3a34fbf9).
2. In the Epic Games Launcher, open **Unreal Engine → Library → Fab Library**, find **Foliage Plugin** and click **Install to Engine**.
3. Open your project, go to **Edit → Plugins**, search for **Foliage Plugin** and enable it.
4. Restart the editor when prompted.

The plugin settings are now available in **Project Settings → Game → Foliage Plugin**.

## Using the plugin from C++
If you reference the plugin's classes from C++, for example to subclass the Foliage Actor or the Foliage Manager, add the `FoliagePlugin` module to your module's `.Build.cs`:

```csharp
PublicDependencyModuleNames.AddRange(new string[] { "FoliagePlugin" });
```

## Next step
[Set up your foliage and Data Table](/docfiles/getting_started/setup).
