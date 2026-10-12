# craft-details — typography, motion, and the interaction layer

> Merged from: `wwewtech/anti-slop-design` (MIT — 8-state system, spacing geometry), `shinewinsu/vibe-frontend-design` (typography engineering), motion principles originally by **Emil Kowalski** (emilkowalski.dev, via the two repos above), and this repo's `impeccable` craft-floor (Apache 2.0 — browser surfaces, verify list). See ATTRIBUTION.md.

This file is the finish work. The layout is decided, the archetype tokens are in place — this is what separates "looks fine in a screenshot" from "feels crafted under the cursor".

## Typography engineering

Typography is the interface's voice; most AI output uses one bored monotone. The rules:

**Pairing.** Maximum two families: a display face with actual character + a body face built for reading (or display + mono for data-heavy surfaces). Characterful pairings that work: `Fraunces` + `Plus Jakarta Sans` (editorial warmth), `Space Grotesk` + `Inter Tight` (Swiss precision), `Playfair Display` + `Newsreader` (long-form elegance), `JetBrains Mono` pairings for terminal-archetype surfaces. Source and self-host the display face; shipping the platform default as your display voice is the closest-installed-font failure from the craft-floor.

**Scale.** Use proportional steps, not invented values:

| Role | Size | Line height | Tracking | Weight |
| --- | --- | --- | --- | --- |
| Display/Hero | 36–72px | 1.05–1.1 | -0.03em to -0.04em | 600–700 |
| H1 | 36–40px | 1.15 | -0.025em | 600–700 |
| H2 | 24–30px | 1.2 | -0.02em | 600 |
| H3 | 18–20px | 1.3 | -0.01em | 600 |
| Body | 14–16px | 1.6 (relaxed) | normal | 400 |
| Meta/caption | 12–13px | 1.4 | normal | 500 |

Every large sans heading gets negative tracking (`tracking-tight`); untracked large type is on the banned-trope list. Measure caps at 65–75ch for body (`max-w-prose`). Display max 6rem — past that, scale stops adding and starts shouting.

**Numbers.** `font-variant-numeric: tabular-nums` on every metric, price, timestamp, and table column. Proportional digits jittering in a live dashboard is an instant amateur tell. In Tailwind: `tabular-nums`.

**Steps must be obvious.** If H2 does not read clearly bigger than H3, the hierarchy does not exist. When torn, make the step larger, not smaller.

## Spacing geometry

**The 8pt rhythm.** All padding and gaps from the ladder: `4` (hairline) → `8` (compact) → `12` (standard control pad) → `16` (card pad) → `24` (section gutter) → `32`/`48`/`64` (macro whitespace). A `13px` and a `15px` in the same component is an accidental inconsistency; fix it to the ladder.

**Nested radius formula.** `radius_inner = max(0, radius_outer - padding)`. A 16px-radius card with 8px padding takes an 8px-radius button inside — not 16, not 0. This single formula is one of the most reliable "a person was here" signals in UI.

**Optical alignment.** Icon-text pairs: `gap-1.5` to `gap-2`, icon sized to the font's x-height (16px icon for 14px text). Pure mathematical centering of unlike shapes reads wrong; optical centering reads right.

**Grouping.** Tight groups, generous separation, and *more space above a heading than below it* — the heading belongs to the section it introduces. Read the computed values in the devtools, not the intention.

## Motion physics

The default AI motion is `transition: all 0.3s ease` on everything, which feels like wet cardboard. The replacement system:

**Duration by frequency (Emil Kowalski decision matrix):**
- Actions triggered 100+ times a day (command palette, row selection, keyboard shortcuts): **0ms. Never animate.** Speed is the feature.
- Standard interactions (tooltips, dropdowns, popovers): **120–180ms**.
- Modals and full-screen drawers: **200–250ms**.

**Easing:**
- `ease-in` is banned for UI — it starts slow and feels laggy.
- Use tense ease-out: `cubic-bezier(0.23, 1, 0.32, 1)`.
- Popovers scale from their trigger point (`transform-origin: top left`), never from screen center.
- Where spring physics are available, prefer them over linear timing: `transition: { type: "spring", stiffness: 400, damping: 28, mass: 0.6 }` — weight and resistance instead of a curve.

**Tactile feedback:** on press, scale down 2–3% — `transform: scale(0.97); transition: transform 60ms ease-out;`. Elements that do not respond to the cursor feel dead.

**Entrances:** one authored moment, not the same fade on every section, and not scattered effects everywhere. If there is a cascade, a lead element moves first, then children stagger 50–80ms apart. Exponential ease-out from an already-visible default state. Past transform and opacity, the palette includes blur, `backdrop-filter`, `clip-path`, `mask`, and shadow — when they stay smooth.

**`prefers-reduced-motion`:** ignoring it is on the death list. Every motion rule needs a reduced variant; usually "no entrance, states still change color".

## The 8-state interactive system

Every interactive primitive ships all eight states or it ships broken:

```
Default → Hover → Focus-visible → Active/press
                Disabled ← Loading ← Error ← Success
```

The production button standard (adapt tokens to the chosen archetype):

```css
.btn-primary {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  padding: 0.5rem 1rem;
  font-size: 0.875rem;
  font-weight: 500;
  line-height: 1.25rem;
  border-radius: var(--radius-sm, 6px);
  background: var(--accent-primary);
  color: var(--accent-foreground);
  border: 1px solid transparent;
  cursor: pointer;
  user-select: none;
  transition: background-color 140ms ease-out,
              transform 80ms ease-out,
              border-color 140ms ease-out;
}
.btn-primary:hover { filter: brightness(1.08); }
.btn-primary:focus-visible {
  outline: 2px solid var(--accent-primary);
  outline-offset: 2px;
}
.btn-primary:active { transform: scale(0.97); }
.btn-primary:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  pointer-events: none;
}
```

Inputs need the same treatment: real `<label>`s, `:focus-visible` rings (`ring-2 ring-primary/20`), error states that name the problem and the recovery, disabled states that block and explain. Loading states: skeletons with a shimmer highlight, or preserved content — never a blank flash.

## Browser surfaces — the cheapest human signal

The parts you did not draw still carry the design, and the browser ships them with defaults that belong to no design system. Theming these is the one thing human teams do and generated UI skips most reliably:

- **Text selection** (`::selection` from the palette),
- **the caret** (`caret-color`),
- **custom scrollbars** (`::-webkit-scrollbar`, `scrollbar-width`/`scrollbar-color`),
- **focus rings** (outline color and offset from tokens, never default blue unless it *is* the accent),
- **underline offset** on body links,
- **tabular numerals in data** (again — it belongs to the browser surface as much as to type).

Ten lines of CSS, and the page reads *built* rather than *assembled*.

## The verify list (run against the render, not the intention)

- **Contrast:** body and placeholder ≥ 4.5:1, large text ≥ 3:1. On colored surfaces, tint secondary text from that hue — never gray-on-color.
- **Depth:** shadows carry an offset and a soft blur. A zero-offset colored halo is decoration — remove it.
- **Spacing:** computed values on the ladder; tight groups; more space above headings than below.
- **Type:** real copy at every breakpoint, nothing overflowing, measure capped, steps obvious.
- **Motion:** one authored moment; high-frequency actions at 0ms; reduced-motion variant exists.
- **States:** all eight present on primitives; keyboard focus travels the page in a sane order; `tabindex` is not a minefield.
- **Browser surfaces:** selection, caret, scrollbars, focus rings themed from tokens.
- **Copy:** the product's own language — controls name their action, errors name the problem and the recovery.
- **Coverage:** every brief requirement present and findable within seconds.

One rendering pass, all checks together — they share one screenshot. Fix everything the pass shows in a single batch, confirm with at most one more round, stop. Open-ended self-QA burns the budget doing worse what a bounded pass does better.
