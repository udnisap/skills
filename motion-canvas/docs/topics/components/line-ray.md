# Line & Ray

**Line**: Polyline or polygon from a list of points. **Ray**: Single segment between two points.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Line

- **points**: Array of positions (e.g. `Vector2[]`). Defines the path; can be open (line) or closed (polygon).
- **stroke**, **lineWidth**, **fill** (if closed): Styling.
- Points are animatable: tween the **points** signal to morph the line over time.

Use for paths, outlines, and morphing shapes defined by vertices.

---

## Ray

- **from**, **to**: Start and end positions (or signals).
- **stroke**, **lineWidth**: Styling.

Simpler than Line when you only need one segment (e.g. arrows, guides).

---

## See also

- [Shapes](shapes.md)
- [SVG](svg.md) (for complex paths)
