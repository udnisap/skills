# Test video: Layouts

**Purely behavioral** (no code, no API names, no file paths). Use this to recreate the scene using only the Motion Canvas docs.

---

## Scene

- A **grid of 8 rectangles** in 3 rows:
  - Row 1: three cells
  - Row 2: three cells
  - Row 3: two cells
- Rounded corners (~8px), thin stroke (~8). One rectangle (center of the second row) has **green** stroke (`#99C47A`); the others **dark** (`#242424`).
- A **title**: the string `"LAYOUTS"`, same style as Interface (JetBrains Mono, 120, `rgba(255,255,255,0.6)`).

---

## Animation sequence

1. **Entry:** Slide from the **bottom** over **1 second**.

2. **Main animation (2 seconds):**
   - The title **animates to `"LAYOUTS"`** over 2 seconds.
   - The **proportions of the rectangles change** over 2 seconds: some cells shrink, some grow. The layout is driven by an animated value that goes from 0 to 1 over 2s. The grid starts in one configuration and ends in another.

3. **Then:** Wait for moment **`"next"`**, then **allow transition out** and animate the **title up by ~320px** over 1 second.
