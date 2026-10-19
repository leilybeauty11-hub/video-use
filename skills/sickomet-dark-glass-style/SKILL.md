---
name: sickomet-dark-glass-style
description: "Use when building a dark Sickomet glass-panel promo."
version: 1.0.0
author: Hermes Agent
license: MIT
category: creative
metadata:
  hermes:
    tags: [video, motion-graphics, promo, persian, style, dark, glass, sickomet]
    related_skills: [sickomet-light-infographic-style, farsi-video-promos]
---

# Sickomet dark glass promo

The dark sibling of the light infographic style: near-black paper, **warm dark-glass panels**, silver metallic Persian type, a single orange accent, a perspective grid, brand chip top-right and a thin progress bar at the bottom. Calm, minimal, premium — **no footage, no faces, no neon.**

## When to Use

- A talking-free 9:16 motion graphic whose brief says "dark", "premium", "glass" or "Claude-orange".
- Feature/benefit beats shown as a fake app UI (a card listing a feature, a video row, a settings panel).
- Whenever the light version would feel too plain but the neon style would be too loud.

## Design tokens (measured off the reference frames, 1080×1920)

| Token | Value | Evidence |
| --- | --- | --- |
| Background | `#050508` top → `#101116` bottom | sampled (5,5,8) and (16,17,22) |
| Warm bloom | radial `rgba(217,119,87,0.10)` behind the headline | the glow reads (49,42,43) — orange at very low alpha |
| Type (primary) | metallic silver: `linear-gradient(#ffffff, #a7acb8)` with `background-clip: text` | the headline's brightest pixel is 254, its body sits near 168 |
| Type (secondary caption) | `#ffffff` at ~0.92 opacity, one line, below the panel | sampled max 228 |
| Accent orange | `#d97757` | the brand dot samples (196,106,78) through its own glow |
| Glass panel | background `rgba(46,41,42,0.55)`, 1px border `rgba(255,255,255,0.10)`, radius ~44 px @1080, inner shadow | panel interior samples (46,41,42) — warm, never neutral grey |
| Panel sub-surface | `#232126`, radius 24 | the darker square holding the play button |
| Skeleton bars | orange at 55 % and grey at 22 % opacity, radius 999 | the fake content inside panels |
| Grid | perspective floor grid, lines `rgba(255,255,255,0.06)`, 1 px | barely visible, converges toward the lower centre |
| Progress bar | height 4 px @1080, track `rgba(255,255,255,0.10)`, fill orange with a **bright head** | bottom, margins ~56 px |

Type: heavy Persian (Vazirmatn Black) 96–130 px @1080, centred, **max 2 lines**, silver gradient fill; a Latin product name appears inside the Persian line, same size and weight, with the **first Latin letter in orange** when the name is the point of the beat.

## Layout bands (1080×1920)

- **Brand chip** — top-right, y ≈ 90: orange dot 30 px with a soft glow, then `@sickomet` in silver (~30 px).
- **Headline** — y ≈ 580–760, centred, silver 2 lines max, sitting on the warm bloom.
- **Glass panel** — the hero: x 100–620, y 860–1180, radius 44. One panel per beat; it holds the mock UI.
- **Caption** — white ~44 px, centred, **below** the panel (y ≈ 1240).
- **Bottom strip** — thin progress bar at y ≈ 1836.
- Keep the top ~25 % nearly empty; the black space is the style.

## Component recipes

**1. Feature panel** (the reference's "app-builder" row)
```
<div class="panel">
  <div class="p-head"><span class="pill">رایگان</span><span class="lat">app-builder</span><span class="dots">•••</span></div>
  <div class="skeleton"></div>   <!-- two rounded bars, low contrast -->
</div>
```
- Filter to keep the contrast low: the panel must never compete with the headline.

**2. Video row panel**
- Left: two orange skeleton bars (title + subtitle). Right: a `#232126` rounded square with a **white ring + small triangle** (a play button). Nothing else.

**3. Chrome**
- Progress bar: track faint white, fill orange that **brightens at its head**; fill direction follows the language (RTL for Persian).
- Brand chip only where it does not fight the headline.

## Motion rules

- **Extremely calm.** The reference had **zero cuts** in 25.5 s and in-scene motion between 0.1 and 5 (of 255) — everything is slow fades and 20–40 px drifts.
- Panels arrive with a soft rise + fade (0.6–0.8 s, `power3.out`), then their skeleton bars fade in 0.15 s later.
- The bloom behind the headline breathes on `sine.inOut`, never flashes.
- No blur filters on type or media (also breaks the render — see Pitfalls).

## Build recipe (HyperFrames)
1. 1080×1920 project; fonts Vazirmatn Black/Bold + one Latin heavy face.
2. Background: near-black gradient + warm bloom + the perspective grid (an SVG or two repeating-linear-gradients inside a `perspective` wrapper).
3. Voiceover first, word-level timestamps; one panel per sentence.
4. Panels as absolutely positioned divs; type with `background-clip: text` for the silver look.
5. Chrome last; then `npx --yes hyperframes@0.8.113 check` and `render`.

## Verification (run on the RENDERED file)
- Background is near-black, not grey: sample (60,260) → expect ≈ `5,5,8`; sample the bottom → ≈ `16,17,22`.
- Type is bright but not pure white everywhere: max in the headline band ≈ 250+, mean body lower (proves the silver gradient rendered, not flat white).
- The tagline **behind-nothing** black space: no frame between beats may be brighter than ~60 mean luma.
- Orange accent present in every chrome sample (brand dot / progress fill) — dark red, never pure `#ff0000`.
- Panel interior stays warm (`r > g > b`), never neutral grey.

## Pitfalls
- **Overlays must be timed clips.** A layer parked inside an untimed wrapper stays visible for the whole composition and stacks with the other scenes' layers — in a past build six stacked dark layers crushed the picture to near-black while the code looked correct. Give every overlay its own `data-start`/`data-duration`.
- **Never put a CSS `filter` on a `<video>` element** in this pipeline: filtered video renders at about half luminance (measured 21 vs 64 on the same frame). Use overlay layers, and `transform` for any scale kick.
- Do not add neon glows or saturated colours: the accent is one muted orange and the type is silver. Neon is a *different* style.
- Do not let a panel fill the frame edge-to-edge; it must float inside the black margins.
- If a caption and a panel headline both exist, the caption is white and smaller, the panel text stays silver/grey.

## Related
- `sickomet-light-infographic-style` — the cream/white sibling (blue accent).
- `farsi-video-promos` — pipeline: VO, procedural music bed, render, Telegram delivery.
