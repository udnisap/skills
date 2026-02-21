# Signals and animation

Signals are animatable reactive values. Tweening changes them over time; flow generators control when things run.

Back to [index](index.md).

---

## Signals

Node properties (position, fill, opacity, etc.) are **signals**. You can:

- **Read**: `signal()` (no arguments).
- **Set**: `signal(value)` (instant).
- **Tween**: `yield* signal(targetValue, duration)` — animates from current value to target over the given time.

Signals are lazy and cached; dependents update when the signal changes. Compound signals (e.g. **position** as x/y) expose sub-signals: `node().position.x(100, 1)` tweens only x.

---

## Tweening

Example: `yield* node().position.x(100, 1)`:

1. **node()**: Gets the node from a ref.
2. **.position**: The position signal (Vector2).
3. **.x**: The x component (number).
4. **(100, 1)**: Target value 100, duration 1 second.
5. **yield***: Pauses the scene generator until the tween finishes.

You can chain: `node().position.x(0, 0.5).to(100, 1)` — first 0.5s to 0, then 1s to 100.

---

## all() and waitFor()

- **all(...generators)**: Run several animations in parallel. `yield* all(...)` waits until all are done. Example: move and change color at the same time.
- **waitFor(seconds)**: Pause for a number of seconds. `yield* waitFor(1)` waits 1 second.
- **waitUntil('eventName')**: Pause until a named time event (e.g. one you set in the editor timeline or in code). Useful for syncing with audio or cues.

---

## Flow generators (conceptual)

Besides `all`, you may have **chain**, **sequence**, **delay**, **any**: they combine or order generators (run in sequence, run first to finish, etc.). Use them to structure multi-step animations without blocking the whole scene.

---

## See also

- [scenes-and-generators](scenes-and-generators.md)
- [core](core.md)
- [getting-started](getting-started.md)
