# Layout

Flexbox-style layout for child nodes. Use to arrange Circle, Rect, Txt, Img, etc. in rows, columns, or with spacing and alignment.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **layout**: `true` to enable (or use the default).
- **direction**: `'row'` or `'column'` (main axis).
- **gap**: Space between children.
- **padding**: Inner padding.
- **alignItems**, **justifyContent**: Alignment (e.g. `'center'`, `'start'`, `'end'`).
- **width**, **height**: Size of the layout box; children are laid out inside it.

---

## Usage

Wrap nodes in a `Layout` and set direction/gap/alignment:

```tsx
view.add(
  <Layout layout direction="row" gap={20} alignItems="center">
    <Circle width={40} height={40} fill="red" />
    <Txt text="Label" />
  </Layout>
);
```

Children can be any 2D nodes (Rect, Circle, Txt, Img, nested Layout, etc.).

---

## See also

- [2d-components](../2d-components.md)
- [Shapes](shapes.md)
