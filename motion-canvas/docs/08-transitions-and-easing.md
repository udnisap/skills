# 08 – Transitions and easing

**When to use:** You need scene-entry transitions (slide, zoom in/out), custom easing on tweens, or to map/remap values (lerp, inverse lerp) and use arc lerp for position/size.

---

## Import map

- `slideTransition`, `zoomInTransition`, `zoomOutTransition` from `@motion-canvas/core/lib/transitions` or `@motion-canvas/core`
- `Direction` from `@motion-canvas/core/lib/types` or `@motion-canvas/core`
- `BBox`, `Vector2` from `@motion-canvas/core/lib/types` or `@motion-canvas/core`
- `linear`, `easeOutCubic`, `easeInCubic`, `easeInOutCubic`, `easeOutElastic`, `easeOutExpo`, `easeInOutExpo` from `@motion-canvas/core/lib/tweening` or `@motion-canvas/core`
- `map`, `remap` from `@motion-canvas/core/lib/tweening` or `@motion-canvas/core`

---

## Concepts

- **slideTransition(Direction, duration?)**: slide scene in; `Direction.Bottom`, `Direction.Top`, `Direction.Left`, `Direction.Right`.
- **zoomInTransition(bbox, duration?)**: zoom from a `BBox` region (e.g. video crop) into the full scene; **zoomOutTransition(bbox, duration?)** zooms out to that region.
- **Easing**: pass as 3rd (or 4th) argument to a tween: `node.x(100, 1, easeOutCubic)`. Common: `linear`, `easeInCubic`, `easeOutCubic`, `easeInOutCubic`, `easeOutElastic`, `easeOutExpo`, `easeInOutExpo`.
- **map(from, to, t)**: lerp; `map(0, 100, t)` where `t` 0..1.
- **remap(a, b, c, d, x)**: map `x` from `[a,b]` to `[c,d]`.
- **Vector2.createArcLerp(radians, power?)** / **Vector2.arcLerp**: for position/size so the path curves; e.g. `node.position([x,y], 0.6, easeInOutCubic, Vector2.createArcLerp(true, 2))`.

---

## Snippets

**slideTransition**

```ts
import {slideTransition} from '@motion-canvas/core/lib/transitions';
import {Direction} from '@motion-canvas/core/lib/types';

yield* slideTransition(Direction.Bottom, 1);
```

**zoomInTransition from a video region**

```ts
import {zoomInTransition} from '@motion-canvas/core/lib/transitions';
import {BBox} from '@motion-canvas/core/lib/types';

yield* zoomInTransition(new BBox(100, 435, 480, 270), 0.6);
```

**zoomOutTransition**

```ts
yield* zoomOutTransition(new BBox(1040, 405, 480, 270), 0.6);
```

**Easing on a tween**

```ts
import {easeOutCubic, easeInOutCubic, easeOutElastic} from '@motion-canvas/core/lib/tweening';

yield* circle().scale(1.5, 0.5, easeOutCubic);
yield* rect().position([100, 50], 1, easeInOutCubic);
yield* shape(1, 1.6, easeOutElastic);
```

**map and remap**

```ts
import {map, remap} from '@motion-canvas/core/lib/tweening';

// lerp: value from 0..1 -> 200..400
width={() => map(200, 400, progress())}
// remap: value in [0,1] -> [min,max]
() => remap(0, 1, 100, 500, t)
```

**Vector2 arc lerp for position/size**

```ts
import {Vector2} from '@motion-canvas/core/lib/types';

yield* node.size([w, h], 0.6, easeInOutCubic, Vector2.createArcLerp(true, 2));
yield* node.position(target, 0.6, easeInOutCubic, Vector2.arcLerp);
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/scenes/layouts.tsx` (slideTransition)
- `repos/examples/examples/motion-canvas/src/scenes/interface.tsx` (slideTransition, linear)
- `repos/examples/examples/smooth-parallax/src/scenes/parallax.tsx` (zoomInTransition, BBox)
- `repos/examples/examples/smooth-parallax/src/scenes/outro.tsx`, `merge.tsx` (zoomOutTransition)
- `repos/examples/examples/anniversary/src/scenes/intro.tsx` (easeInOutCubic, Vector2.createArcLerp, useDuration)
- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (Vector2.createArcLerp, easeInOutCubic)

---

## See also

- [02-scenes-and-flow](02-scenes-and-flow.md) – yield*, waitUntil
- [05-layouts](05-layouts.md) – map for grow
- [13-parallax-and-camera](13-parallax-and-camera.md) – zoomInTransition from video
- [agent-quickref](agent-quickref.md) – "slide in", "zoom into region", "custom easing", "map/remap"
