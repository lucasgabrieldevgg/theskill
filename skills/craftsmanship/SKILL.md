---
name: craftsmanship
description: "Anti-vibe coding and design: make AI-assisted work read as human-crafted. Two merged disciplines in one skill. TRACK 1 - CODE: remove AI tells from source code (generic naming like data/result/manager/handler, ghost comments that restate the code, leaked AI signature phrases, silent catch-all error handling, god functions, copy-paste clones, verbosity inflation, redundant docstrings, defensive over-checking, TODO graveyards, dead imports) and write domain-named, honestly-commented, idiomatically-native code in TypeScript, Python, Go, Rust, Java, C#, and more. TRACK 2 - DESIGN: kill the generic AI template look (purple/indigo gradient blobs, three-equal-card grids, emoji-as-icons, screaming uppercase eyebrow labels, gradient text, glassmorphism everywhere, vanity stats, missing interactive states, broken placeholders) and build bespoke interfaces with real typography engineering, spacing geometry, motion physics, and four curated archetypes (Quiet Luxury SaaS, Technical Terminal, Editorial, Warm Tactile). ALSO COVERS: prose and git communications without chatbot cadence (no throat-clearing openers, no binary contrasts, no false agency, conventional commits with zero AI tells). Use this skill for ANY task that writes, refactors, reviews, or polishes frontend or fullstack code, UI, docs, README, or commits - even when the user never says 'polish': 'make it look professional', 'this feels generic', 'fix the design', 'tighten this up', 'does this look AI-made?', 'de-slop my app', 'add personality', 'make it pop', 'give it a human touch' all trigger it. Before delivering any user-facing artifact, run its quality gates."
version: 1.0.0
license: MIT for the synthesis; upstream content keeps its own licenses - see ATTRIBUTION.md
---

# craftsmanship — code and design that pass as human work

The test for everything this skill produces: a senior engineer or designer reads the result and cannot tell a machine wrote it. Not because it hides AI assistance, but because the work carries the properties human craft always carries: decisions instead of defaults, domain language instead of placeholders, restraint instead of decoration, and evidence of caring.

AI-generated work fails that test in two predictable ways. In code, it produces *vibe slop*: semantically empty names, comments narrating the obvious, error handling that swallows failures, and structure that maximizes line count instead of clarity. In design, it produces *template slop*: the same purple gradient glow, the same three identical cards, the same emoji icons, the same Inter-on-everything, assembled rather than designed. Both share one root cause: the model reaches for the statistical middle of its training data instead of making committed choices.

This skill exists to break that default. It merges two tracks with their own reference files, plus a lighter third track for prose and git communications. Load the reference you need, apply the workflow, run the gates before shipping.

## The craft contract

Four rules that hold across both tracks. They are explained here once because they explain every specific rule that follows.

1. **Decide, don't default.** Every element in the output should be traceable to a choice: this name, this palette, this rhythm, because the domain and the use scene call for it. A default you never questioned is exactly what "looks AI" means. When you catch yourself reaching for the middle of the distribution, stop and pick a side.
2. **The artifact speaks the domain's language.** A codebase about invoices should read `invoiceDueDate`, `dunningLevel`, `writeOff` — not `data`, `item`, `processItem`. An interface for freight logistics should sound like a dispatcher, not like a template. Domain vocabulary is the cheapest and strongest human signal there is.
3. **Restraint is a feature.** Deleting a card, a badge, a comment, a gradient, an animation is often the highest-value edit available. AI output errs toward addition; craft errs toward subtraction. Audit for what can be removed before adding anything.
4. **Verify the built result, not the intention.** Every check in this skill runs against the actual output: the rendered page, the compiled behavior, the diff as the reader will see it. "I meant to" does not count.

## How to route

Identify what the user is working on, then load the matching reference. Most real requests span two tracks — that is expected; run both.

| The work | Reference | What it gives you |
| --- | --- | --- |
| Writing or polishing any source code — frontend, backend, fullstack, any language | [references/anti-vibe-code.md](references/anti-vibe-code.md) | The 14-pattern slop taxonomy with severity levels, naming discipline, comment and error-handling rules, language idioms, before/after examples |
| Building, restyling, or auditing any interface — pages, dashboards, components, landing pages | [references/anti-slop-design.md](references/anti-slop-design.md) | The banned-trope matrix, four archetypes with full CSS tokens, layout patterns, surface hierarchy, UX axioms |
| Typography, motion, interaction detail work | [references/craft-details.md](references/craft-details.md) | Type scales and pairing rules, motion physics and timing, the 8-state interactive system, browser surfaces, spacing geometry |
| README, docs, UI copy, commit messages, PR descriptions, changelogs | [references/prose-git.md](references/prose-git.md) | AI prose patterns to kill, the stop-slop scoring rubric, conventional commits without AI tells |
| Before delivering anything user-facing | [references/quality-gates.md](references/quality-gates.md) | The Design Read protocol, Three Dials, phase loop, and the pre-emit gates for code and UI |

Typical combinations:

- "Build a dashboard" → anti-slop-design (structure + archetype) → craft-details (type + motion) → quality-gates (pre-emit) → anti-vibe-code (while writing the components).
- "This module looks AI-generated, fix it" → anti-vibe-code → quality-gates (code gate).
- "Write the README for this" → prose-git alone.
- "Make a landing page and don't make it look like every AI site" → all four, in the order above.

## The workflow

One loop serves both tracks. The phases compress for small tasks, but none is skipped.

1. **Read before making.** State in one line what the artifact is for, who uses it, and in what scene — before writing anything. For UI work this is the Design Read; for code work it is naming the module's actual job. If you cannot state it in one line, you do not understand it well enough to craft it.
2. **Diagnose against the catalogs.** Walk the existing code or markup against the slop taxonomy (code) or the banned-trope matrix (design). Flag every finding with its severity. Do not fix yet — see the whole field first.
3. **Prescribe the smallest honest diff.** Group related findings and fix them in batches (all renames together, all dead code together, one archetype applied everywhere at once). Never bundle polish with behavior changes; a bug spotted mid-polish gets flagged for a separate change, not fixed here.
4. **Verify behavior survived.** For code: signatures unchanged or all callers updated, control flow identical, tests pass untouched. For UI: the interactive logic, form state, and data handlers from the original survive the restyle — visual refactors never discard function.
5. **Run the gate before delivery.** The pre-emit gates in [references/quality-gates.md](references/quality-gates.md). Score, fix what fails, ship.

## The hard bans

Hybrid rigidity: these are objective, binary, non-negotiable. Everything subjective lives in the references as explained principles instead. When a ban conflicts with an explicit user instruction, the user wins — note the override and proceed.

**Code — never ship:**
- Names from the empty set: `data`, `result`, `temp`, `info`, `obj`, `val`, `thing`, `manager`, `handler`, `helper`, `utils`, `processor` when a domain-specific name exists.
- Comments that restate the adjacent code, or AI signature phrases ("certainly", "here's the implementation", "as an AI").
- Silent error swallowing: `except: pass`, `catch { }`, catch-log-and-continue without re-raise or handling.
- Commented-out code (git remembers) and TODO placeholders you could resolve right now.

**Design — never ship:**
- Purple/indigo radial gradient blobs on dark backgrounds, gradient text, glowing card borders.
- Raw emoji standing in for an icon system; icons come from one library, one stroke weight.
- Three identical icon-heading-text cards as the page structure; nested cards.
- Uppercase tracked-out eyebrow labels above headings.
- Vanity metrics with no source ("99.9% uptime", "10x faster") decorating a layout.
- Placeholders that will 404 in production (placeholder.com, hotlinked Unsplash, lorem ipsum in shipped copy).

**Prose and git — never ship:**
- Throat-clearing openers ("here's the thing", "let me be clear"), em-dash cadence, "not X, but Y" binary contrasts.
- AI tells in commit messages: "leverage", "seamlessly", "robust solution" — they live forever in `git log`.

## Calibration, not uniformity

The failure mode this skill must avoid: producing a new template. Perfectly uniform naming, one spacing value everywhere, identical rhythm in every paragraph — that is also a machine signature. Human codebases have local idioms, a comment in first person where the codebase does that, a deliberate asymmetry, a section that breaks the grid on purpose. The gates ask "was this decided?", and a *documented* inconsistency passes while an *accidental* one fails. When you choose to break a rule here, do it loudly and once, not timidly and everywhere.

## When NOT to trigger

- Greenfield generation with no quality bar stated and no human-craft requirement — the user wants speed, and that is legitimate. (This skill still applies the moment they say "make it good".)
- Pure backend algorithms, data processing, or infra with no user-facing surface AND no naming/comment polish requested.
- Tasks about correctness only ("fix this bug", "make this test pass") — though the *commit message* for that fix is this skill's domain.
- Security audits, test-suite strategy, and multi-language PR review — the sibling sub-skills in this repo (`code-review`, `test-craft`) cover those deeper.

## Attribution

This skill is an original synthesis commissioned for this repo, merging the repo's own sub-skills with five external sources. See [ATTRIBUTION.md](ATTRIBUTION.md) for the full list and licenses; upstream material retains its original licenses and is credited in each reference file.
