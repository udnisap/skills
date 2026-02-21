# 12 – Three.js and 3D

**When to use:** You need to render a Three.js (or raw WebGL) scene into a Motion Canvas 2D node, or use a 2D-projected 3D object (e.g. Tetrahedron). The examples use a custom `Three` component that draws `renderer.domElement` into the 2D canvas.

---

## Import map

- Custom **Three** component (see examples): extends `Layout`, holds `WebGLRenderer`, `Scene`, `Camera`. Override `draw()`: `renderer.render(scene, camera)` then `context.drawImage(renderer.domElement, ...)`.
- `Tetrahedron`: custom node in examples that projects 3D vertices to 2D; has `orbit`, `radius`, `vertices()`, `projectedVertices()`.
- `* as THREE` or `THREE` from `three`
- `tween` from `@motion-canvas/core` when you drive Three objects over time

---

## Concepts

- **Three (custom)**: in `draw()`, run `this.onRender(renderer, scene, camera)` (default: `renderer.render(scene, camera)`), then draw `renderer.domElement` into the 2D context. Call **rerender()** whenever Three state (mesh position, etc.) changes so the next frame uses new state.
- **Driving Three from a tween**: update `mesh.position`, `mesh.rotation`, etc. inside `tween(duration, value => { ... })` or in a `loop`; then `scene.updateWorldMatrix(true, true)` and `three().rerender()`.
- **Tetrahedron**: 2D node that draws a rotating 3D tetrahedron; `orbit`, `radius`, `stroke`, `lineWidth`. Use `vertices()`, `projectedVertices()` to sync Lines/Circles to 3D points.

---

## Snippets

**Custom Three: draw() and rerender**

```ts
// In a Layout subclass:
protected override draw(context: CanvasRenderingContext2D) {
  const { width, height } = this.computedSize();
  this.rerender();
  const scene = this.scene();
  const camera = this.camera();
  const renderer = this.configuredRenderer();
  if (width > 0 && height > 0) {
    this.onRender(renderer, scene, camera);
    context.imageSmoothingEnabled = false;
    context.drawImage(
      renderer.domElement, 0, 0, quality * width, quality * height,
      width / -2, height / -2, width, height,
    );
  }
  super.draw(context);
}
// After changing Three state:
three().rerender();
```

**Tween Three mesh and rerender**

```ts
yield* tween(2, value => {
  gameThree.mesh.position.set(0, 0, map(0, 3, easeInOutCubic(value)));
  gameThree.threeScene.updateWorldMatrix(true, true);
  three().rerender();
});
```

**Loop that rotates mesh and rerenders**

```ts
yield loop(() =>
  tween(8, value => {
    gameThree.mesh.rotation.set(0, 0, value * Math.PI * 2);
    gameThree.threeScene.updateWorldMatrix(true, true);
    three().rerender();
  }),
);
```

**Tetrahedron (2D-projected 3D)**

```ts
<Tetrahedron
  ref={tetra}
  lineWidth={8}
  stroke={theme.stroke}
  radius={2}
  orbit={-90}
/>
// Sync a Line to face:
tetra().add(
  <Line
    points={() => [
      tetra().projectedVertices()[0],
      tetra().projectedVertices()[1],
      tetra().projectedVertices()[3],
      tetra().projectedVertices()[0],
    ]}
    stroke={theme.main}
  />
);
```

---

## Example scenes

- `repos/examples/examples/asset-code/src/nodes/Three.ts` (custom Three component)
- `repos/examples/examples/asset-code/src/scenes/editor.tsx` (Three, Tetrahedron, tween + rerender)
- `repos/examples/examples/asset-code/src/scenes/mesh.tsx` (Tetrahedron, vertices, projectedVertices)
- `repos/examples/examples/asset-code/src/three/game.ts` (THREE.Scene, mesh, geometry)
- `repos/examples/examples/deferred-lighting/src/three/` (createLight, createShadow, layers, level, normals, shadows)

---

## See also

- [04-2d-components](04-2d-components.md) – Layout, Node
- [08-transitions-and-easing](08-transitions-and-easing.md) – map, easeInOutCubic
- [15-advanced-patterns](15-advanced-patterns.md) – tween with function
- [agent-quickref](agent-quickref.md) – "run Three.js / WebGL in the scene"
