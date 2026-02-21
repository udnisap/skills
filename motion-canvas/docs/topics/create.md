# @motion-canvas/create

Project scaffolding: creates a new Motion Canvas project with the right dependencies and config.

Back to [index](index.md).

---

## Usage

```bash
npm init @motion-canvas@latest
```

Prompts:

- **Project name**: Folder and package name.
- **Language**: TypeScript (recommended) or JavaScript.
- **Exporters**: Image sequence (built-in), Video/FFmpeg (adds [ffmpeg](ffmpeg.md)).

Then:

```bash
cd <project-name>
npm install
npm start
```

Opens the [vite-plugin](vite-plugin.md) dev server with the [ui](ui.md) editor.

---

## What it sets up

- **Dependencies**: [core](core.md), [2d](2d.md), [ui](ui.md), [vite-plugin](vite-plugin.md); optionally [ffmpeg](ffmpeg.md).
- **Config**: `vite.config.ts` with `motionCanvas()` (and `ffmpeg()` if chosen).
- **Entry**: `project.ts` (or `.js`) with `makeProject` and a default scene.
- **Scenes**: A sample scene file (e.g. `src/scenes/example.tsx`) to edit.

---

## See also

- [getting-started](getting-started.md)
- [vite-plugin](vite-plugin.md)
- [core](core.md)
