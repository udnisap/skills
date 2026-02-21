# 15 – Advanced patterns

**When to use:** You need `createRefMap`/`createRefArray`, `Ray` between nodes, `CubicBezier` between two nodes, `tween` with a custom function, `modify` for coordinate transforms, or `reparent` to move a node to another parent.

---

## Import map

- `createRefMap`, `createRefArray` from `@motion-canvas/core/lib/utils`
- `Ray`, `CubicBezier` from `@motion-canvas/2d` or `@motion-canvas/2d/lib/components`
- `tween`, `modify` from `@motion-canvas/core`
- `Vector2` from `@motion-canvas/core/lib/types`
- `reparent` is a method on `Node`: `node.reparent(newParent)`

---

## Concepts

- **createRefMap\<T\>()**: named refs; `ref={map.name}` then `map.name()`. Good for many known children (panels, labels).
- **createRefArray\<T\>()**: `ref={arr}` on each of N elements; `arr[0]()`, `arr.at(-1)()`. Grows as you add.
- **Ray**: `from`, `to` (e.g. `a.right`, `b.left`), `startOffset`, `endOffset`, `endArrow`, `end`. Animate `end` to draw.
- **CubicBezier**: `p0`–`p3` (endpoints and controls). Use `toLocal(from.absolutePosition())` etc. so the curve follows two nodes. `end` can be a callback for scroll-based reveal.
- **tween(duration, fn)**: `fn(value)` with `value` 0..1; use to drive external state (Three.js, or any JS) and then `rerender()` or similar.
- **modify(value, fn)**: transform a `SignalValue`; e.g. `fromTo(a, b, v)` = `modify(v, vec => b.worldToLocal().transformPoint(a.worldToParent().inverse().transformPoint(vec)))` so a point in `a`’s space is expressed in `b`’s (for `Line.points` in `b`).
- **reparent(newParent)**: `node.reparent(parent)` moves the node. Use `position.save()`, `moveOffset`, etc. when restructuring.

---

## Snippets

**createRefMap**

```ts
const panels = createRefMap<Rect>();
view.add(
  <Rect ref={panels.viewport} />
  <Rect ref={panels.sidebar} />
);
yield* panels.viewport().opacity(1, 0.3);
```

**createRefArray**

```ts
const items = createRefArray<Rect>();
view.add(<><Rect ref={items} /><Rect ref={items} /></>);
yield* items[0]().opacity(1, 0.3);
```

**Ray from node to node**

```ts
<Ray
  from={window.right}
  to={paper.left}
  startOffset={28}
  endOffset={20}
  endArrow
  end={0}
  lineWidth={8}
  stroke={theme.stroke}
/>
yield* ray().end(1, 0.6);
```

**CubicBezier between two nodes**

```ts
function toLocal(v: Vector2) {
  return line.worldToLocal().transformPoint(v);
}
<CubicBezier
  p0={() => toLocal(from.absolutePosition())}
  p1={() => [mid1().x, toLocal(from.absolutePosition()).y]}
  p2={() => [mid2().x, toLocal(to.absolutePosition()).y]}
  p3={() => toLocal(to.absolutePosition())}
  lineWidth={8}
  stroke={theme.window}
/>
```

**tween with function (drive external state)**

```ts
yield* tween(2, value => {
  externalObject.x = map(0, 100, easeInOutCubic(value));
  scene.updateWorldMatrix(true, true);
  three().rerender();
});
```

**modify for fromTo (Line in outline’s space)**

```ts
function fromTo(a: Node, b: Node, value: SignalValue<PossibleVector2>) {
  return modify(value, v => {
    const world = a.worldToParent().inverse().transformPoint(new Vector2(v));
    return b.worldToLocal().transformPoint(world);
  });
}
outline().points([
  fromTo(viewport, outline, viewport.topRight()),
  fromTo(viewport, outline, viewport.bottomRight()),
  // ...
]);
```

**reparent**

```ts
node.reparent(newParent);
// often followed by position/size tweaks; use position.save() to restore
```

---

## Example scenes

- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (createRefMap, createRefArray, Ray, modify, fromTo, reparent)
- `repos/examples/examples/asset-code/src/scenes/state-machine.tsx` (createRefMap, Code, Atlas, Page)
- `repos/examples/examples/asset-code/src/scenes/shader-graph.tsx` (CubicBezier, createRefMap, createRefArray)
- `repos/examples/examples/smooth-parallax/src/scenes/layers.tsx` (createRefMap-style patterns, Line, moveToBottom)

---

## See also

- [03-signals-and-refs](03-signals-and-refs.md) – createRef, makeRef
- [04-2d-components](04-2d-components.md) – Line, Ray
- [12-three-and-3d](12-three-and-3d.md) – tween + rerender
- [agent-quickref](agent-quickref.md) – "createRefMap/Array", "Ray between nodes", "CubicBezier", "tween with function", "reparent"
