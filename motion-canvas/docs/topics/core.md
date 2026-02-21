# @motion-canvas/core

Animation engine, signals, scenes, project, and plugin API. The base package everything else builds on.

Back to [index](index.md).

---

## Role

- **Project**: Central hub for scenes, settings, metadata. Use `makeProject({ scenes: [...] })` to define the project.
- **Scene**: One animation unit (name, playback, time range). Scenes are generator-based; 2D scenes use [makeScene2D](2d.md) from `@motion-canvas/2d`.
- **Signals**: Reactive, animatable properties (e.g. `SimpleSignal`, `Vector2Signal`, `ColorSignal`). Nodes expose signals; you tween them in generator functions.
- **Flow**: `ThreadGenerator` = generator that controls animation. Use `yield*` to run tweens; `all(...)` to run generators in parallel; `waitFor(seconds)` to pause.

---

## Main exports (conceptual)

| Export | Purpose |
|--------|---------|
| `makeProject` | Create project config (scenes, plugins). |
| `createRef` | Get a reference to a node so you can animate it. |
| `useScene` | Access current scene inside a component. |
| `all` | Run several generators concurrently. |
| `waitFor` | Pause for a duration. |
| `Signal` / `SimpleSignal` / `Vector2Signal` / `ColorSignal` | Signal types for animatable values. |

`makeScene2D` lives in [2d](2d.md); it uses core's generator and scene logic.

---

## See also

- [scenes-and-generators](scenes-and-generators.md)
- [signals-and-animation](signals-and-animation.md)
- [2d](2d.md)
