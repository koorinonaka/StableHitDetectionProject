---
layout: page
title: PreviewScene
permalink: /StableHitDetection/PreviewScene
order: 1
---

# PreviewScene
![PreviewScene]({{ site.baseurl }}/assets/img/f5a12c37-6dcd-6ab9-7c80-52509e13aae3.png)

When opening an animation asset like `AnimSequence`, the weapon can be spawned in the animation preview window.
**Unlike preview meshes, which are added to the skeleton, different actors can be attached to each animation.**
If the `HitDetection_HitComponent` notify is used, this setting must be enabled for correct previewing.

## Creating an actor class to attach to
![BP_Weapon]({{ site.baseurl }}/assets/img/e25df79a-b016-7081-0a80-dd8e7a7a2c55.png)

Create `BP_Weapon`. Here, it is created by inheriting from `StaticMeshActor`, but the inheritance class can be chosen arbitrarily.
If you already have a weapon actor to use in the game, there is no need to create a new one; skip to the HitSocketComponent section.

![Movable]({{ site.baseurl }}/assets/img/043328a1-e27d-0e57-4fdc-a9b2d9b92456.png)

For `StaticMeshActor`, set `Transform.Movable` to `Movable`.
Note that the default for StaticMesh Movable is `Static` and cannot be attached as is if the destination is `Movable`.

### Add HitSocketComponent
![HitSocketComponent]({{ site.baseurl }}/assets/img/80c0496a-7408-75f4-d84f-e5930625d225.png)

Add a hit socket to the weapon.
The number of trace points increases with each additional socket, so be careful not to increase it excessively.

### Set weapon mesh to NoCollision
![No Collision]({{ site.baseurl }}/assets/img/c6ee0e06-c12a-d0af-ccf1-4c8a996cdba0.png)

Preventing hit detection on self-collision.

## Set MetaData in the AnimAsset
![AnimPreviewMetaData]({{ site.baseurl }}/assets/img/7b0bbdbd-3135-46f0-1c0c-8ccc792a2f98.png)

Open the AnimAsset and add `MetaData` to the asset details.
Select `AnimPreview` and set the attachment information to `AttachActors`.

|ActorClass|Spawning actor class.|
|SocketName|Name of socket or bone to be attached.|
|RelativeTransform|Adjustment of transformations.|

### When AnimAsset is opened for the first time, attachments are not reflected.
This is reflected when another AnimAsset is reopened.
This seems to be a bug in the engine; it should be fixed in the future.
