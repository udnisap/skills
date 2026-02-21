# 04 – 2D components

**When to use:** You need to add shapes, text, images, paths, grids, or lines (including arrows) to the scene.

---

## Import map

- `Node`, `Rect`, `Circle`, `Line`, `Txt`, `Img`, `Path`, `Grid`, `Layout`, `Ray` from `@motion-canvas/2d` or `@motion-canvas/2d/lib/components`

---

## Concepts

- **Node**: base; supports `x`, `y`, `rotation`, `scale`, `opacity`, `position`, `layout`, `clip`, `compositeOperation`, `filters`, `cache`. **add(children)**: add nodes at runtime; e.g. `lineGroup().add(<Line .../>)`.
- **Rect, Circle**: `width`, `height` (or `size`), `fill`, `stroke`, `lineWidth`, `radius`.
- **Line**: `points` (array of `[x,y]` or `Vector2`; can use `() =>` for reactive); `start`, `end` (0–1) to animate draw; `startOffset`, `endOffset`, `startArrow`, `endArrow`, `arrowSize`, `lineDash`, `lineDashOffset`, `lineWidth`, `stroke`.
- **Txt**: `text` (string or callback); `text()` returns a tweenable: `txt().text('New', 1, linear)`. Also `fontSize`, `fontFamily`, `fill`, `lineHeight`, `textAlign`, `textWrap`, `offsetX`, `offsetY`.
- **Img**: `src` (URL or import), `width`/`height` or `size`, `smoothing`.
- **Path**: `data` (SVG d string), `fill`, `stroke`; position/scale for placement.
- **Grid**: `spacing`, `stroke`, `lineWidth`, `size`, `lineDash`, `lineDashOffset`.
- **Ray**: `from`, `to` (node edges like `a.right`, `b.left`), `startOffset`, `endOffset`, `endArrow`, `end`, `lineWidth`, `stroke`.

---

## Snippets

**Rect and Circle**

```ts
<Rect width={240} height={240} fill={'#ff6470'} radius={8} />
<Circle width={240} height={240} fill={'#68ABDF'} />
```

**Line with draw animation**

```ts
const line = createRef<Line>();
view.add(
  <Line
    ref={line}
    points={[[0, 0], [200, 200]]}
    stroke={'#666'}
    lineWidth={8}
    endArrow
    end={0}
  />,
);
yield* line().end(1, 0.6);
```

**Line with reactive points**

```ts
<Line
  points={[() => circle().position(), () => square().position()]}
  stroke={'#666'}
  lineWidth={8}
  endArrow
/>
```

**Txt and animate text**

```ts
const label = createRef<Txt>();
view.add(<Txt ref={label} fontSize={32} fill={'white'} />);
yield label().text('Hello', 1, linear);
```

**Img**

```ts
<Img src={imageUrl} width={400} />
// or imported: import logo from './logo.svg';
```

**Path from SVG d**

```ts
<Path data="M10,10 L90,90" fill={'#666'} />
```

**Grid**

```ts
<Grid spacing={80} stroke={'#333'} lineWidth={2} size={'120%'} />
```

**Ray (arrow between nodes)**

```ts
<Ray from={nodeA.right} to={nodeB.left} endArrow end={0} lineWidth={8} stroke={'#666'} />
```

---

## Example scenes

- `repos/examples/examples/logo/src/scenes/logo.tsx` (Rect, compositeOperation)
- `repos/examples/examples/motion-canvas/src/scenes/interface.tsx` (Txt)
- `repos/examples/examples/motion-canvas/src/scenes/signals.tsx` (Circle, Line, Rect, Txt)
- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (Path, Grid, Img, Ray)
- `repos/examples/examples/asset-code/src/scenes/division.tsx` (Rect, Path, Circle)

---

## See also

- [03-signals-and-refs](03-signals-and-refs.md) – createRef, makeRef for animating these
- [05-layouts](05-layouts.md) – Layout, direction, grow
- [09-compositing-and-masking](09-compositing-and-masking.md) – compositeOperation, clip, cache
- [10-images-and-media](10-images-and-media.md) – Img, Gradient, SVG
- [15-advanced-patterns](15-advanced-patterns.md) – Ray, CubicBezier
- [agent-quickref](agent-quickref.md) – "simple 2D shape", "line between points", "add text"
