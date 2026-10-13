# Attribution & Sources

`craftsmanship` is an original synthesis commissioned for this repo, created by merging this repo's own sub-skills with six external sources (five repos and one research body). The synthesis, structure, and merged rule set are MIT (same as this repo's originals). Upstream material retains its original license; each reference file credits its sources inline.

## From this repo (merged in, MIT or upstream licenses as noted)

| Source | What was merged | License |
| --- | --- | --- |
| `skills/code-impeccable` (original to this repo) | Layered diagnosis order, naming discipline, behavior-preservation contract, idiom floor, anti-pattern flags | MIT |
| `skills/stop-slop` (upstream: hardikpandya/stop-slop) | Prose rules 1–7, the scoring rubric, phrase and structure catalogs | See `skills/stop-slop/LICENSE.upstream` |
| `skills/commit-craft` (original to this repo) | Conventional Commits workflow, PR description structure, Keep-a-Changelog format, good/bad commit examples | MIT |
| `skills/impeccable` (upstream: pbakaus/impeccable v4.5.2) | Craft-floor refuse list (banned scaffolds and surface habits), browser-surfaces rule, the bounded-verification principle | Apache 2.0 — see `skills/impeccable/LICENSE.upstream` |
| `skills/test-craft` (original to this repo) | Behavior-verification framing for the code gate | MIT |

Not merged, and not uncredited: `skills/code-review` (upstream: `awesome-skills/code-review-skill`, MIT) stays a standalone sibling sub-skill — its per-language PR-review guides are outside craftsmanship's scope. It is fully credited in the root `SKILL.md` and `README.md` of this repo.

## External sources (researched and merged for this skill)

| Source | What was merged | License |
| --- | --- | --- |
| `ericchen931209/vibe-slop-detector` — TAXONOMY.md | The S1–S13 slop taxonomy, severity levels, detection signals, scoring weights and bands (S14 is original to this repo) | As upstream |
| `wwewtech/anti-slop-design` | The banned-trope matrix, four archetypes with CSS tokens, UX axioms (1-to-3, 85% law), 8-state system, Emil Kowalski motion matrix, 7-axis gate, before/after table | MIT |
| `shahrukh-hack/vibe-superkit` | TASTE_GUIDE aesthetic personalities, slop-vs-craft table, micro-interaction principles, anti-ai-slop rules | As upstream |
| `shinewinsu/vibe-frontend-design` | Design Read protocol, Three Dials, the 10-item death list, layout patterns, surface hierarchy levels, typography engineering scale | As upstream |
| `ConardLi/garden-skills` — web-design-engineer | Read-before-ask calibration pattern, context-gathering priority, code-over-screenshots principle | As upstream |
| Pangram Labs — code-forensics writeups (pangram.com) | The "why AI code is recognizable" framing in `references/anti-vibe-code.md`: tells are structural (name distribution, comment-to-code ratio, error-handling shape, style uniformity), not stylistic; detectors exploit statistical regularities that human code violates naturally | Cited as research; © Pangram Labs |

## Individual credits

- **Emil Kowalski** (emilkowalski.dev) — the duration-by-frequency decision matrix, easing rules, and tactile-feedback principles in `references/craft-details.md` are his motion work, encountered via `wwewtech/anti-slop-design` and `shahrukh-hack/vibe-superkit`. Full credit to him.
- **Hardik Pandya** — the `stop-slop` prose system (rules, rubric, catalogs).
- **Paul Bakaus** — the `impeccable` craft-floor and bounded-verification principle.
- **awesome-skills** — `code-review`, kept as a sibling sub-skill.
- The authors of the five external repos and the Pangram Labs research above. Any errors in the merged synthesis are this repo's, not theirs.

## Pointed sources (cataloged, not merged)

`references/design-sources.md` catalogs third-party design sites — component libraries, generators, galleries — with license labels verified on 2026-10-13. These are pointers the agent may pull from or suggest to a user; **no content from those sites is merged into this skill**. License labels are as verified on that date; the reference instructs re-verification at the source before copying anything.

If you redistribute `craftsmanship`, keep this file and the per-file credits with it.
