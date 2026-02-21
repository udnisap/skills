# Shapes (Circle, Rect, Polygon)

Basic 2D shapes: Circle, Rect, Polygon. All support fill, stroke, and standard Node transforms.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Circle

- **width**, **height** (or size): Diameter. Often set both to the same value for a circle.
- **fill**, **stroke**: Fill and stroke color.
- **lineWidth**: Stroke width.

---

## Rect

- **width**, **height**: Size.
- **radius**: Corner radius (smooth corners).
- **smoothCorners**: When true, use smooth corner curve; **sharpness** controls the curve.
- **fill**, **stroke**, **lineWidth**: Same as Circle.

---

## Polygon

- **sides**: Number of sides (e.g. 6 for hexagon).
- **radius**: Distance from center to vertices.
- **fill**, **stroke**, **lineWidth**: Same as above.

All extend the base Shape/Node; you can animate **position**, **scale**, **rotation**, **opacity**, **width**, **height**, **fill**, etc. with `yield* ref().prop(value, duration)`.

---

## See also

- [Line & Ray](line-ray.md)
- [Layout](layout.md)
