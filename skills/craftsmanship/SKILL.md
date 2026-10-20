---
name: craftsmanship
description: "Anti-vibe coding as a complete discipline: the execution process AND the artifact quality. Three tracks. TRACK 1 - PROCESS: the loop that prevents slop before it exists - brainstorm with hard gates (nothing built until the human approves), bite-sized implementation plans with exact interfaces, TDD as the iron law (no production code without a failing test first - delete code written before its test), systematic debugging (no fixes without root cause; 3+ failed fixes = architecture problem), review with fresh eyes and crafted context, evidence-before-claims verification, and integration as the human's decision. TRACK 2 - CODE: remove AI tells from source code (generic naming like data/result/manager/handler, ghost comments that restate the code, leaked AI signature phrases, silent catch-all error handling, god functions, copy-paste clones, verbosity inflation, redundant docstrings, defensive over-checking, TODO graveyards, dead imports) and write domain-named, honestly-commented, idiomatically-native code in TypeScript, Python, Go, Rust, Java, C#, and more. TRACK 3 - PROSE & GIT: README, docs, UI copy, commit messages, PR descriptions without chatbot cadence (no throat-clearing openers, no binary contrasts, no false agency; conventional commits with zero AI tells). Use this skill for ANY task that plans, writes, refactors, reviews, debugs, tests, or polishes code, docs, or commits - even when the user never says 'polish': 'make it look professional', 'this feels generic', 'fix this bug for real', 'why does my code look AI-generated', 'de-slop my code', 'plan this feature', 'help me build this right' all trigger it. Visual design (UI tropes, archetypes, layout) routes to the sibling 'design' skill."
version: 2.0.0
license: MIT for the synthesis; upstream content keeps its own licenses - see ATTRIBUTION.md
---

# craftsmanship — code and process that pass as human work

The test for everything this skill produces: a senior engineer reads the result and cannot tell a machine wrote it. Not because it hides AI assistance, but because the work carries the properties human craft always carries: decisions instead of defaults, domain language instead of placeholders, evidence instead of claims, and restraint instead of decoration.

AI-generated work fails that test in three predictable ways, and each has a track. In the **process**, it builds before understanding, fixes before diagnosing, and claims before verifying — vibe coding in the literal sense. In the **code**, it produces *vibe slop*: semantically empty names, comments narrating the obvious, error handling that swallows failures, structure that maximizes line count instead of clarity. In **prose and git history**, it leaves chatbot cadence that lives forever in the log. All three share one root cause: the model reaches for the statistical middle instead of making committed choices. This skill exists to break that default.

**Load on demand.** This SKILL.md is the only always-load surface. The reference files route by task — loading all four at once defeats the router and burns context on rules the task never touches.

**Visual design moved out.** The design track (banned tropes, archetypes, typography/motion craft, UI gates) now lives in its own complete skill: the `design` repo (`lucasgabrieldevgg/design`). When the task is about how an interface *looks* — "make it look professional", "this looks AI-generated", landing pages, restyles, UI audits — load that skill. When code and UI meet (the usual fullstack job), run both: `design` for the surface, this skill for everything under it.

## The craft contract

Four rules that hold across all tracks. They explain every specific rule that follows.

1. **Decide, don't default.** Every element in the output should be traceable to a choice: this name, this structure, this test, because the domain and the use scene call for it. A default you never questioned is exactly what "looks AI" means. When you catch yourself reaching for the middle of the distribution, stop and pick a side.
2. **The artifact speaks the domain's language.** A codebase about invoices should read `invoiceDueDate`, `dunningLevel`, `writeOff` — not `data`, `item`, `processItem`. Domain vocabulary is the cheapest and strongest human signal there is.
3. **Restraint is a feature.** Deleting a guard, a comment, a dependency, an abstraction is often the highest-value edit available. AI output errs toward addition; craft errs toward subtraction. Audit for what can be removed before adding anything.
4. **Verify the built result, not the intention.** Every check runs against the actual output: the test run read to its exit code, the compiled behavior, the diff as the reader will see it. "I meant to" does not count.

## How to route

Identify what the user is working on, then load the matching reference. Most real requests span tracks — that is expected; run both, in loop order.

| The work | Reference | What it gives you |
| --- | --- | --- |
| Planning or building anything non-trivial — features, bugfixes, refactors, multi-step work | [references/the-process.md](references/the-process.md) | The full loop: brainstorming with hard gates, plan structure, TDD iron law, systematic debugging, review protocol, evidence-before-claims verification, branch finishing |
| Writing or polishing any source code — frontend, backend, fullstack, any language | [references/anti-vibe-code.md](references/anti-vibe-code.md) | The 14-pattern slop taxonomy with severity levels, naming discipline, comment and error-handling rules, language idioms, before/after examples |
| README, docs, UI copy, commit messages, PR descriptions, changelogs | [references/prose-git.md](references/prose-git.md) | AI prose patterns to kill, the stop-slop scoring rubric, conventional commits without AI tells |
| Before delivering anything user-facing | [references/quality-gates.md](references/quality-gates.md) | The phase loop and the pre-emit gates for code and prose (the UI gate lives in the `design` skill) |

Typical combinations:

- "Build this feature" → the-process (brainstorm → plan → TDD loop) → anti-vibe-code (while writing) → quality-gates (pre-emit).
- "This module looks AI-generated, fix it" → anti-vibe-code → quality-gates (code gate).
- "Fix this bug" → the-process Phase 4 (root cause, failing test first) → the commit via prose-git.
- "Write the README for this" → prose-git alone.
- "Make this page look professional" → the `design` skill (RESTYLE) → anti-vibe-code for the component code it touches → this skill's gates before delivery.

## The workflow

One loop serves all tracks:

1. **Read before making.** State in one line what the artifact is for, who uses it, and in what scene — before writing anything. For process work this is the brainstorm gate; for code work it is naming the module's actual job. If you cannot state it in one line, you do not understand it well enough to craft it.
2. **Diagnose against the catalogs.** Walk the existing code against the slop taxonomy; walk the bug against the four debug phases. Flag every finding with its severity. Do not fix yet — see the whole field first.
3. **Prescribe the smallest honest diff.** Group related findings and fix them in batches (all renames together, all dead code together). Never bundle polish with behavior changes; a bug spotted mid-polish gets flagged for a separate change, not fixed here.
4. **Verify behavior survived.** Signatures unchanged or all callers updated, control flow identical, tests pass untouched — *watched failing, then passing* where new tests exist.
5. **Run the gate before delivery.** The pre-emit gates in [references/quality-gates.md](references/quality-gates.md). Score, fix what fails, ship.

## The hard bans

Hybrid rigidity: objective, binary, non-negotiable. Everything subjective lives in the references as explained principles. When a ban conflicts with an explicit user instruction, the user wins — note the override and proceed.

**Process — never:**
- Production code without a failing test that was watched failing first. Code written before its test gets deleted, not adapted.
- A fix attempted before root-cause investigation; a second fix stacked on a failed first.
- A completion claim ("tests pass", "fixed", "done") without the verifying command's fresh output in the current context.
- Building (scaffolding, dependencies, product code) before the human approved the understood scope.

**Code — never ship:**
- Names from the empty set: `data`, `result`, `temp`, `info`, `obj`, `val`, `thing`, `manager`, `handler`, `helper`, `utils`, `processor` when a domain-specific name exists.
- Comments that restate the adjacent code, or AI signature phrases ("certainly", "here's the implementation", "as an AI").
- Silent error swallowing: `except: pass`, `catch { }`, catch-log-and-continue without re-raise or handling.
- Commented-out code (git remembers) and TODO placeholders you could resolve right now.

**Prose and git — never ship:**
- Throat-clearing openers ("here's the thing", "let me be clear"), em-dash cadence, "not X, but Y" binary contrasts.
- AI tells in commit messages: "leverage", "seamlessly", "robust solution" — they live forever in `git log`.

## Calibration, not uniformity

The failure mode this skill must avoid: producing a new template. Perfectly uniform naming, every function documented identically, zero local exceptions — that is also a machine signature. Human codebases have sediment: local idioms, a first-person comment where the codebase does that, one function that is 80 lines because the domain there is genuinely gnarly, a ledgered ruling that broke the plan on purpose. The gates ask "was this decided?", and a *documented* inconsistency passes while an *accidental* one fails. When you choose to break a rule here, do it loudly and once, not timidly and everywhere.

## When NOT to trigger

- Greenfield generation with no quality bar stated and no human-craft requirement — the user wants speed, and that is legitimate. (This skill still applies the moment they say "make it good".)
- Pure backend algorithms, data processing, or infra with no user-facing surface AND no naming/comment polish requested.
- Tasks about correctness only ("fix this bug", "make this test pass") — though the *process* for that fix (Phase 4: root cause + failing test) and its *commit message* are this skill's domain.
- Security audits, test-suite strategy, and multi-language PR review — the sibling sub-skills in this repo (`code-review`, `test-craft`) cover those deeper.
- Visual/UI design work — the sibling `design` skill.

## Attribution

This skill is an original synthesis commissioned for this repo, merging the repo's own sub-skills with seven external sources — six original (including the process track from `obra/superpowers`, MIT © 2025 Jesse Vincent) plus the design lineage now living in the `design` skill. See [ATTRIBUTION.md](ATTRIBUTION.md) for the full list and licenses; upstream material retains its original licenses and is credited in each reference file.
