# @motion-canvas/vite-plugin

Vite integration: dev server, HMR, and build for Motion Canvas projects.

Back to [index](index.md).

---

## Role

- **Dev server**: Serves your project and the [ui](ui.md) editor. Run `npm start` (or `vite` with the plugin); open the browser for live preview.
- **HMR**: Code changes (scenes, project) hot-reload so you see updates without full refresh.
- **Build**: Bundles the project for production; can export image sequences or video via [ffmpeg](ffmpeg.md) when configured.
- **Project discovery**: Reads `project.ts` (or your project entry), discovers scenes, and wires them into the editor.

---

## Setup

In `vite.config.ts`:

- Import and add `motionCanvas()` to `plugins`.
- If you use [ffmpeg](ffmpeg.md) for video export, add `ffmpeg()` to `plugins` too.
- If you link a local `@motion-canvas/ui` from outside the project, set `server.fs.strict: false` so Vite can serve the UI.

New projects are scaffolded with this via [create](create.md).

---

## See also

- [getting-started](getting-started.md)
- [create](create.md)
- [ui](ui.md)
