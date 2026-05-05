# GMI Cloud — Hero Redesign (v2, brand-accurate)

Single-file hero redesign for `gmicloud.ai/en`, calibrated against the actual
live hero (after seeing a screenshot).

## What stays the same as the live hero

These signals are working well — the redesign keeps them as-is:

- **Pure black background**, lime accent (`#d4f541`), white ink
- **GMI acronym hidden in the headline**: the first letters of **G**eneral / **M**achine / **I**ntelligence are lime — they spell GMI. This is excellent and stays
- **Slice glitch typography** on the headline
- **"Powered by NVIDIA" eyebrow** with the Preferred Partner badge
- **3D wireframe lattice + "+" sparks** as the right-side visual
- **Mono display type** (JetBrains Mono stand-in for the live custom face)
- CTAs: `START IN CONSOLE ↗` (lime) + `CONTACT SALES` (outline)
- Nav: Models / GPUs / Customers / Pricing / Company · English · LOGIN · CONTACT SALES

## What this version improves

Two specific upgrades, both motivated directly by the hero copy:

### 1. The glitch becomes an *inference pass*
The live hero's glitch is static — the letters look broken-once and stay that
way. Here the slice mask animates on a slow ~9.5s loop: the text sits clean
most of the time, then gets briefly "re-decoded" by a sliding scanline before
resolving. It's subliminal — never flashy, never illegible — but it ties the
typography to the verb in the copy: *inference*. The text doesn't just say
"machine intelligence"; it visibly behaves like a model run.

The animation is a CSS-only effect (two stacked `::before` / `::after` copies
with `repeating-linear-gradient` masks and `mix-blend-mode: difference`),
zero JS. Respects `prefers-reduced-motion`.

### 2. The lattice is alive
The live hero's right-side wireframe is a static screenshot of a 3D lattice
with stationary "+" sparkles. Here it's a real-time canvas:

- A **4 × 3 × 4 lattice of GPU nodes** (small wireframe cubes), slowly rotating
- **Token particles continuously traverse the edges** between nodes; the edge
  they're on heats up to lime, then cools back to dim white as they leave
- When a particle reaches a node, the node **flashes lime and emits a 5-spark
  starburst of "+"** marks — the original sparkles, but caused by something
- Ambient "+" dust still surrounds the structure (depth-sorted: faded behind,
  bright in front), so the still-frame impression is preserved

Every visual element now corresponds to a phrase in the copy:

| Phrase | Visual |
|---|---|
| *AI-native inference cloud* | Token particles flowing continuously through the lattice |
| *Dedicated GPU infrastructure* | The 3D lattice of wireframe cube nodes |
| *Serverless scaling* | Particle count is fixed but identities turn over — at every node a particle picks a fresh outgoing edge at random |
| *Predictable performance* | Speed clamps + edge cool-down constants — the system never spirals or freezes; same frame budget always |

## Implementation notes

- **Single self-contained HTML file** — no build step, no framework, no p5.
  Vanilla DOM + canvas
- **Canvas is DPR-aware**, uses simple Y/X-axis rotation + perspective divide,
  back-to-front depth sort for edges
- **Tab-pause** via `visibilitychange` — no CPU when the tab is backgrounded
- **`prefers-reduced-motion`**: renders one static frame, halts the loop
- **Resize-aware**: `ResizeObserver` on the canvas catches layout reflows
  (sidebar collapse, font loading, container resize)

## Files

- `hero.html` — the hero. Drop into a browser at full screen
- `README.md` — this file

## Known stand-ins

These are placeholders because I couldn't access the live site programmatically
(the sandbox blocks `gmicloud.ai`). Swap in real assets before shipping:

- **GMI logo SVG** is a sketched cloud-shape stand-in. Use the real logo
- **Display font** is JetBrains Mono. The live hero uses what looks like a
  custom mono — substitute it
- **NVIDIA eye icon** is a CSS gradient circle. Use the real NVIDIA wordmark
  badge SVG

## Files to compare

If you want the previous (incorrect) version, it's in git history:
`git log -- art/gmi-hero/hero.html` — the prior commit had cyan/magenta
chromatic-split typography and a full-bleed flow field, both wrong for GMI's
brand. This version replaces it.
