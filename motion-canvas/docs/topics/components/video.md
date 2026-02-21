# Video

Plays video in the scene. Supports playback control and synchronization with the animation timeline.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **src**: Video source (URL or asset path).
- **width**, **height**: Display size.
- **play**: Whether to start playing (signal/value).
- **currentTime**: Playback position (can be synced to scene time).
- Standard Node props: **position**, **scale**, **opacity**, etc.

---

## Usage

Add a video node; control playback and currentTime to sync with narration or scene time. Useful for picture-in-picture, overlays, or when the animation drives the video timeline.

---

## See also

- [Img](img.md)
- [rendering-and-export](../rendering-and-export.md) (audio/video export)
