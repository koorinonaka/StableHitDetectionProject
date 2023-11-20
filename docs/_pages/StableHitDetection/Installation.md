---
layout: page
title: Installation
permalink: /StableHitDetection/Installation
order: 0
---

# Installation

Place plugins downloaded from the marketplace in the `Plugins` directory.

## Modify collision settings
![AttackHit]({{ site.baseurl }}/assets/img/4f61e75e-36cd-d919-3de9-496ae2240824.png)

It is recommended that custom collision settings are added to the project.
In the sample project, `AttackHit` has been added. For the hit target, do not use `Block`, but set it up with `Overlap`.
For example, set `Overlap` for `BlockAll` `OverlapAll` `Pawn`, and `Ignore` for `CharacterMesh` `Trigger`.

## Add BP class for AnimNotify
What is done after hit detection depends on the project. Handle the event in the blueprint. [For more information on classes]({{ site.baseurl }}/StableHitDetection/HitDetectionNotify).

![BlueprintClass]({{ site.baseurl }}/assets/img/ccd580d6-add6-c0df-1db8-c8fe9c4638de.png)

Select any class from `SingleSocket`/`MultiSocket`/`HitComponent`. Here, select `HitComponent`.

### Set default properties
![Properties]({{ site.baseurl }}/assets/img/9d608de7-46c9-c413-b0ed-20401a798579.png)

It can be overridden for each AnimAsset, but it is useful to set the values defined in the BP class.

|MultiTraceAdapter|Select the type of tracing to be performed between each socket.|
|HitDirectionEffector|Select the type that determines the hit direction. This method is used because the `ImpactNormal` of the `HitResults` retrieved by the `MultiTraceAdapter` is incorrect for the hit direction.|
|TraceChannel|Configure the `TraceChannel` added above.|
|FrameRate|Unit of substeps in which the trace is performed. The numbers should not be too small as the number of processes increases.|
|DebugDrawTime|Number of seconds of debug drawing shown in the anim preview scene.|

### Implementing post-hit processing
![VerifyAnyHit]({{ site.baseurl }}/assets/img/bbe07310-f66c-d158-7b9a-ca7e15e69004.png)

`StableHitDetection` does not include post-hit processing (e.g. damage handling, motion playback). Implement according to the needs of your project.

## Create an AnimMontage
Note that StableHitDetection only supports `AnimMontage` and cannot embed notify into `AnimSequence`.

### PreviewScene settings
For the HitComponent to work correctly, the WeaponActor must also be spawned in the PreviewScene. Set up according to the [PreviewScene documentation]({{ site.baseurl }}/StableHitDetection/PreviewScene).

### Configure AnimNotify
Add it to the timeline in the same way as a normal notify.
