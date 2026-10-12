# quality-gates — decide before building, verify before shipping

> Merged from: `shinewinsu/vibe-frontend-design` (Design Read, Three Dials), `wwewtech/anti-slop-design` (5-phase loop, 7-axis gate, MIT), and this repo's `code-impeccable` + `stop-slop` (verification layers). See ATTRIBUTION.md.

Everything in this file exists to force the decisions *before* generation starts, and to catch slop *before* the user sees it. The pattern behind all AI-looking output is skipped decisions; the gates put the decisions back in.

## The Design Read (mandatory first line)

Before writing any HTML/CSS/component, output one line that pins the work. This closes the escape route to the statistical middle — once the read is stated, every choice has something to be checked against:

> **`Design Read: building [artifact type] for [audience], in [visual world], dials [V=? / M=? / D=?], stack [design system / components / motion].`**

Examples:

- `Design Read: building an AI devtool landing page for staff engineers and indie hackers, in a Linear-style dark minimal world, dials [V=7 / M=6 / D=4], stack Tailwind + Lucide + Framer Motion springs.`
- `Design Read: building a freight dispatcher dashboard for night-shift controllers, in a Technical Terminal world, dials [V=3 / M=2 / D=8], stack dense tables, tabular numerals, zero decorative motion.`

For code work, the same discipline in one line: *what does this module do, for whom, in which scene* — the code-side Design Read. If the line cannot be written, the understanding is not there yet.

## The Three Dials

Calibrate the three axes from the Design Read; they are the reason "good" differs per context:

**DESIGN_VARIANCE (V, 1–10) — how unexpected?**
- 1–3: regulated, enterprise, compliance-first. Strict symmetry.
- 4–6: modern SaaS, brand sites. Ordered, with local asymmetry.
- 7–8: consumer products, Apple-tier. Bento grids, parallax, dimensional whitespace.
- 9–10: award-tier, studios, experiments. Aggressive asymmetry, typographic collisions.

**MOTION_INTENSITY (M, 1–10) — how alive?**
- 1–2: near-static admin tools; color transitions only.
- 3–4: restrained; entrance shifts of 12–16px, smooth hovers.
- 5–7: standard modern web; parallax, magnetic buttons, sliding tab indicators.
- 8–10: cinematic; 3D tilt, cursor-reactive, shared-element transitions.

**VISUAL_DENSITY (D, 1–10) — how much per screen?**
- 1–3: gallery whitespace, luxury, portfolios.
- 4–5: landing pages, blogs, product intros. The golden middle.
- 6–8: productivity apps, Linear/GitHub dashboards.
- 9–10: trading terminals, ops control rooms.

A dispatch tool at V=9 M=8 is wrong; a studio portfolio at V=2 is wrong. The dials are how taste becomes explicit instead of vibes.

## The phase loop

```text
Phase 1  Diagnose     scan against banned-trope matrix / slop taxonomy; strip clutter
Phase 2  Foundation   pick archetype, declare tokens, pick type pairing, set dials
Phase 3  Structure    page-level controls, 1-to-3 hierarchy, layout pattern, surface stack
Phase 4  Detail       8-state primitives, icon system, motion moments, browser surfaces
Phase 5  Gate         score the axes below; any axis < 4 loops back to Phase 3 (not 4)
```

Bounded verification: build fully, inspect once with a batched pass (desktop + mobile together), fix everything shown in one batch, confirm with at most one more round, stop. Open-ended self-QA burns budget and degrades the result.

## The UI gate — 7 axes, every axis ≥ 4 (score 1–5)

| Axis | Checks |
| --- | --- |
| **1. Anti-slop purity** | Zero gradient blobs / gradient text; zero emoji icons; zero one-word italic accents; zero vanity stats; zero dead placeholders |
| **2. UX speed & 1-to-3** | One primary action per zone; ≤ 3 secondary; filters unified at page level; zero duplicated metrics |
| **3. Typographic discipline** | ≤ 2 families; tabular-nums on all metrics; body ≤ 75ch; sentence case; obvious scale steps; negative tracking on display |
| **4. Spacing geometry** | 8pt ladder values only; nested-radius formula holds; ≥ 16px card padding; optical icon alignment |
| **5. Motion & states** | Transitions < 200ms; 100+/day actions at 0ms; `:active` scale feedback; no `ease-in`; reduced-motion variant; all 8 states present |
| **6. Accessibility** | `:focus-visible` everywhere; no bare `outline: none`; `aria-label` on icon-only buttons; semantic elements (`button`, `nav`, `main`); contrast 4.5:1 / 3:1 |
| **7. Responsive linearity** | Clean vertical stacking on mobile; zero horizontal overflow; ≥ 44px touch targets; tables become cards or scroll containers |

## The code gate

Run the pre-flight from anti-vibe-code.md and score: HIGH findings weigh 10, MEDIUM 5, LOW 2, normalized per 100 lines. **0–20 clean; 21–40 slightly sloppy — fix the HIGHs at least; 41+ not shippable under this skill.** Plus the binary checks: behavior preserved (tests pass unchanged, signatures intact), no polish mixed with behavior change, and the `git log` test — each hunk's *why* is guessable by a reviewer.

## The prose gate

The five-dimension rubric from prose-git.md (directness, rhythm, trust, authenticity, density), 1–10 each. **≥ 35/50 to ship.** For commits and PR descriptions additionally: imperative subjects, why-bodies, no AI tells in history, testing sections present.

## The final assertion

Before delivering anything under this skill, answer honestly:

> *Does this read as crafted by a disciplined professional with extreme respect for the user's attention — or does any part of it look like it was generated from a prompt?*

If any element feels like prompt-slop: eliminate it, do not soften it. Then ship, and stop polishing. The remaining 2% is not worth the user's patience, and over-polished work starts acquiring its own uniformity tells. Craft ends at *decided and verified* — not at *perfect*.
