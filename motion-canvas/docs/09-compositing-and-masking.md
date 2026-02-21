# 09 – Compositing and masking

**When to use:** You need to mask (show/hide with shapes), composite (multiply, add, destination-in/out), clip children to a rect, cache a subtree, or blur.

---

## Import map

- `compositeOperation` on `Node`/`Rect`/`Img` (canvas globalCompositeOperation)
- `clip` on `Node`/`Rect`
- `cache`, `cachePadding` on `Node`
- `blur` from `@motion-canvas/2d` (in `filters` array)

---

## Concepts

- **compositeOperation**: canvas `globalCompositeOperation`. Common: `'destination-in'` (mask: keep where drawn), `'destination-out'` (erase where drawn), `'source-atop'`, `'multiply'`, `'lighter'` (additive).
- **clip**: children are clipped to the node's bounds.
- **cache**: subtree is rasterized to a texture; improves performance when the subtree is complex. Use `cachePadding` if content extends beyond bounds.
- **filters={[blur(px)]}**: blur the node.

---

## Snippets

**destination-in mask (show only where mask draws)**

```ts
// Trail of rects, then a white rect with destination-in to mask the top
<Node>
  <Trail>{/* colored rects */}</Trail>
  <Rect
    width={40}
    height={270}
    fill={'white'}
    offsetY={-1}
    compositeOperation={'destination-in'}
  />
</Node>
```

**destination-out (cut out / erase)**

```ts
<Rect
  width={100}
  height={150}
  fill={'white'}
  offsetY={1}
  rotation={(360 / 5) * i}
  compositeOperation={'destination-out'}
/>
```

**multiply and lighter (deferred-style light * color, light A + light B)**

```ts
<Img src={lightMap} compositeOperation="multiply" />
<Img src={lightA} compositeOperation="lighter" />
```

**clip children**

```ts
<Rect clip width={800} height={450}>
  {/* children clipped to rect */}
</Rect>
```

**cache for performance**

```ts
<Node cache>
  {/* complex subtree */}
</Node>
```

**blur**

```ts
import {blur} from '@motion-canvas/2d';

<Circle filters={[blur(20)]} />
```

---

## Example scenes

- `repos/examples/examples/logo/src/scenes/logo.tsx` (compositeOperation destination-in, destination-out, cache)
- `repos/examples/examples/anniversary/src/scenes/intro.tsx` (clip, compositeOperation destination-out, blur on Circle)
- `repos/examples/examples/deferred-lighting/src/scenes/lightBasics.tsx` (multiply, lighter, Frame/Imgs)
- `repos/examples/examples/asset-code/src/scenes/shader-graph.tsx` (cachePadding)

---

## See also

- [04-2d-components](04-2d-components.md) – Node, Rect
- [10-images-and-media](10-images-and-media.md) – Img
- [14-deferred-and-buffers](14-deferred-and-buffers.md) – multiply, lighter in deferred context
- [agent-quickref](agent-quickref.md) – "mask with compositeOperation", "clip", "cache", "blur"
