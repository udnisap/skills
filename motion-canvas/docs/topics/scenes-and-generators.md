# Scenes and generators

How scenes are defined, how the view hierarchy works, and how the generator controls animation flow.

Back to [index](index.md).

---

## makeScene2D and view

- **makeScene2D**: Takes a generator function and creates a 2D scene. The generator receives **view**, the root of the scene's visual tree.
- **view**: Like a root DOM node. You add all visible nodes to `view` (or to other nodes you add). Use `view.add(<Node />)` to add children.
- **Nodes**: Visual elements ([Circle](components/shapes.md), [Rect](components/shapes.md), [Txt](components/txt.md), [Layout](components/layout.md), etc.). They can be nested; use `Node.add`, `Node.insert`, `Node.remove` to change the hierarchy.

Scenes are registered in the project via [makeProject](core.md) in `src/project.ts` (e.g. `scenes: [example]`).

---

## Generator function and yield

The function you pass to `makeScene2D` is a **generator** (`function*`). It can pause and resume. Animation advances when you **yield**.

- **yield**: Advances to the next frame. Any property changes before it are shown in that frame.
- **yield* someGenerator()**: Runs another generator (usually a tween) and waits until it finishes. Example: `yield* myCircle().fill('#e6a700', 1)` animates fill over 1 second.
- **yield* all(...generators)**: Runs several generators **at the same time**; the scene continues when all are done. Use for parallel animations (e.g. move and change color together).

Other flow helpers (e.g. `chain`, `sequence`, `delay`) let you run generators one after another or with delays. See [signals-and-animation](signals-and-animation.md).

---

## Typical pattern

1. Create refs with `createRef<NodeType>()`.
2. Add nodes to `view` with `view.add(<Node ref={ref} ... />)`.
3. Animate by yielding tweens: `yield* ref().position.x(100, 1)` or `yield* all(...)`.

Back to [index](index.md) · [signals-and-animation](signals-and-animation.md) · [getting-started](getting-started.md).
