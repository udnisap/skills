# 06 – CodeBlock

**When to use:** You need to show code that is edited over time (insert/replace) and to highlight regions with `selection`. Use this for tutorial-style "typing" or "editing" code on screen.

---

## Import map

- `CodeBlock`, `edit`, `insert`, `lines`, `word` from `@motion-canvas/2d/lib/components/CodeBlock`
- `createRef` from `@motion-canvas/core/lib/utils`

---

## Concepts

- **CodeBlock**: displays code; `code` (string or `() =>`), `fontSize`, `lineHeight`, `fontFamily`, `selection` (initial). Use **edit** and **insert** in a tagged template with `code().edit(duration)\`...\``.
- **edit(old, new)**: replace a span; in template: \`...\${edit(\`old\`, \`new\`)}\` (leave unchanged parts as literal).
- **insert(str)**: insert new text: \`\${insert(\`  const x = 1;\`)}\`.
- **selection(ranges, duration)**: highlight; `yield* code().selection(lines(1, 3), 0.3)` or `word(line, col, len)`.
- **lines(from, to?)**: line range; `lines(1)` = line 1; `lines(0, Infinity)` = all.
- **word(line, col, len)**: character range for a single token.

---

## Snippets

**CodeBlock and edit (insert new line)**

```ts
const code = createRef<CodeBlock>();
view.add(
  <CodeBlock
    ref={code}
    fontFamily={'JetBrains Mono'}
    fontSize={24}
    lineHeight={36}
    code={`export default makeScene2D(function* (view) {

});`}
  />,
);
yield* code().edit(0.8)`export default makeScene2D(function* (view) {
${insert(`  const radius = createSignal(3);`)}
});`;
```

**edit (replace in place)**

```ts
yield* code().edit(1.2)`...
  const area = createSignal(${edit(`() => Math.PI * radius() * radius()`, `42`)});
...`;
```

**Selection: lines and word**

```ts
yield* code().selection(lines(1), 0.3);
yield* code().selection(lines(1, 4), 0.3);
yield* code().selection(word(1, 8, 6), 0.3); // line 1, col 8, length 6
```

---

## Example scenes

- `repos/examples/examples/motion-canvas/src/scenes/signalsCode.tsx`
- `repos/examples/examples/motion-canvas/src/scenes/layoutsCode.tsx`

---

## See also

- [02-scenes-and-flow](02-scenes-and-flow.md) – yield*, waitUntil
- [07-code-highlighting](07-code-highlighting.md) – Code, Lezer, CODE, append/prepend (different component)
- [agent-quickref](agent-quickref.md) – "animate code being edited", "change code selection"
