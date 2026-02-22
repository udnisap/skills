---
name: cli
description: Using npx remotion CLI to capture stills, render video segments, list compositions, and inspect state
metadata:
  tags: cli, still, render, compositions, screenshot, debugging
---

## When to use

Load this rule when you need to get a screenshot at a frame, render a video (full or segment), list compositions, or discover composition metadata via the CLI. Use it to run commands autonomously and return output file paths to the user.

## Commands

### Screenshot at frame

`npx remotion still [entry-point]? <composition-id> [output-location]`

- **`--frame N`**: Frame to render (default `0`). Use `-1` for the last frame.
- **`--output <path>`**: Output path (alternative to positional output-location).
- **`--image-format`**: `png`, `jpeg`, `webp`, or `pdf` (default `png`).

The command writes the image file. Return the **resolved output path** (absolute or relative as appropriate) to the user.

### Render video

`npx remotion render [entry-point]? <composition-id> <output-location>`

- **`--frames <range>`**: Render a subset. Examples: `0-9` (first 10), `100-` (from frame 100 to end), `-100` (last 100 frames).
- **`--output <path>`**: Output path (alternative to positional).
- **`--codec`**: e.g. `h264`, `h265`, `mp3`. Default H.264.
- **`--muted`**: Disable audio.

For a **time range** (t1→t2 in seconds): the CLI uses frames. Convert with `frame = timeInSeconds * fps` (get fps from `npx remotion compositions` or project config), then use `--frames startFrame-endFrame`.

The command writes the media file. Return the **output path** to the user.

### List compositions

`npx remotion compositions [entry-point]?`

- Default: prints composition IDs and metadata (FPS, width, height, duration).
- **`--quiet`** / **`-q`**: Only space-separated composition IDs (for scripting).
- **`--props <path>`**: JSON file path for props; use when composition uses `calculateMetadata()` so metadata is resolved correctly.

Use this to get composition IDs and metadata before calling `still` or `render`.

### Other

- **`npx remotion help`**: List available CLI commands.
- **`--props <path-to-json>`**: Pass input props (prefer file path in automation). Use with `still`, `render`, or `compositions`.
- Entry-point (or serve URL) is an optional first argument; if omitted, Remotion determines the entry point.
- If output location is omitted, stills and renders go to the `out/` folder.

---

## Examples

Run or adapt these when the user asks for a screenshot, video segment, or composition list.

### Screenshot at a given frame

Frame 42 of composition `MyComp`, save to a file and return the path:

```bash
npx remotion still src/root.tsx MyComp out/frame-42.png --frame 42
```

Last frame of the composition:

```bash
npx remotion still src/root.tsx MyComp out/last-frame.png --frame -1
```

Return the written path (e.g. `out/frame-42.png` or the absolute path) to the user.

### Render full composition

```bash
npx remotion render src/root.tsx MyComp out/mycomp.mp4
```

Return the output path.

### Render segment by frame range

Frames 10–50 of `MyComp`:

```bash
npx remotion render src/root.tsx MyComp out/segment.mp4 --frames 10-50
```

Return the output path.

### Render segment by time range

Example: 5s to 10s at 30 fps. Frames: `5*30 = 150`, `10*30 = 300`.

```bash
npx remotion render src/root.tsx MyComp out/segment.mp4 --frames 150-300
```

Get FPS from `npx remotion compositions` output or from the project config. Return the output path.

### List compositions

Get IDs and metadata (FPS, dimensions, duration) before still/render:

```bash
npx remotion compositions src/root.tsx
```

IDs only (e.g. for scripting or loops):

```bash
npx remotion compositions src/root.tsx --quiet
```

---

## Debugging and state inspection

Use these to discover composition state or diagnose issues autonomously.

| Goal | Command |
|------|---------|
| List compositions and metadata | `npx remotion compositions [entry-point]?` |
| Resolve metadata when it depends on props | `npx remotion compositions [entry-point]? --props path/to/props.json` |
| Composition IDs only (scripting) | `npx remotion compositions [entry-point]? --quiet` |
| Verbose logs (timeout, bundle issues) | Add `--log=verbose` to `compositions`, `still`, or `render` |
| Validate Remotion package versions | `npx remotion versions` |
| Chrome GPU usage (render/headless issues) | `npx remotion gpu` |
| Measure render performance | `npx remotion benchmark [entry-point]? <composition-id>` |
| Create repro ZIP for bug reports | `npx remotion render ... --repro` |
