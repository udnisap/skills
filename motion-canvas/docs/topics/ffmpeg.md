# @motion-canvas/ffmpeg

Video export using FFmpeg. Renders the animation to an image sequence or stream and encodes to a video file (e.g. MP4), with optional audio.

Back to [index](index.md).

---

## Role

- **Video export**: Encodes the project's frames (and optional audio) into a single video file via FFmpeg.
- **Integration**: Vite plugin; add `ffmpeg()` next to `motionCanvas()` in `vite.config.ts`. The editor then shows a video export option alongside image-sequence export.

---

## Setup

1. Install: `npm install @motion-canvas/ffmpeg`
2. In `vite.config.ts`: `import ffmpeg from '@motion-canvas/ffmpeg'` and add `ffmpeg()` to the `plugins` array.

FFmpeg must be installed on the system (or the package may bundle or download it depending on version). Export is triggered from the [ui](ui.md) editor or programmatically via the project's export APIs.

---

## See also

- [rendering-and-export](rendering-and-export.md)
- [vite-plugin](vite-plugin.md)
- [ui](ui.md)
