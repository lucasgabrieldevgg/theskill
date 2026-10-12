# anti-slop-design — the design track

> Merged from: `wwewtech/anti-slop-design` (MIT), `shahrukh-hack/vibe-superkit`, `shinewinsu/vibe-frontend-design`, and this repo's `impeccable` craft-floor (upstream pbakaus/impeccable, Apache 2.0). See ATTRIBUTION.md.

An interface crafted under this track looks *decided*: one committed visual world, a layout that follows the content instead of the container library, hierarchy you can see from across the room, and nothing decorative that is not also structural. The instant any element reads as "the default thing the model does", it goes.

## The banned-trope matrix

These are the assembled-not-designed tells. Each row: the trope, how it shows up, and the replacement that carries the same job with actual craft. Scan any UI you touch against this list before doing anything else.

| Trope | How it shows up | Replace with |
| --- | --- | --- |
| **AI dark-mode blob** | `radial-gradient` from indigo-600/purple-900 blurred into corners of a dark background | Deliberate monochrome surfaces (`#09090b`, `#121214`) with 1px hairline borders `rgba(255,255,255,0.08)` |
| **Slate/indigo default** | `bg-slate-900 text-slate-400 bg-indigo-600` everywhere | A curated token set with a chosen temperature (OKLCH/HSL) — see archetypes below |
| **Three-identical-card grid** | Three same-size icon-heading-text cards with hover glow | Content-driven layout: asymmetric bento (one hero tile spans 2×2), split panels, or workflow rows |
| **Emoji as icons** | `🚀 🔥 💡 📊` in buttons, sidebars, cards | One icon library (Lucide, Phosphor, Heroicons), single stroke weight 1.5–2px |
| **Vanity stats** | "+99.9% uptime", "10x faster", "50k+ users" with no source | Real telemetry, or delete the card. Zero invented metrics |
| **Screaming eyebrows** | Tracked-out uppercase `FEATURES` / `OVERVIEW` above every heading | Sentence case, or nothing — a heading that needs a label is a weak heading |
| **One-word gradient/italic accent** | "Make it *pop* tonight" with the accent word in gradient text | Uniform weight; let the whole statement carry authority. Emphasis from size or weight, never gradient |
| **Metric duplication** | The same KPI in header, sidebar, and three cards | One source of truth per viewport; drill-downs below the single primary KPI banner |
| **Filter pollution** | Date picker repeated inside every card | One page-level control bar that syncs all views |
| **Space-wasting hero widget** | Giant 3D globe / world map at 60% of viewport with no actionable data | Compact bar comparisons, sparklines, or delta tables with tabular numbers |
| **Missing states** | Buttons with hover only — no focus-visible, active, loading, disabled | The full 8-state system (see craft-details.md) |
| **Dead placeholders** | via.placeholder.com, hotlinked Unsplash, lorem ipsum in shipped copy | Inline SVG, CSS shapes, local verified assets, real copy |
| **Glassmorphism everywhere** | `backdrop-blur` on every surface | Blur reserved for floating chrome (sticky nav, overlays) — surfaces elsewhere stay solid and layered |
| **Mono-as-costume** | Monospace font to feel "technical" on non-technical text | Monospace only for code, data, measurements |
| **Pure black on pure white** | `#000000` / `#ffffff` in dark mode with flat gray text | Tinted charcoal (`#090a0f`, `#0d0e12`), multi-step text (`zinc-100 → zinc-400`) |
| **Same-fade-everything** | Every element fades in with identical rhythm | One lead element, then staggered cascade (50–80ms steps) — or no entrance at all |

Also banned outright (from impeccable's craft-floor): nested cards; a colored `border-left` above 1px on cards/alerts; hard offset shadows (`4px 4px 0`) outside a genuinely neobrutalist world; section numbers (`01 / 02`) unless sequence carries information; a modal for a task needing neither interruption nor protected focus; display faces that ship as the platform default (source a real face whose character matches — the closest installed font is a failure, not a fallback).

## The four archetypes

Pick one per project and commit. Mixing archetypes mid-page is the fastest way back to slop. Each block is a complete token starter — adapt hues to the brand, keep the *structure* of the relationships (canvas darkest, surfaces stepping up, one accent, two text steps minimum).

### A — Quiet Luxury SaaS (B2B tools, dashboards, pro apps)

```css
:root {
  --bg-canvas: #09090b;
  --bg-surface: #121215;
  --bg-surface-elevated: #18181c;
  --border-subtle: rgba(255,255,255,0.08);
  --border-hover: rgba(255,255,255,0.16);
  --accent-primary: #3b82f6;         /* Electric Cobalt */
  --accent-foreground: #ffffff;
  --text-primary: #f4f4f5;
  --text-secondary: #a1a1aa;
  --text-muted: #71717a;
  --radius-sm: 6px;  --radius-md: 10px;  --radius-lg: 14px;
}
```
Reference feel: Linear. Restraint as luxury; the accent appears on exactly one primary action per viewport.

### B — Technical Dense Terminal (DevTools, FinTech, observability)

```css
:root {
  --bg-canvas: #0c0d0e;
  --bg-surface: #141618;
  --bg-surface-elevated: #1a1d20;
  --border-subtle: #24282c;
  --border-hover: #383e44;
  --accent-primary: #10b981;         /* Precision Emerald */
  --accent-secondary: #f59e0b;       /* Amber for alerts only */
  --text-primary: #e6edf3;
  --text-secondary: #8b949e;
  --font-mono: 'JetBrains Mono', monospace;
  --radius-sm: 2px;  --radius-md: 4px;
}
```
Reference feel: GitHub dark, Bloomberg. Density is the point; tabular numbers everywhere.

### C — Editorial & Refined (media, portfolios, long-form, landing pages with taste)

```css
:root {
  --bg-canvas: #faf8f5;
  --bg-surface: #ffffff;
  --border-subtle: #e8e4df;
  --border-hover: #d1ccc4;
  --accent-primary: #1a1a1a;         /* Ink is the accent */
  --text-primary: #1a1918;
  --text-secondary: #635f59;
  --font-display: 'Playfair Display', serif;   /* or Fraunces */
  --font-body: 'Newsreader', 'Inter', sans-serif;
  --radius-sm: 0px;  --radius-md: 2px;
}
```
Reference feel: Stripe Press, Kinfolk, high-end journals. Asymmetry, generous whitespace, ink and paper.

### D — Warm Tactile (consumer products, creator tools, physical goods)

```css
:root {
  --bg-canvas: #f4f4f0;
  --bg-surface: #ffffff;
  --border-subtle: #e2e1db;
  --border-hover: #cbcac4;
  --accent-primary: #d97706;         /* Warm Ochre */
  --text-primary: #1c1917;
  --text-secondary: #78716c;
  --radius-sm: 8px;  --radius-md: 16px;  --radius-lg: 24px;
}
```
Reference feel: Teenage Engineering, Apple Pro pages. Tactile radii, warm neutrals, photography-forward.

Aesthetic mapping for typography personalities: Editorial pairs `Fraunces`/`Playfair` + `Plus Jakarta Sans`; Swiss Precision pairs `Space Grotesk` (tracking -0.04em) + `Inter Tight`; Tactile Luxe pairs a heavy geometric display + crisp mono tags. Default prohibition: unmodified Inter as the *entire* type system. Two families maximum, display + body (or display + mono for data).

## Layout patterns that read as designed

Anchor every view to one of these instead of free-form boxes (full parameter reference in craft-details.md):

- **Bento grid** — one hero tile `col-span-2 row-span-2` plus supporting tiles; hierarchy through size, not glow. `grid grid-cols-1 md:grid-cols-3 gap-4 lg:grid-cols-4`.
- **Split-screen** — 50/50 or 60/40: value proposition + live interactive preview / real screenshot / code block. `grid lg:grid-cols-12` with 5/7 or 7/5 splits.
- **Asymmetric 12-col** — 7:5, 8:4 column splits with occasional `translate-y-8` overlap; magazine breathing.
- **Masonry** — equal width, natural heights: testimonial walls, galleries. `columns-1 sm:columns-2 lg:columns-3`.
- **Card flow / timeline** — single column with a connecting rail: changelogs, step flows. `relative border-l pl-6 space-y-8`.
- **SaaS shell** — fixed sidebar (240px, 64px icon-rail collapsed) + page header (breadcrumbs, search, primary action) + scrollable main `max-w-7xl mx-auto px-6 py-8`.
- **High-density dashboard** — sticky page-level control bar → single-row 4-col KPI strip → 70/30 split (primary trend / secondary breakdown) → paginated table.
- **Conversion landing** — crisp nav (brand, 3 links, 1 CTA) → hero (one offer, one primary button, one secondary link, one dominant visual) → social proof strip → bento benefits → interactive preview → pricing matrix → footer.

## Surface hierarchy

Never let everything sit on one plane. Four levels, tokens already reflect it:

- **Level 0 — canvas:** the page base.
- **Level 1 — surface:** large containers, sidebar, cards. One step up from canvas, hairline border.
- **Level 2 — overlay/interactive:** hovered rows, list cards, popovers anchored to content. Second step, hover brightens border to `--border-hover`.
- **Level 3 — elevated:** modals, menus, floating panels. `shadow-2xl` class depth, own focus ring.

## UX axioms (speed is the metric)

- **The 1-to-3 rule.** Every screen zone: one primary element or action, at most three secondary. Five equal-weight buttons is a popover waiting to happen.
- **The 85% law.** Design for the scenario 85% of users run ("Create link", "Run report"), instant and zero-click. Secondary actions lose visual weight and tuck away. High-frequency controls never live inside monthly-configuration screens.
- **No duplication.** One brand mark per viewport. One primary CTA per card. One global filter bar per view.
- **Mobile linearity on desktop.** Two competing horizontal logic blocks side by side lose; sequential top-to-bottom rhythm wins.
- **Context splits assets.** Physical goods: the interface is a silent frame — neutral canvas, generous whitespace, photography dominates. Digital products: visualize the intangible — real interactive components, syntax-highlighted code, live KPI figures.
- **Mini-mockups over screenshots.** For feature showcases, build styled DOM cards, micro-charts, realistic data rows — not static fake screenshots. Avatars: SVG identicons or monograms on neutral backdrops, `alt` and explicit `aspect-ratio` on every image (CLS is a craft failure).

## Before/after transformations

| Element | Slop version | Craft version | Why |
| --- | --- | --- | --- |
| Analytics header | Date filter inside 4 individual cards, 3 duplicate counters | One global date range in the page header, one KPI banner | Cards sync, no disjoint time slices |
| Sidebar | Emojis + purple gradient on active link | 240px rail, 1.5px-stroke Lucide icons, hairline active border | Corporate credibility, less fatigue |
| Regional data | Decorative 3D globe, zero percentages | Horizontal bar list with deltas, tabular numbers | Utility instead of CPU-hogging fluff |
| Primary button | `bg-indigo-600 transition-all duration-300`, no focus ring | `bg-zinc-900 active:scale-[0.97] focus-visible:ring-2`, 140ms ease-out | Physical response, WCAG, human feel |
| Hero | 140px headline over 4 lines, 1 word bold-italic, 3 buttons, preloader | 44px headline on one offer, 1 CTA + 1 demo link, instant render | First impression in 50ms; preloaders bleed users |

## The refusal test (from impeccable)

Before shipping any interface, hold it against this: *does this feel crafted by someone with extreme respect for the user's attention and time, or does it look like it was generated from a prompt?* If any element feels like prompt-slop, eliminate that element — not soften it. Then run the gates in quality-gates.md.
