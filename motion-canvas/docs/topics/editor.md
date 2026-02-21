# Editor

The Motion Canvas editor: timeline, viewport, inspector, and scene graph. Shown when you run the dev server.

Back to [index](index.md).

---

## What the editor is

The editor is the web UI you get when you run `npm start` (via [vite-plugin](vite-plugin.md)). It uses [ui](ui.md) and shows:

- **Viewport**: The canvas where the current frame is rendered. You can zoom and pan. This is the same renderer as in [2d](2d.md).
- **Timeline**: Playback (play/pause), current time, and the range of the scene. You scrub time to see any frame. Time events (for [waitUntil](signals-and-animation.md)) can be adjusted here.
- **Inspector**: When you select a node (in the viewport or scene graph), the inspector shows its properties (signals). You can edit values for the current time to tweak the look.
- **Scene graph**: Tree of all nodes in the current scene. Select a node to inspect or keyframe it.

---

## Workflow

1. Edit scene code (e.g. `src/scenes/example.tsx`). Changes hot-reload.
2. Use the viewport to see the result and the timeline to play or scrub.
3. Use the inspector to tweak properties at the current time if needed.
4. Export from the editor (image sequence or video) when ready; see [rendering-and-export](rendering-and-export.md).

---

## See also

- [ui](ui.md)
- [vite-plugin](vite-plugin.md)
- [getting-started](getting-started.md)
