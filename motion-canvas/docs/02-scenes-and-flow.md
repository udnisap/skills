# 02 – Scenes and flow

**When to use:** You need to define a 2D scene, pause until a named moment (e.g. for voiceover/editing), run animations in parallel or sequence, start/cancel/join loops, or end a scene.

---

## Import map

- `makeScene2D` from `@motion-canvas/2d`
- `all`, `chain`, `delay`, `loop`, `waitFor`, `waitUntil` from `@motion-canvas/core/lib/flow` or `@motion-canvas/core`
- `cancel`, `join` from `@motion-canvas/core/lib/threading` or `@motion-canvas/core`
- `finishScene`, `useScene` from `@motion-canvas/core`

---

## Concepts

- **makeScene2D(function* (view) { ... })**: scene is a generator; `yield` or `yield*` waits for a tween or sub-generator.
- **waitUntil('name')**: pauses until that name is reached (used with editor/audio).
- **all(...)**: run several tweens/generators in parallel; often `yield* all(a.opacity(1, 1), b.x(100, 1))`.
- **chain(...)**: run in sequence; e.g. `chain(a.end(1, 1), delay(0.5, b.opacity(1, 0.5)))`.
- **delay(t, genOrTween)**: wait `t` then run.
- **loop(n, fn)** or **loop(Infinity, fn)**: repeat; returns a task. Use **cancel(task)** to stop, **join(task)** to wait for it to finish.
- **finishScene()**: mark scene as finished (e.g. before a final transition). **useScene().enterCanTransitionOut()** allows transition out.

---

## Snippets

**Basic scene and waitUntil**

```ts
import {makeScene2D} from '@motion-canvas/2d';
import {waitUntil} from '@motion-canvas/core/lib/flow';

export default makeScene2D(function* (view) {
  view.add(<Txt text={'Hello'} />);
  yield* waitUntil('next');
});
```

**Parallel animations**

```ts
yield* all(
  circle().opacity(1, 1),
  rect().x(200, 1),
  line().end(1, 1),
);
```

**Chain (sequence)**

```ts
yield* chain(
  line().end(1, 1),
  delay(0.2, target().opacity(1, 0.2)),
  line().start(1, 1),
);
```

**Background loop and cancel**

```ts
const task = yield loop(Infinity, function* () {
  yield* circle().scale(1, 1).to(1.5, 1);
});
yield* waitUntil('stop');
cancel(task);
yield* join(task); // wait for loop to finish
```

**End scene and allow transition out**

```ts
yield* waitUntil('end');
useScene().enterCanTransitionOut();
yield* join(task2);
```

**finishScene before final transition**

```ts
finishScene();
yield* all(node.opacity(0, 0.6), view.fill(null, 0.6));
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/scenes/signals.tsx` (waitUntil, loop, cancel, join, all, chain, delay)
- `repos/examples/examples/motion-canvas/src/scenes/layouts.tsx`
- `repos/examples/examples/motion-canvas/src/scenes/interface.tsx`
- `repos/examples/examples/smooth-parallax/src/scenes/parallax.tsx`
- `repos/examples/examples/asset-code/src/scenes/intro.tsx`

---

## See also

- [01-setup-and-project](01-setup-and-project.md) – project and scenes
- [03-signals-and-refs](03-signals-and-refs.md) – createRef, makeRef for nodes you animate
- [08-transitions-and-easing](08-transitions-and-easing.md) – slideTransition, zoomInTransition
- [agent-quickref](agent-quickref.md) – "Wait for a named moment", "Run in parallel", "Run a loop"
