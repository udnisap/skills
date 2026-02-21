# 03 – Signals and refs

**When to use:** You need reactive state that drives property values, derived values from other signals, or references to nodes so you can animate them later.

---

## Import map

- `createSignal`, `createComputed` from `@motion-canvas/core/lib/signals` or `@motion-canvas/core`
- `createRef`, `makeRef`, `makeRefs`, `createRefMap`, `createRefArray` from `@motion-canvas/core/lib/utils` or `@motion-canvas/core`

---

## Concepts

- **createSignal(initial)**: returns a getter/setter. In JSX use `width={() => size()}` or `width={size}`; to tween: `size(0, 1).to(100, 1)`.
- **createComputed(fn)**: derived from other signals; updates when dependencies change.
- **createRef\<T\>()**: one ref. In JSX: `ref={ref}`; in logic: `ref().opacity(1, 1)`.
- **makeRef(arr, i)**: push into an array in `map`: `ref={makeRef(circles, i)}` so `circles[i]` is the node.
- **makeRefs**: for components that expose multiple refs (e.g. `{ value, text }`).
- **createRefMap\<T\>()**: named refs; `ref={map.foo}` then `map.foo()`.
- **createRefArray\<T\>()**: `ref={refArray}` on each of several elements; access `refArray[0]()`, `refArray.at(-1)()`.

---

## Snippets

**Signal and reactive property**

```ts
const size = createSignal(1);
view.add(<Rect width={() => 100 * size()} height={100} fill={'#333'} />);
yield* size(2, 1); // tween to 2 over 1s
```

**Computed**

```ts
const radius = createSignal(3);
const area = createComputed(() => Math.PI * radius() * radius());
// use area() in JSX or tweens
```

**createRef**

```ts
const rect = createRef<Rect>();
view.add(<Rect ref={rect} width={200} height={100} />);
yield* rect().opacity(1, 0.5);
```

**makeRef in map**

```ts
const circles: Circle[] = [];
view.add(
  positions.map(([x, y], i) => (
    <Circle ref={makeRef(circles, i)} x={x} y={y} width={20} height={20} fill={'#242424'} />
  )),
);
yield circles[0].fill('#68ABDF').opacity(1, 0.1);
```

**createRefMap**

```ts
const labels = createRefMap<Txt>();
view.add(
  <>
    <Txt ref={labels.title} />
    <Txt ref={labels.subtitle} />
  </>,
);
yield labels.title().text('Hello', 1);
```

**createRefArray**

```ts
const panels = createRefArray<Rect>();
view.add(
  <>
    <Rect ref={panels} />
    <Rect ref={panels} />
  </>,
);
yield panels[0]().opacity(1, 0.3);
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/scenes/signals.tsx` (makeRef, createRef)
- `repos/examples/examples/motion-canvas/src/scenes/layouts.tsx` (createSignal, map for grow)
- `repos/examples/examples/asset-code/src/scenes/intro.tsx` (createComputed, createSignal, createRef)
- `repos/examples/examples/smooth-parallax/src/scenes/parallax.tsx`
- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (createRefMap, createRefArray)

---

## See also

- [02-scenes-and-flow](02-scenes-and-flow.md) – yield, waitUntil, all
- [04-2d-components](04-2d-components.md) – Node, Rect, Circle, etc.
- [05-layouts](05-layouts.md) – grow with map
- [agent-quickref](agent-quickref.md) – "reactive state", "reference to a node", "list of refs"
