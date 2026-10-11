---
name: theskill
description: "The definitive skill collection for polishing software deliverables — UI, prose, code, and commits. Use whenever the user wants to refine, audit, harden, or elevate the quality of a frontend interface (websites, dashboards, components, design systems, typography, spacing, motion, accessibility); remove AI writing patterns from any prose (drafting, editing, reviewing); polish source code without changing behavior (naming, dead code, structure, idiomatic patterns, readability, refactor opportunities); or craft high-quality git communications (commit messages, PR descriptions, release notes, changelogs). Trigger this skill for ANY quality-polishing intent — even when the user doesn't explicitly say 'polish' or 'refine' but clearly wants something made better: vague requests like 'make this cleaner', 'this looks off', 'fix the writing', 'review my PR', 'why does this sound like AI', or 'tighten up the code' all apply. Routes between four specialized sub-skills: impeccable (frontend/UI), stop-slop (anti-AI prose), code-impeccable (code quality), commit-craft (git communications)."
---

# theskill — the quality toolkit

`theskill` is a meta-skill: a small bundle of four specialized polishing skills that share one entry point so your `available_skills` inventory stays lean. When this skill triggers, you route to the right sub-skill based on what the user actually wants.

## Routing table

Read the user's request, then pick the matching sub-skill. If two apply (e.g., "polish the UI copy and make sure it doesn't sound like AI"), invoke both in sequence — UI first, then prose.

| User intent | Sub-skill | Path |
| --- | --- | --- |
| Refine, audit, redesign, or elevate a frontend interface — websites, dashboards, components, design systems, typography, spacing, motion, accessibility, error states, empty states | `impeccable` | `skills/impeccable/SKILL.md` |
| Remove AI writing patterns from prose — drafting, editing, reviewing, eliminating predictable tells like "delve", "tapestry", em-dash asides, hollow hedging | `stop-slop` | `skills/stop-slop/SKILL.md` |
| Polish source code without changing behavior — naming, dead code removal, structure, readability, idiomatic patterns, refactor opportunities | `code-impeccable` | `skills/code-impeccable/SKILL.md` |
| Write high-quality git communications — conventional commit messages, PR descriptions, release notes, changelog entries | `commit-craft` | `skills/commit-craft/SKILL.md` |

## How to route

1. Read the user's message and identify what kind of artifact they're working on (a UI? a piece of writing? code? a git change?).
2. Open the matching sub-skill's `SKILL.md` and follow its instructions.
3. If the request spans two domains (e.g., "polish my landing page copy and make sure it doesn't sound AI-generated"), apply `impeccable` first for the visual/structural polish, then `stop-slop` for the prose pass.
4. If no sub-skill cleanly matches, default to the one whose domain is closest to the artifact's medium (UI → impeccable, prose → stop-slop, code → code-impeccable, git artifact → commit-craft).

## When NOT to trigger

- Pure backend logic, algorithms, or infrastructure work that doesn't touch UI, prose, code style, or git messages.
- Generating brand-new content from scratch (this is a polishing toolkit, not a generator). Use the appropriate generation skill instead.
- Tasks that are explicitly about correctness/behavior (e.g., "fix this bug", "make this test pass") rather than quality/polish.

## Bilingual note

All four sub-skills are written in English (the working language of most codebases and AI tooling), but they apply equally to Portuguese or bilingual content. When the user writes in Portuguese, respond in Portuguese and apply the same principles — the polish patterns are language-agnostic, only the examples differ.

---

*theskill — because polish is the difference between "good enough" and "obviously the best on the market."*
