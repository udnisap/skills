# Test video: Interface

**Purely behavioral** (no code, no API names, no file paths). Use this to recreate the scene using only the Motion Canvas docs.

---

## Scene

- One **text element**, nothing else.
- Font: monospace (e.g. JetBrains Mono). Size: about 120px, line height 120.
- Color: light gray/white at 60% opacity, e.g. `rgba(255,255,255,0.6)`.
- **Initial:** Text is empty (invisible).

---

## Animation sequence

1. **Entry:** The whole scene enters with a **slide from the bottom** over **1 second**.

2. **Text:** The text **animates to the string `"USER INTERFACE"`** over **1 second**, **linear** timing.

3. **Hold:** The scene then **waits until a moment named `"next"`**. No further on-screen change; this moment is used for editing/voiceover.
