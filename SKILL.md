---
name: theskill
description: "The definitive skill collection for polishing software deliverables — UI, prose, code, tests, commits, and PR reviews. Use whenever the user wants to refine, audit, harden, or elevate the quality of a frontend interface (websites, dashboards, components, design systems, typography, spacing, motion, accessibility); remove AI writing patterns from any prose (drafting, editing, reviewing); polish source code without changing behavior (naming, dead code, structure, idiomatic patterns, readability, refactor opportunities); write or audit tests — unit, integration, e2e, property-based (naming, assertions, edge cases, fixtures, isolation, flakiness, test pyramid); write high-quality git communications (commit messages, PR descriptions, release notes, changelogs); or conduct a code review of a pull request (architecture, performance, security, code quality, common bugs across React/Vue/Rust/TS/Go/Python/Java/etc.). Trigger this skill for ANY quality-polishing intent — even when the user doesn't explicitly say 'polish' or 'refine' but clearly wants something made better: vague requests like 'make this cleaner', 'this looks off', 'fix the writing', 'review my PR', 'why does this sound like AI', 'tighten up the code', 'are these tests any good' all apply. Routes between six specialized sub-skills: impeccable (frontend/UI, from pbakaus/impeccable v4.5.2), stop-slop (anti-AI prose, from hardikpandya/stop-slop), code-impeccable (code quality without behavior change), code-review (PR reviews, from awesome-skills/code-review-skill), test-craft (test suite quality), commit-craft (git communications)."
---

# theskill — the quality toolkit

`theskill` is a meta-skill: a small bundle of six specialized polishing skills that share one entry point so your `available_skills` inventory stays lean. When this skill triggers, you route to the right sub-skill based on what the user actually wants.

Three of the sub-skills (`impeccable`, `stop-slop`, `code-review`) are imported verbatim from their official upstream repositories — do not modify them in-place. The other three (`code-impeccable`, `test-craft`, `commit-craft`) are original to this repo.

## Routing table

Read the user's request, then pick the matching sub-skill. If two apply (e.g., "polish the UI copy and make sure it doesn't sound like AI"), invoke both in sequence — UI first, then prose.

| User intent | Sub-skill | Path | Origin |
| --- | --- | --- | --- |
| Refine, audit, redesign, or elevate a frontend interface — websites, dashboards, components, design systems, typography, spacing, motion, accessibility, error states, empty states | `impeccable` | `skills/impeccable/SKILL.md` | Upstream: `pbakaus/impeccable` v4.5.2 (Apache 2.0) |
| Remove AI writing patterns from prose — drafting, editing, reviewing, eliminating predictable tells like filler phrases, formulaic structures, narrator-from-a-distance voice, em-dashes | `stop-slop` | `skills/stop-slop/SKILL.md` | Upstream: `hardikpandya/stop-slop` |
| Polish source code without changing behavior — naming, dead code removal, structure, readability, idiomatic patterns, refactor opportunities | `code-impeccable` | `skills/code-impeccable/SKILL.md` | Original |
| Conduct a code review of a pull request — architecture, performance, security, code quality, common bugs; language-specific guidance for React/Vue/Angular/Svelte/Rust/TS/Go/Python/Java/C#/etc. | `code-review` | `skills/code-review/SKILL.md` | Upstream: `awesome-skills/code-review-skill` (MIT) |
| Write or audit tests — unit, integration, e2e, property-based; naming, assertions, edge cases, fixtures, isolation, flakiness, test pyramid | `test-craft` | `skills/test-craft/SKILL.md` | Original |
| Write high-quality git communications — conventional commit messages, PR descriptions, release notes, changelog entries | `commit-craft` | `skills/commit-craft/SKILL.md` | Original |

## How to route

1. Read the user's message and identify what kind of artifact they're working on (a UI? a piece of writing? code? a test suite? a PR? a git change?).
2. Open the matching sub-skill's `SKILL.md` and follow its instructions.
3. If the request spans two domains:
   - UI copy + anti-slop: `impeccable` first, then `stop-slop`.
   - Code refactor + test update: `code-impeccable` first, then `test-craft` (without changing assertions).
   - PR review + commit message: `code-review` first, then `commit-craft` for the final commit.
4. If no sub-skill cleanly matches, default to the one whose domain is closest to the artifact's medium (UI → impeccable, prose → stop-slop, code → code-impeccable, PR review → code-review, tests → test-craft, git artifact → commit-craft).

## Important: sub-skill-specific tooling

The `impeccable` sub-skill ships with its own scripts under `skills/impeccable/scripts/` — including the `impeccable` CLI launcher, font-index data, and live-browser automation. When invoking `impeccable`, follow its setup instructions verbatim (it expects to be invoked from the user's project root and may need to run `impeccable context` once per session). Do not assume the simpler skills' workflows apply.

The `code-review` sub-skill ships with assets (PR review template, review checklist) under `skills/code-review/assets/` and language-specific references under `skills/code-review/reference/`. Load the relevant language file when reviewing code in that language.

The `stop-slop` sub-skill is self-contained: just read `SKILL.md` and the three reference files in `references/` as needed.

## When NOT to trigger

- Pure backend logic, algorithms, or infrastructure work that doesn't touch UI, prose, code style, tests, PR review, or git messages.
- Generating brand-new content from scratch (this is a polishing toolkit, not a generator). Use the appropriate generation skill instead.
- Tasks that are explicitly about correctness/behavior (e.g., "fix this bug", "make this test pass") rather than quality/polish.

## Bilingual note

All six sub-skills are written in English (the working language of most codebases and AI tooling), but they apply equally to Portuguese or bilingual content. When the user writes in Portuguese, respond in Portuguese and apply the same principles — the polish patterns are language-agnostic, only the examples differ.

## Attribution

- `impeccable` is © Paul Bakaus, licensed Apache 2.0, source: <https://github.com/pbakaus/impeccable>. See `skills/impeccable/LICENSE.upstream`.
- `stop-slop` is © Hardik Pandya, source: <https://github.com/hardikpandya/stop-slop>. See `skills/stop-slop/LICENSE.upstream`.
- `code-review` is © awesome-skills, licensed MIT, source: <https://github.com/awesome-skills/code-review-skill>. See `skills/code-review/LICENSE.upstream`.
- `code-impeccable`, `test-craft`, and `commit-craft` are original to this repo, MIT licensed.

---

*theskill — because polish is the difference between "good enough" and "obviously the best on the market."*
