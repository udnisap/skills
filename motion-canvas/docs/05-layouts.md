# 05 – Layouts

**When to use:** You need to stack or arrange nodes in a row/column with gap and padding, or animate `grow` (flex-grow) from a signal.

---

## Import map

- `Layout`, `Rect` from `@motion-canvas/2d` or `@motion-canvas/2d/lib/components`
- `map` from `@motion-canvas/core/lib/tweening` or `@motion-canvas/core`
- `createSignal` from `@motion-canvas/core/lib/signals` or `@motion-canvas/core`
- `Direction`, `Spacing` from `@motion-canvas/core/lib/types` or `@motion-canvas/core`

---

## Concepts

- **Layout** (or **Rect** with `layout`) uses `direction` (`'row'` | `'column'`), `gap`, `padding`, `alignItems`, `justifyContent`.
- **grow**: flex-grow; e.g. `grow={1}`. Use **map(from, to, t)** so `grow={animate(3,1)}` animates from 3 to 1 as `size` goes 0→1: `const animate = (from, to) => () => map(from, to, size());`
- **Spacing** for `radius`/`padding` that differ per side: `new Spacing(8)` or `[top, right, bottom, left]`.
- Set **layout** on the parent; children can use `layout={false}` to opt out.

---

## Snippets

**Column layout with gap and padding**

```ts
<Layout direction={'column'} gap={28} layout padding={20}>
  <Rect grow={1} />
  <Rect grow={1} />
  <Rect grow={2} />
</Layout>
```

**Row with shrink and justifyContent**

```ts
<Layout direction={'row'} gap={20} layout shrink={0} justifyContent={'space-between'}>
  <Txt text={'Left'} />
  <Txt text={'Right'} />
</Layout>
```

**Animate grow from a signal**

```ts
const size = createSignal(0);
const animate = (from: number, to: number) => () => map(from, to, size());

view.add(
  <Layout direction={'column'} gap={28} layout padding={20}>
    <Rect grow={animate(3, 1)} />
    <Rect grow={1} />
    <Rect grow={animate(2, 4)} />
  </Layout>,
);
yield size(0, 2).to(1, 2);
```

**Spacing for radius**

```ts
rect.radius(new Spacing(8));
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/scenes/layouts.tsx`
- `repos/examples/examples/asset-code/src/scenes/editor.tsx`
- `repos/examples/examples/deferred-lighting/src/scenes/layers.tsx`
- `repos/examples/examples/deferred-lighting/src/components/GBuffer.tsx`

---

## See also

- [03-signals-and-refs](03-signals-and-refs.md) – createSignal for animated grow
- [04-2d-components](04-2d-components.md) – Rect, Layout, Txt
- [08-transitions-and-easing](08-transitions-and-easing.md) – map, easing
- [agent-quickref](agent-quickref.md) – "stack in row/column", "animate layout grow"
