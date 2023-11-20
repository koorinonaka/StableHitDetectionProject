<table>
  <tr>
    <td valign="top"><img src="https://github.com/koorinonaka/StableHitDetectionProject/assets/39552085/0f3e2f1a-9c87-46b7-925e-cc4931056657/7d8f9d49-0733-72fa-5a8b-38489222ed88.gif"/></td>
    <td valign="top"><img src="https://github.com/koorinonaka/StableHitDetectionProject/assets/39552085/fa9d3414-a581-4b33-b2c9-2df8148cff47/2c7bab73-08e2-08df-d170-a40db4f4acf8.gif"/></td>
  </tr>
</table>

`StableHitDetection` is designed to completely prevent missed hits.
The combination of AnimNotify and MultiTrace provides an optimal hit detection solution.

## Features
- **Hits missed due to low FPS or hitching are completely preventable**.
  - The position of the hit box is fixed and is not affected by delta time.
- MultiTrace `Line`/`Sphere`/`Box`/`Capsule` hit detection in the AnimNotify section.
  - Generate a mesh of hit box between sockets or components.
- Actor spawning and attachment in anim preview scenes (extra).

## Installation
1. Clone this repository.
2. Place plugins downloaded from the marketplace in the `Plugins` directory.

## Documents
https://koorinonaka.github.io/StableHitDetectionProject/
