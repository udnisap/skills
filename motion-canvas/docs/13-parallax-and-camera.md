# 13 – Parallax and camera

**When to use:** You need parallax layers (different scroll speeds), a camera/FOV diagram, or to zoom from a video region (BBox) into the full scene.

---

## Import map

- **Parallax**: custom in `smooth-parallax`; `camera`, `ratios`, `upscale`, `snap`, `light`. `parallax().layers`, `parallax().ratios()`, `parallax().camera(x)`.
- `zoomInTransition`, `zoomOutTransition` from `@motion-canvas/core/lib/transitions`
- `BBox` from `@motion-canvas/core/lib/types`
- `Img`, `Rect`, `Line`, `Txt` for camera/FOV diagrams and ratio labels

---

## Concepts

- **Parallax**: `ratios` is an array of layer speeds (e.g. `[0.4, 0.6, 1, 2]`); `camera` is the scroll offset. `upscale` controls pixel scale; `snap` for subpixel snapping.
- **zoomInTransition(bbox, duration)**: zoom from that rectangle (e.g. video crop) into the full scene. **zoomOutTransition(bbox, duration)** zooms out to that region.
- **BBox(x, y, width, height)**: rectangle in scene coordinates.
- **createRatios** (in examples): helper that adds Line+Txt to show `d1/d2`-style ratios; returns `{ show, hide }` generators.

---

## Snippets

**Parallax with ratios and camera**

```ts
import {Parallax} from '../components';

<Parallax
  ref={parallax}
  ratios={() => [0.4, 0.6, 1, 2]}
  upscale={30}
/>
// drive scroll
yield* parallax().camera(-200, 0.6);
```

**Zoom from video region into scene**

```ts
import {zoomInTransition} from '@motion-canvas/core/lib/transitions';
import {BBox} from '@motion-canvas/core/lib/types';

yield* zoomInTransition(new BBox(100, 435, 480, 270), 0.6);
```

**Zoom out to a region**

```ts
yield* zoomOutTransition(new BBox(1040, 405, 480, 270), 0.6);
```

**FOV-style rays (Line with reactive points)**

```ts
const fov = createSignal(0);
<Line
  points={[() => [(scan() - 0.5) * fov(), -800], 0]}
  lineWidth={8}
  stroke={Colors.blue}
  end={0}
/>
yield* fov(1200, 0.6);
```

---

## Example scenes

- `repos/examples/examples/smooth-parallax/src/scenes/parallax.tsx` (zoomInTransition, BBox, Parallax, createRatios, FOV, scan)
- `repos/examples/examples/smooth-parallax/src/scenes/layers.tsx` (Parallax, ratios, camera, perspective, d1/d2)
- `repos/examples/examples/smooth-parallax/src/scenes/upscale.tsx`
- `repos/examples/examples/smooth-parallax/src/components/Parallax.tsx`

---

## See also

- [08-transitions-and-easing](08-transitions-and-easing.md) – zoomInTransition, zoomOutTransition, BBox
- [04-2d-components](04-2d-components.md) – Line, Img
- [10-images-and-media](10-images-and-media.md) – Img for layers
- [agent-quickref](agent-quickref.md) – "parallax layers", "zoom from video region"
