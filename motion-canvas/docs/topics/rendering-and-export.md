# Rendering and export

You can export the animation as an image sequence or as a video (with optional audio). Both are triggered from the editor or via the project's export APIs.

Back to [index](index.md).

---

## Image sequence

Built-in exporter. Renders each frame to an image file (PNG, JPEG, or WebP). You can then import the sequence into a video editor or encode it yourself.

- **File type**: PNG (lossless), JPEG, or WebP. WebP support depends on the browser.
- **Quality**: 0–100 for JPEG/WebP; 100 is lossless where supported.
- **Group by scene**: If enabled, each scene goes into its own subfolder named after the scene.

Configure and start the export from the editor's Video Settings / export UI.

---

## Video (FFmpeg)

Uses [ffmpeg](ffmpeg.md): renders frames (and optionally audio) and encodes a single video file (e.g. MP4).

- **Setup**: Install `@motion-canvas/ffmpeg` and add `ffmpeg()` to `vite.config.ts` plugins. FFmpeg is typically installed automatically by the package.
- **Include audio**: If you've set up audio for the project, you can include it in the exported video.
- **Fast start**: Option for web playback so the video can start before the file is fully downloaded.

Configure and run from the editor after selecting the Video (FFmpeg) exporter in Video Settings.

---

## Audio

Audio can be attached to the project or scene for playback in the editor and for inclusion in video export. Set up audio in the project (e.g. via project settings or scene metadata); the exact API depends on your Motion Canvas version. Once set, the "Include audio" option in the video exporter will use it.

---

## See also

- [ffmpeg](ffmpeg.md)
- [editor](editor.md)
- [vite-plugin](vite-plugin.md)
