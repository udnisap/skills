# Plugin authoring

Custom plugins extend Motion Canvas: they can change project settings, add exporters, and hook into Project, Player, Presenter, and Renderer. Editor UI extensions are experimental.

Back to [index](index.md).

---

## Creating a plugin

Use **makePlugin** (from [core](core.md)) and pass an object that matches the **Plugin** interface. Add it to the **plugins** array in **makeProject**:

```ts
import { makeProject, makePlugin } from '@motion-canvas/core';

export default makeProject({
  scenes: [ ... ],
  plugins: [
    makePlugin({
      name: 'my-plugin',
      // optional hooks
    }),
  ],
});
```

Plugins can also be specified as string module paths for dynamic import (useful so editor-only code is not in production builds).

---

## Plugin interface (conceptual)

- **name**: Unique string id for the plugin.
- **settings?(settings)**: Modify project settings before the project is created. Return updated settings or mutate and return void.
- **project?(project)**: Called with the Project instance after it's created.
- **player?(player)**: Called with the Player instance.
- **presenter?(presenter)**: Called with the Presenter instance.
- **renderer?(renderer)**: Called with the Renderer instance.
- **exporters?(project)**: Return an array of custom Exporter classes. Used to add new export formats (e.g. the FFmpeg plugin adds a video exporter).

---

## What plugins can do

- **Change project settings** in `settings()`.
- **Add custom exporters** via `exporters()` so new export options appear in the editor.
- **Use core instances** in the lifecycle hooks (project, player, presenter, renderer) to read or drive the animation.
- **Extend the editor** (experimental): editor plugins can add tabs, overlays, inspectors, and shortcuts via the EditorPlugin interface.

---

## See also

- [core](core.md)
- [ffmpeg](ffmpeg.md) (example of a plugin that adds an exporter)
- [rendering-and-export](rendering-and-export.md)
