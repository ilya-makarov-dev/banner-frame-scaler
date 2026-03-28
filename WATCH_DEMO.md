# Banner Frame Scaler — Demo Guide

Six short videos showing the engine on real production banners. Each video is self-contained — watch any one to see a specific capability.

<p align="center">
  <a href="https://youtu.be/JCN9pqSKNCM"><img src="./assets/thumb-main.png" width="720" alt="▶ Watch full demo on YouTube" /></a>
  <br>
  <a href="https://youtu.be/JCN9pqSKNCM"><sub><b>▶ Full walkthrough on YouTube</b> (~3 min) — all six cases back-to-back</sub></a>
</p>

No voiceover — text labels on screen indicate source/target sizes. Descriptions below explain what's happening in each case.

---

## 1) Master banner — core case

<p align="center">
  <a href="https://youtu.be/-D247wvEzm4"><img src="./assets/thumb-1.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/-D247wvEzm4"><sub><b>▶ Watch on YouTube</b> · 46 sec</sub></a>
</p>

**What to look for:**
- Two reference banners: **16:9** (1920×1080) and **9:16** (1080×1920)
- Each gets **Remember** — the plugin saves the layout structure for every element
- A different banner is selected → target size chosen → **Scale (saved layout)**
- The output matches the master's composition: logo in header, CTA at bottom, disclaimer and age rating in correct slots
- Then the same flow in reverse: 9:16 → 16:9

This is the flagship workflow — one master per format, apply to any banner with similar structure.

---

## 2) Unusual template support

<p align="center">
  <a href="https://youtu.be/aYBxoKWKi5s"><img src="./assets/thumb-2.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/aYBxoKWKi5s"><sub><b>▶ Watch on YouTube</b> · 38 sec</sub></a>
</p>

**What to look for:**
- A non-standard template at 1400×1230 (neither 16:9 nor 9:16 — unusual dimensions)
- A completely different design (forest/tree creative) with atypical layer nesting
- The engine runs cross-master layout using the existing 16:9 and 9:16 masters
- Slots are matched by semantic type (title, logo, button) despite the completely different aspect ratio and layer structure

Shows the engine is not hardcoded to standard banner formats.

---

## 3) Edge cases — complex aspect ratios

<p align="center">
  <a href="https://youtu.be/OLFq4mTBKjE"><img src="./assets/thumb-3.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/OLFq4mTBKjE"><sub><b>▶ Watch on YouTube</b> · 25 sec</sub></a>
</p>

**What to look for:**
- Ultra-wide banner (1920×430) resized to near-square (400×430)
- This is an extreme aspect ratio change — almost no scaling tool handles this well
- The engine rearranges content into the new shape using Remember layout

**Known issue (visible in video):** the CTA button renders as a black bar on the resized output. This is an honest edge case — included intentionally to show where the current limits are. Being tracked and tuned.

---

## 4) Cluster scaling — portrait (9:16)

<p align="center">
  <a href="https://youtu.be/gkj9jYPyJOY"><img src="./assets/thumb-4.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/gkj9jYPyJOY"><sub><b>▶ Watch on YouTube</b> · 33 sec</sub></a>
</p>

**What to look for:**
- 9:16 banner (1080×1920) resized to smaller portrait (500×889), then back to full size
- Pure cluster scaling — no Remember, no layout guide
- Background fills the target frame, content stays proportional, text remains readable
- Two resize steps from the same source: shows the engine is idempotent

---

## 5) Cluster scaling — landscape (16:9) → multi-format

<p align="center">
  <a href="https://youtu.be/USS-ExfiXm8"><img src="./assets/thumb-5.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/USS-ExfiXm8"><sub><b>▶ Watch on YouTube</b> · 46 sec</sub></a>
</p>

**What to look for:**
- 16:9 banner (1920×1080) resized to multiple targets in sequence: another 16:9, then 1:1 (1080×1080), then 9:16 (1080×1920)
- All without Remember or layout guide — just the base cluster scaling engine
- Consistency across orientations: content reflows correctly for each shape

---

## 6) Vector illustration example

<p align="center">
  <a href="https://youtu.be/wA1rhzN6Brs"><img src="./assets/thumb-6.png" width="720" alt="▶ Watch on YouTube" /></a>
  <br><a href="https://youtu.be/wA1rhzN6Brs"><sub><b>▶ Watch on YouTube</b> · 44 sec</sub></a>
</p>

**What to look for:**
- A pure vector layout: no photos, no raster images — only paths and shapes
- Resized from landscape to 1:1, then to portrait, and back
- Shapes scale cleanly, paths stay sharp, no raster artifacts

**Expected behavior note:** at extreme aspect changes (wide → tall), vector illustrations appear small with empty space around them. This is correct — the engine preserves proportions for a layout designed for a specific shape. In production, a **per-format master** (Remember on a designer-composed vertical version) would fill the frame properly.

---

## Technical context

- All videos recorded on the same build of the plugin
- No post-editing of Figma output — what you see is the raw engine result
- Each case uses real production banner designs (Kerastase) and a community vector illustration set
- Videos are screen recordings of the actual Figma canvas with the plugin panel visible

For technical details: [README.md](./README.md) · [FAQ.md](./FAQ.md)
