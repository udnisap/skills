# Test video: Signals Act 1 (complex)

**Purely behavioral** (no code, no API names, no file paths). Use this to recreate the scene using only the Motion Canvas docs.

---

## Scene

- A **title** in a dark rounded Rect: the string `"SIGNALS"`. Same style as Interface: JetBrains Mono, 120, `rgba(255,255,255,0.6)`.
- About **16 circles** at fixed positions distributed across the canvas. Size ~20. Dark fill `#242424`, initially opacity 0. One circle is highlighted (blue `#68ABDF`, opacity 1).

---

## Animation sequence

1. **Title:** The title **animates to `"SIGNALS"`** over **1 second**, **linear**.

2. **Repeating network animation (infinite until "next"):**
   - From the **currently highlighted circle**, draw **2–4 lines** to other circles. The **first line** is blue (`#68ABDF`); the others dark (`#242424`). Lines have round caps, ~8pt thickness, initially not drawn (`end` 0).
   - **Draw** each line: `end` 0→1. When a line reaches a target circle, that circle highlights (blue, opacity 1). **Speed** of each line scales with the distance between start and target (e.g. distance / 1500).
   - For the **non‑main** lines: after drawing, **undraw** (`start` 0→1). For the **main** (first) line: when it reaches its target, that target highlights; after about **1 second** the target and the main line **fade** (target back to dark, line opacity 0).
   - The **next** iteration starts from that former target. Repeat until "next".

3. **On "next":** The **label block** (Rect with title), the **line group**, and the **circle group** all **move up** off the top of the screen (e.g. y to about -1080 or -1400) over **1 second**. The repeating animation **stops** (cancel the loop and wait for it to finish).
