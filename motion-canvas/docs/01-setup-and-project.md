# 01 – Setup and project

**When to use:** You need to define a Motion Canvas project, register scenes, wire Vite, and attach audio for voiceover or music.

---

## Import map

- `makeProject` from `@motion-canvas/core`
- Scene modules: `from './scenes/foo?scene'`
- Vite: `motionCanvas` from `@motion-canvas/vite-plugin`, `ffmpeg` from `@motion-canvas/ffmpeg`

---

## Concepts

- **makeProject** takes `scenes` (array of scene modules) and optional `audio` (URL or imported audio file).
- Scenes are imported with the **`?scene`** query so the Motion Canvas plugin can register them.
- **Vite**: use `motionCanvas()`; add `ffmpeg()` when you need to export video.
- `experimentalFeatures: true` is used in some examples (e.g. asset-code).

---

## Snippets

**Project with scenes and audio**

```ts
import {makeProject} from '@motion-canvas/core';
import scene1 from './scenes/scene1?scene';
import scene2 from './scenes/scene2?scene';
import audio from './audio/voice.mp3';

export default makeProject({
  scenes: [scene1, scene2],
  audio,
});
```

**Vite config with Motion Canvas and ffmpeg (for export)**

```ts
import {defineConfig} from 'vite';
import motionCanvas from '@motion-canvas/vite-plugin';
import ffmpeg from '@motion-canvas/ffmpeg';

export default defineConfig({
  plugins: [motionCanvas(), ffmpeg()],
});
```

**Vite config without ffmpeg (preview only)**

```ts
import motionCanvas from '@motion-canvas/vite-plugin';
import {defineConfig} from 'vite';

export default defineConfig({
  plugins: [motionCanvas()],
});
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/project.ts`
- `repos/examples/examples/asset-code/src/project.ts`
- `repos/examples/examples/smooth-parallax/src/project.ts`
- `repos/examples/examples/motion-canvas/vite.config.ts`
- `repos/examples/examples/asset-code/vite.config.ts`

---

## See also

- [02-scenes-and-flow](02-scenes-and-flow.md) – define a scene
- [agent-quickref](agent-quickref.md) – "Set up a project with scenes and audio"
