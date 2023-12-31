---
layout: page
title: HitDetectionNotify
permalink: /StableHitDetection/HitDetectionNotify
order: 2
---

# HitDetectionNotify
This `AnimNotify` class uses `MultiTrace` implemented in the engine to detect hits and notify the user of the hit decision.
​
## Frame Rate
<ul id="c3eca504-f5d0-fd28-174f-b052e20a30ef">
<li><img src="{{ site.baseurl }}/assets/img/7d8f9d49-0733-72fa-5a8b-38489222ed88.gif" alt="substeps off"></li>
<li><img src="{{ site.baseurl }}/assets/img/2c7bab73-08e2-08df-d170-a40db4f4acf8.gif" alt="substeps on"></li>
</ul>
<style>
	ul#c3eca504-f5d0-fd28-174f-b052e20a30ef {
		display: flex;
		justify-content: center;
	}
	ul#c3eca504-f5d0-fd28-174f-b052e20a30ef li {
		list-style: none;
		padding: 1%;
	}
</style>
`StableHitDetection` supports operation at low frame rates.
This is handled by dividing the elapsed time into sub-steps instead of determining the timing of `NotifyTick`.
If a large frame time has elapsed, e.g. when the frame rate drops or a hitch occurs, it is processed according to the minimum time set here.
**The elapsed frame is fixed, so the tracing position and shape are stable, ensuring consistent hit decisions without fluctuations caused by delta time.**
The default value for `FrameRate` is 0.0167 (60 fps). It is related to the processing load, so change it according to the needs of your project. It can also be adjusted, for example, if you want a finer split for some animations.
If load is a concern, it can be switched off, but note that if there is severe position skipping, the process will also skip.
​
## TraceChannel
Can only be set in the BP class of AnimNotify. Default is `Visiblity`.
[Consider adding a trace channel]({{ site.baseurl }}/StableHitDetection/Installation#modify-collision-settings) to ensure that the character mesh is not hit.

## MultiTraceAdapter
Call `KismetSystemLibrary::XXXTraceMulti` between each socket location; supports `Line`/`Sphere`/`Box`/`Capsule`.
​
## HitDirectionEffector
![HitDirection]({{ site.baseurl }}/assets/img/44ebb3e1-cacc-de28-aabd-a11438630eea.png)

Set the hit direction to play the hit effect; do not use `Normal` or `ImpactNormal` in the `HitResult`.
​
### from Move Delta
For the position of the socket, the direction of movement compared to the previous frame is treated as the hit direction.
​
### from Actor Vector
Returns a normalised vector based on the `ActorForwardVector`, with the Forward, Right and Up components added. Used, for example, when the position of the socket does not move in the desired direction.

## Debug Draw Time
Time to display the trace in anim preview.
The following `ConsoleVariable` can be used to display it while playing.
```
StableHitDetection.DrawDebugTrace 2 // Displayed for 2s, valid for values greater than 0.f
```
​
## Function overrides
Implemented by overriding events. `StableHitDetection` is only responsible for hit detection; damage handling should be done by the project.
Note that `Receiver_NotifyBegin/Tick/End` is not called.
​
### BeginDetection
Notified at `NotifyBegin` timing.
​
### EndDetection
Notified at `NotifyEnd` timing.
​
### CanHitComponent
Determines whether `HitSocketComponent` is valid for any of the child components of the animation mesh.
​
### VerifyAnyHit
Notified when a hit is made by `NotifyTick`.

![VerifyAnyHit]({{ site.baseurl }}/assets/img/bbe07310-f66c-d158-7b9a-ca7e15e69004.png)

Example of debugging the drawing of `HitResults` from the impact point to the hit direction.

## AnimNS_HitDetection_SingleSocket
![SingleSocket]({{ site.baseurl }}/assets/img/f0a01716-1596-2b1a-3275-75624d313d64.png)

Trace frame positions before and after a single socket.

|MultiTraceAdapter|Traces between sockets.|
|Socket.Target|Specifying the socket position.|
|Socket.RelativeTransform|Adjustment values based on socket transform.|

## AnimNS_HitDetection_MultiSocket
![MultiSocket]({{ site.baseurl }}/assets/img/bdfefc70-03db-018a-989c-e3dc2a3d9f16.png)

Trace frame positions before and after a multi socket.

|Trace (Other at Current Frame)|Traces between different sockets in the same frame. |
|Trace (Same at Last Frame)|Traces between the same socket on the different frames. Used to bridge gaps due to time differences.|
|Trace (Other at Last Frame)|Traces between different sockets on different frames. Used to fill finer gaps.|

## AnimNS_HitDetection_HitComponent
`HitSocketComponent`, a child component of the attached actor, is traced as a socket location.
Although it is easier to use a socket, **this method is recommended as it has many advantages, such as easier adjustment of the decision position and the ability to change weapons**.
Parameters are the same as for `MultiSocket`. For previews, see **[PreviewScene]({{ site.baseurl }}/StableHitDetection/PreviewScene)** settings.

### When attaching multiple actors
![MultipleAttachment]({{ site.baseurl }}/assets/img/c64101f3-388d-83a1-613b-7c2c5c82d905.png)

HitComponent recursively searches for all `HitSocketComponents` attached to the `CharacterMesh`.
When multiple actors are attached, e.g. two-faced, this can be inconvenient as all component location are connected.

![SplitNotify]({{ site.baseurl }}/assets/img/321055cc-e65b-c4d4-bdd9-6aec7de79093.png)

In this case, specify the attached socket names in `AllowedTargets` and split the notify.
