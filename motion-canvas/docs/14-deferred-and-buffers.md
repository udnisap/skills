# 14 – Deferred and buffers

**When to use:** You need to explain or visualize deferred rendering: G-buffer (color, normals), light × color, and additive lights (lighter). The examples use `Frame` (Img + label) and `GBuffer`/`LBuffer` layout components with `compositeOperation` on Imgs.

---

## Import map

- **Frame**: `name`, `refs: { value: Img, text: Txt }`, `src`, `compositeOperation` (optional). From deferred-lighting `../components`.
- **GBuffer**, **LBuffer**, **Buffer**: layout components that compose Frames; refs for `value`, `text`, `color`, `normals`.
- `Img` from `@motion-canvas/2d`
- `makeRef`, `makeRefs` from `@motion-canvas/core/lib/utils`

---

## Concepts

- **G-buffer**: color + normals (and optional depth). Rendered to separate images; displayed as a grid (e.g. `GBuffer` with `Frame` for COLOR and NORMAL).
- **Light × color**: `compositeOperation="multiply"` to show light map × albedo.
- **Additive lights**: `compositeOperation="lighter"` to add light A + light B.
- **Frame**: an `Img` with a `Txt` label; `refs` for `value` (Img) and `text` (Txt). Use `makeRefs<typeof Frame>()` for `{ value, text }`.
- **LBuffer / output buffer**: holds the final shaded image (e.g. `Frame` with `src={shaded}`).

---

## Snippets

**Frame (Img + label)**

```ts
<Frame
  name="COLOR"
  refs={colorRef}
  src={colorImage}
  width={440}
/>
<Frame name="LIGHT" refs={lightRef} src={lightImage} compositeOperation="lighter" />
```

**Multiply (light × color)**

```ts
<Frame
  name="SHADED"
  refs={finalRef}
  src={shadedImage}
  fill={'#242424'}
/>
// multiply is applied when compositing light pass onto color
```

**Lighter (additive lights)**

```ts
colorLeft.value.compositeOperation('lighter', 0.5);
// or on Img: compositeOperation="lighter"
```

**GBuffer with color and normals**

```ts
<GBuffer refs={gbuffer} width={520} />
// refs: { value, text, color: { value, text }, normals: { value, text } }
```

---

## Example scenes

- `repos/examples/examples/deferred-lighting/src/scenes/lightBasics.tsx` (GBuffer, LBuffer, Frame, multiply, lighter)
- `repos/examples/examples/deferred-lighting/src/scenes/color.tsx`
- `repos/examples/examples/deferred-lighting/src/scenes/normals.tsx`, `normal.tsx`
- `repos/examples/examples/deferred-lighting/src/components/GBuffer.tsx` (Frame, GBuffer, LBuffer, Buffer)

---

## See also

- [09-compositing-and-masking](09-compositing-and-masking.md) – compositeOperation multiply, lighter
- [10-images-and-media](10-images-and-media.md) – Img
- [04-2d-components](04-2d-components.md) – Rect, Layout
- [agent-quickref](agent-quickref.md) – "deferred-style buffers"
