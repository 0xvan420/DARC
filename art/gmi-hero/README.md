# GMI Cloud — Hero Redesign

Single-file hero redesign for `gmicloud.ai/en`, driven directly by the hero copy.

## Source copy (verbatim from the request)

> **General Machine Intelligence**
> An AI-native inference cloud built for production AI, combining serverless scaling and dedicated GPU infrastructure with predictable performance and cost.

The original headline rendered as `General MachineMachine IntelligenceIntelligence` — that visible duplication is treated here as a deliberate **type-echo** design language, not a typo.

## Concept

**"Compute Lattice"** — three layers, each tied to a specific phrase in the copy.

| Layer | What you see | Phrase it serves |
|---|---|---|
| Background canvas | A jittered hex lattice of GPU nodes; inference particles flow in from the edges, get captured, emit warm pulses, then dim and recycle | *"AI-native inference cloud" · "dedicated GPU infrastructure"* |
| Headline echo | Each duplicated word ("Machine", "Intelligence") rendered with a chromatic-split echo (cyan + magenta translucent ghosts that breathe slowly) | *"General Machine Intelligence"* — the doubled words become the brand signature |
| Stats strip + clamps | Four small KPIs anchored under the CTAs; speed/life clamps in the canvas keep throughput visually steady regardless of seed | *"predictable performance and cost"* |

## Why this and not the previous Lattice Flux artwork

The previous `art/lattice-flux/` piece is **gallery-style generative art** — full-bleed, freeform, high contrast, owns the frame. A hero needs the opposite: the **copy is the protagonist**, the visual is a low-contrast bed that holds it. So this version:

- Drops saturation hard (deep blue-black bg, ~50% alpha trails)
- Adds a radial vignette focused on the reading area
- Slows particle motion (~50% the speed of the gallery version)
- Pauses on `visibilitychange`, respects `prefers-reduced-motion`
- Is a single self-contained HTML file (no p5 dep — vanilla canvas, ~60fps, DPR-aware)

## Files

- `hero.html` — the hero, drop into a browser and view full-screen
- `README.md` — this file

## Notes on the design

- **Type**: Space Grotesk for the display word (geometric, slightly technical), Inter for body — both via Google Fonts CDN
- **Palette**: ink `#ecf1f8`, bg `#07090f`, accent `#7cf0ff` (cyan), `#b388ff` (magenta), `#ff8a5b` (warm pulse). Replace these CSS vars to match GMI's actual brand if it differs
- **CTAs**: solid "Get started" + ghost "Talk to sales" — typical B2B AI-infra pattern
- **Stats**: placeholder values (P50 latency, GPU types, autoscale, SLA) — **swap with real numbers** before shipping
- **Nav**: minimal placeholder — adapt to the real GMI IA

## What I didn't have access to

WebFetch and outbound HTTP to `gmicloud.ai` are blocked from this sandbox, so I couldn't verify the live site's exact:
- Brand color tokens
- Real CTA labels and nav structure
- Current stats/social-proof numbers
- Whether the headline has a tagline above it ("eyebrow")

Everything in `hero.html` is a reasoned interpretation from the copy you pasted. If you share screenshots or the real palette/IA, I'll iterate.
