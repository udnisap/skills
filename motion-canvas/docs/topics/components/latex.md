# LaTeX

Renders and animates LaTeX equations. Uses MathJax under the hood; extends SVG node.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **tex**: LaTeX string, or array of strings. Use `{{...}}` in the string to split into parts for per-part animation.
- **renderProps**: Options for the MathJax renderer.
- **SVGNode props**: `fill`, `fontSize`, `x`, `y`, etc. (inherited).

---

## Animating

Tween the `tex` property. Pass a new LaTeX string (with optional `{{...}}` segments) and duration; the node animates from the previous equation to the new one. Example:

```tsx
const tex = createRef<Latex>();
view.add(<Latex ref={tex} tex="{{y=}}{{a}}{{x^2}}" fill="white" />);
yield* tex().tex('{{y=}}{{a}}{{x^2}} + {{bx}}', 1);
```

---

## See also

- [Code](code.md) (similar animation model)
- [SVG](svg.md) (base for LaTeX rendering)
