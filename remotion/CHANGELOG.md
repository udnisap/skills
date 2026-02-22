# Changelog – skill/remotion

This skill wraps best practices and rules for [Remotion](https://github.com/remotion-dev/remotion) (video creation in React). The upstream project and docs live in the original repo.

**Original repo:** [remotion-dev/remotion](https://github.com/remotion-dev/remotion)

**Reference (original repo):**

| Ref   | Git hash (short) | Date (UTC) |
|-------|------------------|------------|
| main  | `a1e929b`        | 2026-02-22 |

Full commit: [a1e929b55f1404c46ba2a24eb05cc1de1eb7074c](https://github.com/remotion-dev/remotion/commit/a1e929b55f1404c46ba2a24eb05cc1de1eb7074c).

---

## Changes in this skill

### Added

- **CLI rule** ([rules/cli.md](rules/cli.md)) – How the agent can use `npx remotion` to:
  - Capture a screenshot at a given frame (`npx remotion still`) and return the output file path
  - Render a full composition or a segment by frame range or time range (`npx remotion render` with `--frames`) and return the output path
  - List compositions and metadata (`npx remotion compositions`), including `--quiet` for IDs only and `--props` for metadata that depends on props
  - Run concrete examples (still at frame, render by frames, render by time) and report paths
  - Use debugging/state-inspection commands: `npx remotion versions`, `npx remotion gpu`, `npx remotion benchmark`, `--log=verbose`, `--repro` on render

- **SKILL.md updates:**
  - New rule link in "How to use": [rules/cli.md](rules/cli.md) for CLI usage (still, render, compositions; output paths)
  - Note in "How to use": when to capture a still, render a video segment, or list compositions via the CLI, load the CLI rule
