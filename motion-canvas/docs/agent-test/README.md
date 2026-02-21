# Motion Canvas docs-only agent test

Run a constrained test: an agent may use **only** the `/docs/` documentation and a video description to recreate a Motion Canvas scene. No access to `repos/examples/examples` source.

---

## Interface test (simple)

1. **Enable the rule**  
   In Cursor, enable `motion-canvas-docs-test-agent`.

2. **Run the recreate**  
   Prompt:
   > Recreate the video described in `docs/test-video-interface.md`.  
   > Write the scene to `repos/examples/examples/docs-agent-test/src/scenes/recreate-interface.tsx`.  
   > Use only the documentation under `docs/` and `docs/agent-quickref.md`; do not read `repos/examples/examples` (except `docs-agent-test`).

3. **Serve and compare**
   - **Original:** `npm run motion-canvas` (or `npm run serve -w examples/motion-canvas`) and open the **interface** scene. Run from `repos/examples/` (skill root: `motion-canvas/repos/examples/`).
   - **Recreated:** `npm run docs-agent-test` from the `repos/examples/` folder, or `npm run serve -w examples/docs-agent-test`, or `npm run serve` from `repos/examples/examples/docs-agent-test`.

4. **Check**  
   Same sequence: slide from bottom → text to "USER INTERFACE" (1s, linear) → hold until "next". Same look: JetBrains Mono, 120, `rgba(255,255,255,0.6)`.

---

## Complex test (Signals Act 1)

1. **Enable the rule**  
   Same as above.

2. **Run the recreate**  
   Prompt:
   > Recreate the video described in `docs/test-video-signals-act1.md`.  
   > Write the scene to `repos/examples/examples/docs-agent-test/src/scenes/recreate-signals-act1.tsx`.  
   > Use only `docs/` and `docs/agent-quickref.md`; do not read `repos/examples/examples` (except `docs-agent-test`).

3. **Serve and compare**
   - **Original:** `motion-canvas` project, **signals** scene (first act only: until "next" and everything moves up).
   - **Recreated:** `docs-agent-test` project (e.g. `npm run docs-agent-test` from `repos/examples/`), then pick **recreate-signals-act1** in the Motion Canvas UI.

4. **Check**  
   Title "SIGNALS", ~16 circles, repeating lines that draw/undraw and highlight targets, main line and target fade after ~1s, then on "next" all groups move up and the loop stops.
