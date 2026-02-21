# 11 – Custom shaders

**When to use:** You need custom GLSL on a `Rect` or other node (e.g. SDF blending, procedural noise, custom composition). The fragment shader receives uniforms; include Motion Canvas common if you need standard helpers.

---

## Import map

- `Rect` (or any node that supports `shaders`) from `@motion-canvas/2d`
- GLSL as string: `import shader from './shader.glsl';` (Vite/plugin resolves)
- `Color`, `Matrix2D` from `@motion-canvas/core` for uniforms

---

## Concepts

- **shaders**: `{ fragment: string, uniforms?: Record<string, T> }`. `fragment` is the GLSL fragment source. `uniforms` can be numbers, `Color`, `Matrix2D`, or **signals** (reactive). Use `() => value` for matrices from node transforms: `dataMatrix: () => new Matrix2D(data().worldToLocal())`.
- **#include "@motion-canvas/core/shaders/common.glsl"**: provides common utilities and varying/uniform glue. Use in your shader.
- Typical uniforms: `vec4` (color), `float`, `mat3`/`mat2` (Matrix2D), and signals so the shader updates when they change.

---

## Snippets

**Rect with custom fragment and uniforms**

```ts
import shader from '../shaders/background.glsl';

<Rect
  size={'100%'}
  zIndex={-1}
  shaders={{
    fragment: shader,
    uniforms: {
      background: new Color('#0000'),
      backgroundSd: backgroundSd,  // signal
      shape,
      blur: 0.5,
      dataMatrix: () => new Matrix2D(data().worldToLocal()),
    },
  }}
/>
```

**Fragment shader header (common.glsl)**

```glsl
#version 300 es
precision highp float;

#include "@motion-canvas/core/shaders/common.glsl"

uniform float backgroundSd;
uniform vec4 background;
uniform float shape;

void main() {
  // use gl_FragCoord, u_resolution, etc. from common
}
```

**Uniforms: signals and callbacks**

```ts
uniforms: {
  edge: edge,           // signal -> auto-update
  morph: morph,
  dataMatrix: () => new Matrix2D(data().worldToLocal()),  // per-frame
  blur: 0.5,           // constant
}
```

**Shader on a small preview Rect (e.g. graph node)**

```ts
<Rect
  size={320}
  radius={8}
  shaders={{
    fragment: shader,
    uniforms: { index },
  }}
/>
```

---

## Example scenes

- `repos/examples/examples/asset-code/src/scenes/intro.tsx` (Binary with shaders, many uniforms including signals and Matrix2D)
- `repos/examples/examples/asset-code/src/scenes/division.tsx` (Rect with shaders, background.glsl)
- `repos/examples/examples/asset-code/src/scenes/division2.tsx` (Rect with shaders)
- `repos/examples/examples/asset-code/src/scenes/shader-graph.tsx` (Rect with shaders, `uniform float index`)
- `repos/examples/examples/asset-code/src/shaders/background.glsl`
- `repos/examples/examples/asset-code/src/shaders/shader-graph.glsl`

---

## See also

- [03-signals-and-refs](03-signals-and-refs.md) – signals as uniforms
- [04-2d-components](04-2d-components.md) – Rect
- [agent-quickref](agent-quickref.md) – "custom GLSL on a Rect"
