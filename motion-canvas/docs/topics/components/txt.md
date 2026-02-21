# Txt

Text display and animation. Supports nested text nodes and standard text styling.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Role

- Renders text in the scene. You can set content, font, size, fill, and other [Node](../2d.md) properties.
- Text is animatable: tween `text` (or the node's position, opacity, etc.) like any other signal.

---

## Props (main)

- **text**: The string to display (signal/value).
- **fontFamily**, **fontSize**, **fontWeight**, **fontStyle**: Typography.
- **fill**: Color (e.g. `'#fff'` or a color signal).
- **x**, **y**, **position**: Layout; inherits from Node.

---

## Usage

Add a `Txt` to the view, optionally with `createRef`, and animate:

```tsx
const label = createRef<Txt>();
view.add(<Txt ref={label} text="Hello" fontSize={48} fill="white" />);
yield* label().text('World', 0.5);
```

---

## See also

- [Code](code.md)
- [Layout](layout.md) (positioning multiple nodes)
