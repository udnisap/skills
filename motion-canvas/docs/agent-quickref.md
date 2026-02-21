# Agent quick reference

One-page lookup: **"I need to..."** to doc and snippet. Use the linked doc for imports and full snippets.

---

## I need to...

| Task | Doc | Snippet |
|------|-----|---------|
| Set up a project with scenes and audio | [01-setup-and-project](01-setup-and-project.md) | `makeProject({ scenes: [scene1, scene2], audio })` |
| Define a 2D scene | [02-scenes-and-flow](02-scenes-and-flow.md) | `makeScene2D(function* (view) { ... })` |
| Wait for a named moment (voiceover/editing) | [02-scenes-and-flow](02-scenes-and-flow.md) | `yield* waitUntil('moment');` |
| Run several animations in parallel | [02-scenes-and-flow](02-scenes-and-flow.md) | `yield* all(a.opacity(1, 1), b.x(100, 1));` |
| Chain animations one after another | [02-scenes-and-flow](02-scenes-and-flow.md) | `yield* chain(a.end(1, 1), a.start(1, 1));` |
| Run a repeating background animation | [02-scenes-and-flow](02-scenes-and-flow.md) | `const task = yield loop(Infinity, () => node.rotation(0).rotation(360, 4, linear));` |
| Cancel a loop and wait for it to finish | [02-scenes-and-flow](02-scenes-and-flow.md) | `cancel(task);` then `yield* join(task);` |
| Use reactive state that triggers redraws | [03-signals-and-refs](03-signals-and-refs.md) | `const x = createSignal(0);` then `width={() => x() * 10}` |
| Derive value from other signals | [03-signals-and-refs](03-signals-and-refs.md) | `const area = createComputed(() => Math.PI * r() * r());` |
| Get a reference to a node to animate later | [03-signals-and-refs](03-signals-and-refs.md) | `const ref = createRef<Rect>();` then `<Rect ref={ref} />` and `ref().opacity(1, 1)` |
| Build a list of refs in map | [03-signals-and-refs](03-signals-and-refs.md) | `const refs: Rect[] = [];` and `ref={makeRef(refs, i)}` |
| Use a simple 2D shape | [04-2d-components](04-2d-components.md) | `<Circle width={80} height={80} fill={'#68ABDF'} />` |
| Draw a line between points | [04-2d-components](04-2d-components.md) | `<Line points={[[0,0], [100,100]]} stroke={'#666'} lineWidth={8} end={0} />` then `line().end(1, 0.5)` |
| Add text | [04-2d-components](04-2d-components.md) | `<Txt text={'Hello'} fontSize={32} fill={'white'} />` or `txt().text('New', 1, linear)` |
| Stack nodes in a row or column | [05-layouts](05-layouts.md) | `<Layout direction={'column'} gap={20} layout><Rect grow={1} /></Layout>` |
| Animate layout grow from a signal | [05-layouts](05-layouts.md) | `grow={animate(3,1)}` where `animate = (from,to) => () => map(from, to, size());` |
| Animate code being edited (CodeBlock) | [06-code-block](06-code-block.md) | `yield* code().edit(1)\`old\${insert('new')}\`;` |
| Change code selection (highlight) | [06-code-block](06-code-block.md) | `yield* code().selection(lines(1, 3), 0.3);` or `word(1, 8, 6)` |
| Show syntax-highlighted Code (Lezer) | [07-code-highlighting](07-code-highlighting.md) | `import {Code} from '@motion-canvas/2d';` then `<Code highlighter={new LezerHighlighter(parser, style)} code={\`...\`} />` |
| Append or prepend to Code | [07-code-highlighting](07-code-highlighting.md) | `yield* code().code.append(\`\nnew lines\`, 0.6);` or `code().code.prepend(0.4)\`prefix\`` |
| Slide in from bottom/top | [08-transitions-and-easing](08-transitions-and-easing.md) | `yield* slideTransition(Direction.Bottom, 1);` |
| Zoom into a region (BBox) | [08-transitions-and-easing](08-transitions-and-easing.md) | `yield* zoomInTransition(new BBox(x, y, w, h), 0.6);` |
| Use custom easing | [08-transitions-and-easing](08-transitions-and-easing.md) | `node.x(100, 1, easeOutCubic)` or `easeOutElastic`, `easeInOutCubic` |
| Map 0–1 to a range (lerp) | [08-transitions-and-easing](08-transitions-and-easing.md) | `map(0, 100, t)` or `remap(0, 1, 200, 400, t)` |
| Mask with compositeOperation | [09-compositing-and-masking](09-compositing-and-masking.md) | `compositeOperation={'destination-in'}` or `'destination-out'`, `'source-atop'` |
| Clip children to a rectangle | [09-compositing-and-masking](09-compositing-and-masking.md) | `<Rect clip>...</Rect>` |
| Cache a node for performance | [09-compositing-and-masking](09-compositing-and-masking.md) | `<Node cache>...</Node>` |
| Blur a node | [09-compositing-and-masking](09-compositing-and-masking.md) | `filters={[blur(20)]}` |
| Show an image | [10-images-and-media](10-images-and-media.md) | `<Img src={imageUrl} width={200} />` |
| Fill with a gradient | [10-images-and-media](10-images-and-media.md) | `view.fill(new Gradient({ type: 'linear', from, to, stops }))` |
| Use raw SVG as Path | [10-images-and-media](10-images-and-media.md) | `container.innerHTML = svgRaw;` then `<Path data={pathEl.getAttribute('d')} fill={color} />` |
| Custom GLSL on a Rect | [11-custom-shaders](11-custom-shaders.md) | `shaders={{ fragment: glsl, uniforms: { u: signal } }}` |
| Run Three.js / WebGL in the scene | [12-three-and-3d](12-three-and-3d.md) | Custom `Three` component: `draw()` runs `renderer.render(scene, camera)` and `context.drawImage(renderer.domElement, ...)`; call `rerender()` after tweening Three state |
| Parallax layers | [13-parallax-and-camera](13-parallax-and-camera.md) | `<Parallax ref={p} ratios={() => [0.4, 0.6, 1, 2]} />` |
| Zoom from a video region into scene | [13-parallax-and-camera](13-parallax-and-camera.md) | `yield* zoomInTransition(new BBox(x, y, w, h), 0.6);` |
| Deferred-style buffers (G-buffer, light * color) | [14-deferred-and-buffers](14-deferred-and-buffers.md) | `compositeOperation="multiply"` or `"lighter"` on Img; compose with Frame/GBuffer pattern |
| createRefMap / createRefArray | [15-advanced-patterns](15-advanced-patterns.md) | `const map = createRefMap<Txt>();` then `ref={map.label}` and `map.label()` |
| Ray/arrow between two nodes | [15-advanced-patterns](15-advanced-patterns.md) | `<Ray from={a.right} to={b.left} endArrow end={0} />` then `ray().end(1, 0.5)` |
| CubicBezier between two nodes | [15-advanced-patterns](15-advanced-patterns.md) | `p0={() => toLocal(from.absolutePosition())}` and `p3={() => toLocal(to.absolutePosition())}` |
| tween with a function (custom interpolation) | [15-advanced-patterns](15-advanced-patterns.md) | `yield* tween(2, value => { obj.x = map(0, 100, easeOutCubic(value)); });` |
| Reparent a node | [15-advanced-patterns](15-advanced-patterns.md) | `node.reparent(newParent)` |

---

## Import cheat sheet

| Symbol | From |
|--------|------|
| `makeScene2D` | `@motion-canvas/2d` |
| `makeProject` | `@motion-canvas/core` |
| `Circle`, `Rect`, `Layout`, `Line`, `Txt`, `Img`, `Path`, `Grid`, `Node`, `SVG`, `Gradient` | `@motion-canvas/2d` or `@motion-canvas/2d/lib/components` |
| `CodeBlock`, `edit`, `insert`, `lines`, `word` | `@motion-canvas/2d/lib/components/CodeBlock` |
| `Code` | `@motion-canvas/2d` |
| `all`, `chain`, `delay`, `loop`, `waitFor`, `waitUntil` | `@motion-canvas/core/lib/flow` or `@motion-canvas/core` |
| `cancel`, `join`, `spawn` | `@motion-canvas/core/lib/threading` or `@motion-canvas/core` |
| `createRef`, `makeRef`, `makeRefs`, `createRefMap`, `createRefArray`, `range` | `@motion-canvas/core/lib/utils` or `@motion-canvas/core` |
| `createSignal`, `createComputed` | `@motion-canvas/core/lib/signals` or `@motion-canvas/core` |
| `linear`, `easeOutCubic`, `easeInCubic`, `easeInOutCubic`, `easeOutElastic`, `map`, `remap` | `@motion-canvas/core/lib/tweening` or `@motion-canvas/core` |
| `slideTransition`, `zoomInTransition`, `zoomOutTransition` | `@motion-canvas/core/lib/transitions` or `@motion-canvas/core` |
| `Direction`, `Vector2`, `BBox`, `Spacing` | `@motion-canvas/core/lib/types` or `@motion-canvas/core` |
| `blur` | `@motion-canvas/2d` |
| `useScene`, `useDuration`, `useRandom`, `usePlayback` | `@motion-canvas/core/lib/utils` or `@motion-canvas/core` |
| `finishScene` | `@motion-canvas/core` |
| `tween` | `@motion-canvas/core` |
| `Ray`, `CubicBezier` | `@motion-canvas/2d/lib/components` |
