# SVG

Renders SVG content (markup string or parsed SVG). Base for vector graphics and for nodes like [LaTeX](latex.md) that render to SVG.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **svg** (or equivalent): The SVG document or string to render.
- **fill**, **stroke**: Override or default styles.
- Standard Node props: **position**, **scale**, **rotation**, **opacity**, **width**, **height**.

---

## Role

- Use when you have existing SVG (icons, illustrations) to embed in the scene.
- LaTeX and some other components render to SVG internally. For raw SVG markup or assets, use the SVG node directly so you can animate its props or swap content.

---

## See also

- [LaTeX](latex.md)
- [Line & Ray](line-ray.md)
- [Shapes](shapes.md)
