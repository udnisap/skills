# 10 – Images and media

**When to use:** You need to show images, fill with a gradient, use video frames or stills, or import SVG and use `Path` with `data` from SVG elements.

---

## Import map

- `Img`, `Gradient` from `@motion-canvas/2d` or `@motion-canvas/2d/lib/components`
- `Path` from `@motion-canvas/2d` or `@motion-canvas/2d/lib/components`
- `Color` from `@motion-canvas/core` for `Color.createSignal` in gradients

---

## Concepts

- **Img**: `src` (URL or `import img from './x.png'`), `width`/`height` or `size`, `smoothing` (default true). For video, use a frame image or `play`/`time` if supported.
- **Gradient**: `new Gradient({ type: 'linear', from, to, stops })`. `from`/`to` are `Vector2` or `fromX, fromY, toX, toY`. `stops`: `[{ offset: 0, color }, { offset: 1, color }]`. `color` can be a `Color` signal.
- **view.fill(gradient)**: fill the view with a gradient.
- **SVG**: import as `?raw` and parse; use `Path` with `data={el.getAttribute('d')}` and `fill`/`stroke`. For inline SVG use `SVG` with `svg={raw}`.
- **Path**: `data` (SVG `d`), `fill`, `stroke`, `position`, `scale` for placement.

---

## Snippets

**Img**

```ts
import logo from './logo.svg';
<Img src={logo} width={200} />
<Img src={'https://...'} width={400} height={300} smoothing={false} />
```

**Gradient on view**

```ts
import {Gradient} from '@motion-canvas/2d';
import {Vector2} from '@motion-canvas/core/lib/types';

view.fill(
  new Gradient({
    type: 'linear',
    from: view.size().scale(-0.5),
    to: view.size().scale(0.5),
    stops: [
      { offset: 0, color: 'rgba(85,88,218,1)' },
      { offset: 1, color: 'rgba(95,209,249,1)' },
    ],
  }),
);
```

**Gradient with Color.createSignal (animated)**

```ts
const from = Color.createSignal('rgba(85,88,218,1)');
const to = Color.createSignal('rgba(95,209,249,1)');
view.fill(
  new Gradient({
    type: 'linear',
    from: view.size().scale(-0.5),
    to: view.size().scale(0.5),
    stops: [{ offset: 0, color: from }, { offset: 1, color: to }],
  }),
);
yield* from('rgb(255, 148, 114)', 1);
```

**Path from SVG (parsed from ?raw)**

```ts
import svgRaw from './asset.svg?raw';
const container = document.createElement('div');
container.innerHTML = svgRaw;
const pathEl = container.querySelector('path');
<Path data={pathEl.getAttribute('d')} fill={'#666'} />
```

**Path with position/scale**

```ts
<Path
  data="M10,10 L90,90"
  fill={theme.stroke}
  position={parent.position().scale(-1)}
  scale={0.1}
/>
```

---

## Example scenes

- `repos/examples/examples/anniversary/src/scenes/intro.tsx` (Img, Gradient, Color.createSignal, clip)
- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (Img, Path from SVG, `logo.svg?raw`)
- `repos/examples/examples/asset-code/src/scenes/mesh.tsx` (Path from SVG, `asset-tiles.svg?raw`, `executable.svg?raw`)
- `repos/examples/examples/deferred-lighting/src/scenes/lightBasics.tsx` (Img as Frame, compositeOperation)
- `repos/examples/examples/smooth-parallax/src/scenes/parallax.tsx` (Img for video frame, train.png)

---

## See also

- [04-2d-components](04-2d-components.md) – Img, Path
- [09-compositing-and-masking](09-compositing-and-masking.md) – compositeOperation on Img
- [14-deferred-and-buffers](14-deferred-and-buffers.md) – Img as Frame in buffers
- [agent-quickref](agent-quickref.md) – "show an image", "fill with gradient", "SVG as Path"
