<iframe width="560" height="315" src="https://www.youtube.com/embed/WcD6sRx8nAM?si=i06AS-8zJXV152JB" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture; web-share" allowfullscreen></iframe>

`StableHitDetection` is designed to completely prevent missed hits.<br />
The combination of AnimNotify and MultiTrace provides an optimal hit detection solution.

## Features
- **Hits missed due to low FPS or hitching are completely preventable**.
  - The transform of the hit box is fixed and is not affected by delta time.
- MultiTrace `Line`/`Sphere`/`Box`/`Capsule` hit detection in the AnimNotify section.
  - Generate a mesh of hit box between sockets or components.
- Actor spawning and attachment in anim preview scenes (extra).

## Installation
1. Clone this repository.
2. Place plugins downloaded from the marketplace in the `Plugins` directory.

## Documents
https://koorinonaka.github.io/StableHitDetectionProject/
