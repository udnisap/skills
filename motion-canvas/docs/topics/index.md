# Motion Canvas

Motion Canvas is a specialized tool for creating programmatic vector animations, designed for informative animations synchronized with voice-overs. It has two parts: a TypeScript library that uses generators to program animations, and an editor that provides a real-time preview and lets you edit animation aspects.

---

## Plugins (packages)

| Package | Description |
|--------|-------------|
| [@motion-canvas/core](core.md) | Animation engine, signals, scenes, project, plugin API |
| [@motion-canvas/2d](2d.md) | 2D renderer, shapes, text, layout, paths |
| [@motion-canvas/ui](ui.md) | Editor UI: timeline, viewport, inspector, scene graph |
| [@motion-canvas/vite-plugin](vite-plugin.md) | Vite integration, dev server, HMR, build |
| [@motion-canvas/player](player.md) | Playback component for in-browser display |
| [@motion-canvas/create](create.md) | Project scaffolding (`npm init @motion-canvas@latest`) |
| [@motion-canvas/ffmpeg](ffmpeg.md) | Video export via FFmpeg |

---

## Main components

| Component | Description |
|-----------|-------------|
| [LaTeX](components/latex.md) | Equations and math (LaTeX node) |
| [Code](components/code.md) | Syntax-highlighted code (Code node, Lezer) |
| [Txt](components/txt.md) | Text display and animation (Txt node) |
| [Shapes](components/shapes.md) | Circle, Rect, Polygon (basic shapes) |
| [Line & Ray](components/line-ray.md) | Lines and rays (Line, Ray nodes) |
| [Layout](components/layout.md) | Flexbox layout (Layout node) |
| [Img](components/img.md) | Images (Img node) |
| [Video](components/video.md) | Video playback (Video node) |
| [SVG](components/svg.md) | SVG content (SVG node) |

---

## Feature guides

| Topic | Doc |
|-------|-----|
| Getting started | [getting-started](getting-started.md) |
| Scenes and generators | [scenes-and-generators](scenes-and-generators.md) |
| Signals and animation | [signals-and-animation](signals-and-animation.md) |
| 2D components overview | [2d-components](2d-components.md) |
| Editor | [editor](editor.md) |
| Rendering and export | [rendering-and-export](rendering-and-export.md) |
| Plugin authoring | [plugin-authoring](plugin-authoring.md) |
| Examples | [examples](examples.md) |
