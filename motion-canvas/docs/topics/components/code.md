# Code

Syntax-highlighted code with animation. Uses Lezer for parsing and highlighting.

Back to [2d-components](../2d-components.md) · [index](../index.md).

---

## Props (main)

- **code**: The code string (or signal). Animatable via `code().code(...)`.
- **highlighter**: Optional highlighter instance; defaults to `Code.defaultHighlighter` (set in project config with a Lezer parser).
- **selection**: Range(s) to highlight (e.g. for "current line" or selection).

---

## Animating code

The `code` property is a `CodeSignal` with:

- **Tween to new code**: `yield* code().code('const x = 1;', 0.6)` — diffs and animates the change.
- **append / prepend**: `yield* code().code.append('\nconst two = 2;', 0.6)` and `.prepend(...)`.
- **insert / replace / remove**: Use `CodeRange` (e.g. `word()`, `lines()`) for precise edits.
- **edit**: Template-string style: `` yield* code().code.edit(0.6)`...${insert('...')}...${replace('a','b')}...` ``.

Set `Code.defaultHighlighter` to a `LezerHighlighter` for your language so syntax highlighting works.

---

## See also

- [Txt](txt.md)
- [LaTeX](latex.md)
