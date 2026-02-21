# @motion-canvas/ui

Editor UI: timeline, viewport, inspector, scene graph. Used by the Vite-based dev server to preview and edit animations.

Back to [index](index.md).

---

## Role

- **Timeline**: Playback, time range, scrubbing. Controls what the [core](core.md) playback manager does.
- **Viewport**: Renders the current frame (canvas). Zoom, pan, overlays.
- **Inspector**: Edit selected node properties (signals) in the UI.
- **Scene graph**: Tree of nodes; select nodes to inspect or edit.
- **Layout**: Resizable panels (viewport, timeline, console, inspector, scene graph).

The editor is served by [vite-plugin](vite-plugin.md); you run `npm start` and open the dev URL. The UI talks to the project and renderer from [core](core.md) and [2d](2d.md).

---

## When you use it

You use it implicitly when you run the Motion Canvas dev server. You don't import `@motion-canvas/ui` in your scene code; the vite plugin loads the editor. For embedding playback without the editor, use [player](player.md).

---

## See also

- [editor](editor.md) (timeline, viewport, workflow)
- [vite-plugin](vite-plugin.md)
- [player](player.md)
