---
name: sickomet-light-infographic-style
description: "Use when building a light cream Sickomet promo."
version: 1.0.0
author: Hermes Agent
license: MIT
category: creative
metadata:
  hermes:
    tags: [video, motion-graphics, promo, persian, style, light, infographic, sickomet]
    related_skills: [sickomet-dark-glass-style, farsi-video-promos, mehdi-promo-mix-pattern]
---

# Sickomet light infographic promo

The light counterpart of the dark theme: cream paper background, pure-white floating cards, black Persian display type, one blue accent, a perspective floor grid, brand chip top-right and an RTL progress bar at the bottom. Flat, clean, infographic — **no footage, no faces, no glow-heavy neon**.

## When to Use

- A promo/explainer that must read as a **clean infographic**: pricing, comparison, "how it works" beats.
- The piece is a talking-free motion graphic (voiceover only) in **9:16**.
- Whenever the brief says "light", "white", "clean" or "Seedance-style" — as opposed to `sickomet-dark-glass-style`.

## Design tokens (measured off the reference frames, 720×1280)

| Token | Value | Where it came from |
| --- | --- | --- |
| Background | `#f5f3ef` cream | sampled (245,243,239) |
| Background edges | `#f2f0ea` | vignette darkens the corners (242,240,234) |
| Top glow | white radial, ~12 % | the upper third is washed lighter |
| Card | `#ffffff`, radius ~32 px @720, shadow `0 22px 55px rgba(0,0,0,0.10)` | the cards are pure white, never grey |
| Primary type | `#0a0a0a` (effectively black, sampled value 7) | titles and card headlines |
| Accent blue | `#1c82ed` | the blue bar sampled (28,130,237) |
| Accent blue (soft) | `#6a9be3` | badge fills render lighter through AA |
| Secondary dark | `#28272a` | the "market price" bar |
| Muted grey | `#545454` | brand text, small captions |
| Grid lines | `rgba(0,0,0,0.07)`, 1 px | perspective floor grid |
| Progress bar | height 5 px @720, black fill, track `rgba(0,0,0,0.10)` | bottom, margins ~56 px |

Type: a heavy Persian face (Vazirmatn Black/ExtraBold) at 96–120 px @1080, centred, max 2 lines; Latin words (e.g. `Seedance`) sit **inside the Persian line in the same weight and colour** — never a second font family, never italic.

## Layout bands (1080×1920)

- **Brand chip** — top-right, y ≈ 70: `@sickomet` in `#545454` (~30 px) then a **blue rounded-square icon** 44×44, radius 12, `#1c82ed`.
- **Caption** — grey `#545454`, ~44 px, centred, sits **above** its card (y ≈ 430 in the reference).
- **Headline** — black, y ≈ 440–560, centred, 2 lines max.
- **Card** — the hero element: occupies x 90–630, y 520–860, radius 32, pure white, big soft shadow. One card per beat.
- **Card interior** — caption/blue label at the card's top, the data/viz in the middle, labels at the card's foot.
- **Bottom strip** — progress bar at y ≈ 1238, x 56–664.
- Everything else stays **empty** — the emptiness is what makes it read as premium.

## Component recipes

**1. Minimal stat card** (the reference's "cost per video" beat)
```
<div class="card">
  <p class="c-cap">هزینهی هر ویدیو</p>
  <div class="c-icon"></div>          <!-- black disc, 46px, black ring 12px -->
  <p class="c-big">تومان</p>
</div>
```

**2. Comparison bar chart card**
- Two bars, equal width (~150 px), standing on the card's bottom inset; **left bar `#28272a`, right bar `#1c82ed` with a blue glow** (`box-shadow: 0 0 40px rgba(28,130,237,0.35)`).
- Labels **above** the bars (`قیمت بازار` black, `با ما` blue) and footers **below** (`بقیه` black, `Seedance` blue, bold).
- Three faint horizontal gridlines across the card behind the bars.

**3. Plan / offer card**
- Blue pill badge (white text, radius 999) at the card's top → big black headline (`پلن ویژه`) → a **dark chip** (`#1a1a1c`, radius 999) holding a blue dot + the Latin product name in white.

**4. Chrome**
- Progress bar fills **right-to-left** (RTL): `transform-origin: right center` and animate `scaleX`. Getting this backwards is the most obvious tell that the piece is not Persian-native.
- Optional brand top-right only on the first and last beat; keep it on all beats if the piece is a reel.

## Motion rules

- **Calm**: fades and 20–40 px rises over 0.5–0.7 s with `power3.out`; no blur filters on text or media.
- One element lead per beat: caption → headline → card → card interior, each offset 0.08–0.15 s.
- A **perspective floor grid** drifts very slowly (or static); it must never distract.
- Scene changes are **soft dissolves or gentle slides**, not hard cuts — the reference had exactly **one** scene change in 25.3 s.
- Bars/charts grow with `scaleY` from their base, once, on the beat.

## Build recipe (HyperFrames)
1. Scaffold (or reuse) a 1080×1920 project; fonts: Vazirmatn Black/Bold + one Latin heavy face.
2. Voiceover first, word-level timestamps; one card per sentence.
3. Background layer: cream + white top glow + the perspective grid (two repeating-linear-gradients inside a `perspective` wrapper, or a single SVG).
4. Cards as absolutely positioned white divs; never tint them.
5. Chrome last (brand chip, progress bar with RTL fill).
6. `npx --yes hyperframes@0.8.113 check` then `render`.

## Verification (run these on the RENDERED file, not the composition)
- Background reads cream, not white: `ffmpeg -ss <t> -i out.mp4 -frames:v 1 -vf "crop=8:8:20:300,scale=1:1" -f rawvideo -pix_fmt rgb24 -` → expect ≈ `245,243,239`.
- Card interior is pure white (≈255,255,255) **and** the area around it is not (proves the card is a card, not a full-bleed panel).
- Headline is black: darkest pixel in the headline band < 40.
- Progress fill direction: sample the bar at 25 % and 75 % of the timeline — the bar's filled end must grow **leftwards**.
- No frame may go near-black (mean luma > 120 across the whole piece) — that would mean a dark-style layer leaked in.

## Pitfalls
- **Overlays must be timed clips.** A layer parked inside an untimed wrapper stays visible for the whole composition and stacks with the other scenes' layers — this halved the luminance in a past build. Give every overlay its own `data-start`/`data-duration`.
- **Never put a CSS `filter` on a `<video>` element** in this pipeline: the frame renders at roughly half luminance. Grade with overlay layers instead.
- Do not tint the cards or add gradients inside them; the style's identity is flat pure white on cream.
- Keep the type inside the middle band; leave the top ~25 % and the bottom ~15 % empty apart from chrome.
- If footage is ever added to this style, it belongs **inside a card**, not full-bleed — full-bleed footage turns it into a different style.

## Related
- `sickomet-dark-glass-style` — the dark sibling (black glass panels, silver type, orange accent).
- `farsi-video-promos` — the pipeline: VO, procedural music bed, render, Telegram delivery.
