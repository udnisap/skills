# 2D components overview

All built-in 2D nodes you can add to a scene. Each has a short doc in [components/](components/).

Back to [index](index.md).

---

## Components (links)

| Component | Doc | Purpose |
|-----------|-----|---------|
| LaTeX | [latex](components/latex.md) | Equations and math |
| Code | [code](components/code.md) | Syntax-highlighted code |
| Txt | [txt](components/txt.md) | Text |
| Shapes | [shapes](components/shapes.md) | Circle, Rect, Polygon |
| Line & Ray | [line-ray](components/line-ray.md) | Lines and rays |
| Layout | [layout](components/layout.md) | Flexbox layout |
| Img | [img](components/img.md) | Images |
| Video | [video](components/video.md) | Video |
| SVG | [svg](components/svg.md) | SVG content |

---

## Common ideas

- **Node**: All 2D components extend Node. They have **position**, **scale**, **rotation**, **opacity**, and can be nested. Use **createRef** and **yield* ref().prop(value, duration)** to animate.
- **Signals**: Properties are signals; see [signals-and-animation](signals-and-animation.md).
- **Layout**: Use [Layout](components/layout.md) to arrange children in a row or column with gap and alignment.

Paths and curves (e.g. **Curve** for Bézier paths) are also part of the 2d package; for complex paths you compose from segments or use SVG.

---

## See also

- [2d](2d.md) (package)
- [scenes-and-generators](scenes-and-generators.md)
