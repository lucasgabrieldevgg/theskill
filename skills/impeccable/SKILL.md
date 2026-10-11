---
name: impeccable
description: "Use when the user wants to design, redesign, shape, critique, audit, polish, clarify, distill, harden, optimize, adapt, animate, colorize, extract, or otherwise improve a frontend interface. Covers websites, landing pages, dashboards, product UI, app shells, components, forms, settings, onboarding, and empty states. Handles UX review, visual hierarchy, information architecture, cognitive load, accessibility, performance, responsive behavior, theming, anti-patterns, typography, fonts, spacing, layout, alignment, color, motion, micro-interactions, UX copy, error states, edge cases, i18n, and reusable design systems or tokens. Also use for bland designs that need to become bolder or more delightful, loud designs that should become quieter, live browser iteration on UI elements, or ambitious visual effects that should feel technically extraordinary. Not for backend-only or non-UI tasks."
---

# impeccable — frontend polish

`impeccable` is the skill for making frontend interfaces feel finished. It covers everything from a single misaligned button to a full design-system audit.

## When to use

Trigger this sub-skill when the user is working on anything user-facing and wants it to look, feel, or behave better. That includes:

- **Visual polish**: typography, spacing, alignment, color, contrast, hierarchy, density.
- **Interaction polish**: motion, micro-interactions, hover/focus/active states, transitions, loading states, empty states.
- **Structural polish**: information architecture, layout, component composition, design tokens, reusable patterns.
- **Audit mode**: review an existing UI and produce a prioritized list of issues.
- **Directional shifts**: make a bland design bolder, or quiet down a loud one.

## How to use

### Step 1 — Understand the artifact

Before suggesting any change, identify what you're polishing:

- A single component, a full page, a flow, or a whole design system?
- Static design (Figma/screenshot) or live code (HTML/CSS/React/Vue)?
- What's the audience and the brand voice?
- Is the user asking for a directional shift (bolder? quieter? more delightful? more professional?) or just "make it better"?

If the user didn't specify direction, ask one short question — but bias toward action: pick the most likely direction, state your assumption, and proceed.

### Step 2 — Diagnose

Walk through the interface in this order (each layer builds on the previous):

1. **Structure & hierarchy** — Is the information architecture clear? Does the eye know where to land first? Are there competing primaries?
2. **Layout & spacing** — Is the spacing scale consistent (typically 4px or 8px base)? Are alignment relationships explicit (grid, flex)? Are edges flush where they should be?
3. **Typography** — Is the type scale limited and consistent (usually 3–5 sizes)? Is line-height comfortable for body copy (1.4–1.6)? Are font weights used meaningfully, not decoratively?
4. **Color & contrast** — Is the palette limited? Does text meet WCAG AA (4.5:1 for body, 3:1 for large)? Is color used semantically, not decoratively?
5. **Motion & interaction** — Do state changes feel responsive (under 100ms for direct manipulation, 200–400ms for transitions)? Are easings natural (cubic-bezier, not linear)? Are hover/focus/active states visible?
6. **Edge cases** — Empty states, error states, loading states, long content, RTL, dark mode, reduced-motion preferences.

### Step 3 — Prescribe

For each issue found, give the user:

- **What** is wrong (specific element, specific property).
- **Why** it matters (the perceptual, cognitive, or accessibility reason — not just "looks better").
- **How** to fix it (concrete CSS/design-token/code change, not "make it nicer").
- **Priority** (P0 blocking / P1 should-fix / P2 nice-to-have).

Avoid vague prescriptions like "improve spacing" or "make it pop". If you can't write the exact CSS or token change, you don't understand the issue well enough yet — diagnose more.

### Step 4 — Deliver

If working in code, propose the smallest possible diff. If working in design language, propose the smallest token-system change that ripples correctly. Always prefer edits over rewrites.

## Common anti-patterns to flag

- **Decorative gradients on text** — kills legibility, looks dated.
- **Box-shadow as depth** without a coherent elevation system — produces visual noise.
- **Border-radius inconsistency** — usually a sign of borrowed components; pick one scale (4/8/12/16 or 6/12/24) and stick to it.
- **Hover states that only change color** — feedback should be immediate and visible; combine color with subtle scale or shadow shift.
- **Empty states that are just "No data"** — empty states are an opportunity to teach, onboard, or suggest next actions.
- **Modals for confirmation** — prefer inline confirmation for low-stakes actions.
- **Auto-advancing carousels** — research consistently shows users hate them.
- **Infinite scroll on transactional pages** — users can never reach a footer or a sense of completion.

## When NOT to use

- Pure backend logic or infrastructure.
- Content writing / copywriting alone — that's `stop-slop`'s domain.
- Brand-new generation of UI from scratch (this is polish, not generation).
- Code-style refactors that don't touch the visible result — that's `code-impeccable`.

## References

Place deeper reference docs in `references/` — e.g., `references/design-tokens.md`, `references/accessibility-checklist.md`. Load them when the user asks about a specific subdomain.
