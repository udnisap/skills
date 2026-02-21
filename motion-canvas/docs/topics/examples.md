# Examples

Official example projects from the Motion Canvas examples repo. Each can be run with the command below from the repo root (after `npm install`). They demonstrate different features and patterns.

Back to [index](index.md).

---

## List of examples

| Example | Run command | What it demonstrates |
|---------|-------------|----------------------|
| **Smooth Parallax** | `npm run smooth-parallax` | Parallax effects, Three.js integration, custom components (Upscale, Parallax). |
| **Deferred Lighting** | `npm run deferred-lighting` | Deferred lighting, Three.js, shadows, Light component. |
| **Logo** | `npm run logo` | Basic Motion Canvas logo-style animation. |
| **Asset Code** | `npm run asset-code` | Code node, syntax highlighting, Binary/Atlas nodes, code-focused animations. |
| **Anniversary** | `npm run anniversary` | "One Year of Motion Canvas" style, commit/data visualization. |
| **Motion Canvas** | `npm run motion-canvas` | Core features: signals, layouts, and main library usage. |

---

## How to run (repos)

The examples repo is included in this skill as a git submodule at `repos/examples` (from the skill root). Clone the skill with `--recurse-submodules` or run `git submodule update --init --recursive` to populate it.

1. From the **skill root** (the `motion-canvas/` folder): `cd repos/examples && npm install`
2. Run one of the scripts above, e.g. `npm run smooth-parallax`
3. Open the URL shown (e.g. localhost) to view the example in the editor.

See [repos](../../repos/) for the submodule location.

---

## Concepts by example

- **Signals and layout**: [signals-and-animation](signals-and-animation.md), [Layout](components/layout.md) — motion-canvas, logo.
- **Code and syntax**: [Code](components/code.md) — asset-code.
- **3D / Three.js**: smooth-parallax, deferred-lighting (custom 3d integration).
- **Custom nodes**: smooth-parallax (Parallax, Upscale), deferred-lighting (Light).

---

## See also

- [getting-started](getting-started.md)
- [2d-components](2d-components.md)
- [components/code](components/code.md)
