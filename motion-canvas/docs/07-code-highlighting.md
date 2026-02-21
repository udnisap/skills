# 07 – Code highlighting

**When to use:** You need syntax-highlighted code (Code component) with Lezer-based or custom highlighters, `CODE` tagged template, or `code.append` / `code.prepend` to add/prefix lines.

---

## Import map

- `Code`, `CODE`, `LezerHighlighter`, `withDefaults` from `@motion-canvas/2d`
- `lines` from `@motion-canvas/2d` (for `code().selection(lines(...))`)
- Lezer parsers: `@lezer/javascript`, `@lezer/rust`, `@lezer/yaml`, etc.
- `HighlightStyle`, `tags` from `@codemirror/language` and `@lezer/highlight` for styles

---

## Concepts

- **Code**: `code` (string or signal), `highlighter` (LezerHighlighter or `null` for plain), `fontSize`, `fontFamily`, `fill`, etc. Use **code()** for tweens: `code().selection(lines(4, 6), 0.6)`.
- **CODE\`...\`**: tagged template; embeds signals/live values as \`${data}\` and marks them for highlighting (vs raw string).
- **Code.createSignal(...)**: build a signal whose value is the code string; pass into CODE or `code={data}`.
- **code.append(str, duration)** / **code.prepend(duration)\`str\`**: add at end or beginning with optional tween duration.
- **code().selection(ranges, duration)**: same idea as CodeBlock; **findAllRanges(needle)** for all matches.
- **LezerHighlighter(parser, HighlightStyle)**: parser from @lezer/...; extend to override `highlight()` for custom tokens.
- **withDefaults(Code, { highlighter, fill, ... })**: create a preconfigured `PlainCode`, `RSCode`, `JSCode`, etc.

---

## Snippets

**Code with Lezer highlighter**

```ts
import {Code, LezerHighlighter} from '@motion-canvas/2d';
import {parser as js} from '@lezer/javascript';
import {HighlightStyle, tags} from '@codemirror/language';

const Style = HighlightStyle.define([
  { tag: tags.keyword, color: '#ff5d62' },
  { tag: tags.string, color: '#98bb6c' },
  // ...
]);

<Code
  ref={code}
  highlighter={new LezerHighlighter(js, Style)}
  code={`const x = 1;`}
  fontFamily={'JetBrains Mono'}
  fontSize={28}
/>
```

**CODE tagged template with embedded signal**

```ts
const data = Code.createSignal('  [1, 2, 3],');
<Code ref={code} code={CODE`[\n${data}\n];`} highlighter={...} />
yield* data(`  [4, 5, 6],`, 0.6);
```

**code.append and code.prepend**

```ts
yield* code().selection(lines(4, 17), 0.6);
yield* code().code.append(
  `

fn render_mesh(matrix: &Mat4) {
  // ...
}`,
  0.6,
);
yield* code().code.prepend(0.4)`const MESH: [[f32; 3]; 12] = `;
```

**Selection and findAllRanges**

```ts
yield* code().selection(lines(4, 6), 0.6);
yield* code().selection(code().findAllRanges('MESH'), 0.4);
```

**PlainCode (no highlighter) via withDefaults**

```ts
const PlainCode = withDefaults(Code, { fill: 'white', fontSize: 32, highlighter: null });
<PlainCode code={`Data { ... }`} />
```

---

## Example scenes

- `repos/examples/examples/asset-code/src/scenes/mesh.tsx` (Code, CODE, RSCode, lines, append, prepend, findAllRanges)
- `repos/examples/examples/asset-code/src/scenes/state-machine.tsx` (JSCode, YamlCode, Atlas, Page)
- `repos/examples/examples/asset-code/src/nodes/Code.ts` (LezerHighlighter, withDefaults, custom CsharpHighlighter, YamlHighlighter)

---

## See also

- [06-code-block](06-code-block.md) – CodeBlock, edit, insert (editable tutorial code)
- [03-signals-and-refs](03-signals-and-refs.md) – createRef, createSignal
- [agent-quickref](agent-quickref.md) – "syntax-highlighted Code", "append/prepend to Code"
