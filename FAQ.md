# FAQ (engineers)

Short answers for common screening questions.

## Is it deterministic? Any AI/ML in this plugin?

Fully deterministic. **No AI/ML** at runtime. The engine uses spatial algorithms and heuristics — cluster scaling, semantic layout, and the Remember template system all run without any machine learning.

## Does it rely on layer names to classify elements?

**No.** Classification relies on spatial and visual properties of each node — never on layer names. Names are stored as metadata for UI display but are **never compared, filtered, or matched** in any algorithm path.

## How do you handle text reliably in Figma (mixed styles, font loading)?

Before any mutations, the engine pre-loads all required fonts (`figma.loadFontAsync()`), including those inside INSTANCE children.

For text scaling:
- font size is scaled conservatively to avoid illegible results under non-uniform transforms
- `figma.mixed` is handled per-character/range (range font size read/set)
- if a font fails to load, it falls back to a safe default and applies the scaled size
- minimum readable font sizes enforced per semantic slot type

## What is the Remember system and how does it work?

**Remember** saves a per-format master template — a snapshot of the banner's layout.

**Workflow:**
1. Build a reference banner at **16:9** → hit **Remember**
2. Build another at **9:16** → hit **Remember** — now you have two format masters
3. Select any banner with the same slot structure → pick target format → **Scale**
4. Engine matches layers by semantic type and applies the master's layout

After scaling, the active temp **rebinds to the output** — you can chain: output → new W×H → Scale → next output.

## How does cross-master matching work across different aspect ratios?

Multiple matching strategies activate depending on how different the source and target aspect ratios are. The engine selects the most reliable pairing approach for each element type at each level of aspect divergence. Details available in a live screen-share.

## What about auto-layout, constraints, and instances?

- Constraints frozen before processing
- Auto-layout intentionally disabled — output uses absolute positioning
- Instance children are **walked** for slot detection and Remember capture
- Only the instance container is resized — Figma handles internal scaling

## What's the difference between strict and cross mode?

**Strict (saved layout):** the selected frame is the same one Remember was run on. Slots applied directly — the engine knows which element is which.

**Cross (master layout):** different frame than the remembered template. Slots matched by **semantic type**. More flexible but depends on both frames having compatible slot structures.

## Where does the computation run?

Everything runs inside the **Figma plugin sandbox** using the Figma Plugin API. No external servers, no offline compute, no network calls at runtime.

## What are the biggest risks / honest limitations?

- **Heuristic semantic detection** can misclassify unusual layouts (mitigated by Remember — explicit slot map overrides heuristics).
- **Auto-layout disabled** during processing (absolute positioning output).
- **Instance internals** are read-only (Figma API constraint).
- **Cross-master matching** degrades gracefully but can mismatch when slot counts differ significantly.
- **Complex decorative backgrounds across aspect ratios:**
  - When master and target have very different aspect ratios (e.g. 16:9 → 9:16), complex background compositions may not transfer correctly
  - This is a fundamental design problem — no single algorithmically "correct" way to remap a composition built for one canvas shape onto a different one
  - **Intended workflow:** Remember a dedicated master for each aspect ratio family, where the designer has placed the background for that format
  - Cross-master reliably handles **content** (text, buttons, logos) across any aspect change — the background is the part that benefits from per-format masters

## Recommended next steps

1. Watch the demo / request a live screen-share with your edge cases.
2. For deeper technical discussion: [reach out](mailto:kurokie1337@proton.me).
