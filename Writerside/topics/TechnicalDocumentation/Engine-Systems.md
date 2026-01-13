# Engine Systems

This document outlines the specifics of deactivating unnecessary or redundant sections of the Unreal Engine codebase. 
Its purpose is to track and document all modifications that alter default UE behavior,
specifically those made for optimization, performance improvements, and engine feature debloating.

## Changes to Default Settings
> Important Read You need to be aware of these default changes as they affect projects directly

### Runtime changes

[Skeletal Meshes Optimized Config as Default](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/33fe7c638829b8120e8a02ecc639acda761df835)
![SkeletalMeshesOptimizedConfig.png](SkeletalMeshesOptimizedConfig.png)

[OverlapEvents disabled by default for Primitive Component](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/02d7c0ad0a7542b382a70dc3e37877d6ec052d76)
![OverlapEventsDisabled.png](OverlapEventsDisabled.png)

[Optimized Actor runtime, *Important READ](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/970cbb989c3712f13be1fa370b778e769e5d864c)
![OptimizedActorRuntime.png](OptimizedActorRuntime.png)

### Scalability Ini Settings
[Shadow Quality 4 is now in use for Mid Shadoe Setting · GapingPixel/UE5-PhysX-Vite@1718cd6](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/1718cd66e08a2b47222f895162e3be2b2c98ee6a)

### Disabled Plugins
[Disabled More Plugins, VR needs to be enabled · GapingPixel/UE5-PhysX-Vite@e9aebc2](https://github.com/GapingPixel/UnrealEngineVite-PhysX/commit/e9aebc2ef9f8acb7326a7e989f288ef68969342f)</br>
[Disabled More Default Plugins · GapingPixel/UE5-PhysX-Vite@6c5948b](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/6c5948bf12ea61f82784193ccaa5d43c4f574ae9)

### Misc Changes
Generate LightmapUVs has been disabled by default </br>
[Better defaults · GapingPixel/UE5-PhysX-Vite@acce6fb](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/acce6fbe432fe9fe5a2536f0979befd5dcd741d1#diff-b8a75e65f88cab66d24c562031b16504d663ea4af4a0c59135afa2c5fe69a513) </br>
[Safe Backports · GapingPixel/UE5-PhysX-Vite@fe7a6f4](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/fe7a6f4d7c54d8725d6308820d5b4fd546b9ff49) </br>
[Backport: AlwaysOpenAnimationAssetsInNewTab · GapingPixel/UE5-PhysX-Vite@8bdae91](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/8bdae919e6eae61a27ef8d09d38027592a473d8c) </br>
[Add config var to disable ShowNewPluginsPopup · GapingPixel/UE5-PhysX-Vite@9af0349](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/9af0349c1832b7094ceae7f47ba8ca5d261e0e69) </br>
[bDisableAllTutorialAlerts=True · GapingPixel/UE5-PhysX-Vite@d9fd593](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/d9fd593e11581fd93d0ff60b2933794f150b4780)

## Optional Debloat
From here and on, these refer to optional things that can be deactivated but that cannot be deactivated at the Fork-Release Branch for compatibility reasons.
### Vite Plugin Removal:
Removing the added plugins would improve compile times somewhat (houdini is the largest). Compile times on my Ryzen 9 9950x3d are: Full Repo 15min, No Vite Plugins 12min
![VitePlugins.png](VitePlugins.png)

## Engine Tick systems optimization
### SpeedTree Tick:
[UE5-PhysX-Vite/Engine/Source/Runtime/Engine/Private/LevelTick.cpp at 3e4a16aa89de4f4c37da300c945d6a14dc62edd7 · GapingPixel/UE5-PhysX-Vite](https://github.com/GapingPixel/UE5-PhysX-Vite/blob/3e4a16aa89de4f4c37da300c945d6a14dc62edd7/Engine/Source/Runtime/Engine/Private/LevelTick.cpp#L1709)
![SpeedTreeTick.png](SpeedTreeTick.png)

### Niagara Tick:
Niagara Tick can be deactivated by disabling the plugin at the project level.

## Default Settings Changes:

### SkeletalMeshComponent:
```c++
bAllowClothActors = true;
bPostEvaluatingAnimation = false;
bAllowAnimCurveEvaluation = true;
bDisablePostProcessBlueprint = false;

// By default enable overlaps when blending physics - user can disable if they are sure it's unnecessary
bUpdateOverlapsOnAnimationFinalize = true;

bPropagateCurvesToSlaves = false;

bSkipKinematicUpdateWhenInterpolating = false;
bSkipBoundsUpdateWhenInterpolating = false;
```
![SkeletalMeshDefault.png](SkeletalMeshDefault.png)

### Console Commands

```c++
GEngine->Exec(nullptr, TEXT("r.RayTracing.Culling.UseMinDrawDistance 1"));
```

From: [RT Culling Optimization: Use MinDrawDistance in ray tracing cullling · GapingPixel/UE5-PhysX-Vite@595f376](https://github.com/GapingPixel/UE5-PhysX-Vite/commit/595f376f6de0912606b05768739aa3d24ac4f61a)