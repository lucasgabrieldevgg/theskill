# Attribution & Sources

`craftsmanship` is an original synthesis commissioned for this repo, created by merging this repo's own sub-skills with external sources. As of v2.0.0 it carries three tracks — process (new), code, and prose/git — after the design track moved to its own complete skill, the `design` repo. The synthesis, structure, and merged rule set are MIT (same as this repo's originals). Upstream material retains its original license; each reference file credits its sources inline.

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
| `obra/superpowers` (v7.0.0) | The entire process track (`references/the-process.md`, added v2.0.0): brainstorming with hard gates, plan structure and task right-sizing, TDD iron law and red-green discipline, inline-execution rulings/ledger, the four-phase systematic debugging method with the 3-fixes architecture stop, review request/reception protocol, evidence-before-claims verification, branch finishing menu. Adapted to this repo's craft framing; behavioral content is theirs | MIT — © 2025 Jesse Vincent |
| `ericchen931209/vibe-slop-detector` — TAXONOMY.md | The S1–S13 slop taxonomy, severity levels, detection signals, scoring weights and bands (S14 is original to this repo) | As upstream |
| `shahrukh-hack/vibe-superkit` | Micro-interaction principles and anti-ai-slop rules (the surviving code-track portions; the taste/design portions moved with the design track) | As upstream |
| `ConardLi/garden-skills` — web-design-engineer | Read-before-ask calibration pattern, context-gathering priority, code-over-screenshots principle | As upstream |
| Pangram Labs — code-forensics writeups (pangram.com) | The "why AI code is recognizable" framing in `references/anti-vibe-code.md`: tells are structural (name distribution, comment-to-code ratio, error-handling shape, style uniformity), not stylistic; detectors exploit statistical regularities that human code violates naturally | Cited as research; © Pangram Labs |

## Individual credits

- **Jesse Vincent** (obra) and the superpowers contributors — the execution methodology in `references/the-process.md` is their work, merged under MIT with adaptation.
- **Hardik Pandya** — the `stop-slop` prose system (rules, rubric, catalogs).
- **Paul Bakaus** — the `impeccable` craft-floor and bounded-verification principle.
- **awesome-skills** — `code-review`, kept as a sibling sub-skill.
- The authors of the external repos and the Pangram Labs research above. Any errors in the merged synthesis are this repo's, not theirs.

## The design track moved out (v2.0.0)

The design references (`anti-slop-design.md`, `craft-details.md`, `design-sources.md`, and the UI gates from `quality-gates.md`) moved to the `design` repo (`lucasgabrieldevgg/design`) so both disciplines could be complete. That repo carries the full design lineage and credits: `wwewtech/anti-slop-design` (MIT), `shinewinsu/vibe-frontend-design`, Emil Kowalski's motion principles, `pbakaus/impeccable`'s design-side rules — plus five new sources merged there (`Nutlope/hallmark`, `oil-oil/oil-ui`, `xiaopu-ai/web-design`, `dominikmartn/nothing-design-skill`, `Gesso-Build/skills`). See that repo's ATTRIBUTION.md.

## Pointed sources (cataloged, not merged)

`references/design-sources.md` moved to the `design` repo with the rest of the design track (2026-10-20). It catalogs third-party design sites with license labels verified on 2026-10-13 — pointers only; nothing from those sites is merged into either skill.

If you redistribute `craftsmanship`, keep this file and the per-file credits with it.
