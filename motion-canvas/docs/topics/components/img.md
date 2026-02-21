# Img

Displays an image in the scene. Source can be a URL or an asset path resolved by the project.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **src**: Image source (URL string or import/asset path).
- **width**, **height**: Display size; if one is set, the other can scale to preserve aspect ratio.
- **smooth**: Whether to smooth scale (default true).
- Standard Node props: **position**, **scale**, **rotation**, **opacity**, etc.

---

## Usage

Add an image to the view; animate position, scale, or opacity like any node:

```tsx
view.add(<Img src="/path/to/image.png" width={200} />);
```

For video, use [Video](video.md).

---

## See also

- [Video](video.md)
- [SVG](svg.md)
