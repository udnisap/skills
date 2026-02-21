# Getting started

Install a new project, run the editor, and add a first animation. No external links—everything you need is below or in linked docs.

Back to [index](index.md).

---

## Prerequisites

- **Node.js** 16 or greater. Check with `node -v`.

---

## Create a new project

1. Scaffold:
   ```bash
   npm init @motion-canvas@latest
   ```
   If that fails, try: `npm exec @motion-canvas/create@latest`.

2. Prompts: project name, language (TypeScript recommended), exporters (image sequence and/or video/FFmpeg).

3. Go to the project folder and install:
   ```bash
   cd <project-path>
   npm install
   ```

4. Start the editor:
   ```bash
   npm start
   ```
   Open the URL shown in the terminal (the dev server address). You'll use this to preview animations.

---

## Project structure (typical)

- **src/project.ts** (or .js): Exports `makeProject({ scenes: [ ... ] })`. Entry point.
- **src/scenes/*.tsx**: Scene files. Each exports a default scene (from `makeScene2D`).
- **vite.config.ts**: Uses `motionCanvas()` (and optionally `ffmpeg()`) in `plugins`.

Scenes are imported in the project file with the `?scene` query (e.g. `import example from './scenes/example?scene'`).

---

## First animation

Edit **src/scenes/example.tsx** (or the default scene file). Example: a circle that moves and changes color.

```tsx
import {makeScene2D, Circle} from '@motion-canvas/2d';
import {all, createRef} from '@motion-canvas/core';

export default makeScene2D(function* (view) {
  const myCircle = createRef<Circle>();

  view.add(
    <Circle
      ref={myCircle}
      x={-300}
      width={140}
      height={140}
      fill="#e13238"
    />,
  );

  yield* all(
    myCircle().position.x(300, 1).to(-300, 1),
    myCircle().fill('#e6a700', 1).to('#e13238', 1),
  );
});
```

- **makeScene2D**: Defines a 2D scene; the generator receives `view` and adds nodes to it.
- **createRef**: Gets a reference so you can animate that node.
- **view.add(...)**: Adds the Circle to the scene.
- **yield* all(...)**: Runs several tweens in parallel. Here: move x and animate fill.

Save the file; the editor hot-reloads. Press play to see the animation.

---

## Next steps

- [scenes-and-generators](scenes-and-generators.md) — scene structure and generator flow.
- [signals-and-animation](signals-and-animation.md) — signals, tweening, and `all` / sequencing.
- [2d-components](2d-components.md) — list of components (Circle, Rect, Txt, Code, etc.).
- [create](create.md) — what the scaffold sets up.
