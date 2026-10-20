# the-process — the execution discipline: spec, plan, TDD, debug, review, verify

> Merged from: `obra/superpowers` (MIT, © 2025 Jesse Vincent — skills brainstorming, writing-plans, executing-plans, subagent-driven-development, test-driven-development, systematic-debugging, verification-before-completion, requesting-code-review, receiving-code-review, finishing-a-development-branch), adapted to this repo's craft framing. See ATTRIBUTION.md.

Vibe coding has two faces: the artifact face (empty names, ghost comments, swallowed errors — the S-taxonomy in [anti-vibe-code.md](anti-vibe-code.md)) and the **process face**: building before understanding, fixing before diagnosing, claiming before verifying. This track is the cure for the second. It is a complete loop, and each phase exists because its absence has a named failure mode.

```
brainstorm → written design → implementation plan → execute (TDD) → review → verify → finish
```

Small tasks run the loop compressed in chat; real projects run it as files. The phases compress; none is skipped.

## Phase 1 — Brainstorm: what do they actually want?

Before any creative work, find out what the human actually wants and why. **People rarely have finished deciding what they want; good questions help them think it through.** When you understand the why, you make the hundred decisions they never mention the way they would have made them.

- First message: one line offering to skip the questions ("if you'd rather I just start, say so"), then **one open question that gets them describing** — anchored in specifics: "What's the moment you find yourself wishing this existed?", "Walk me through the last time this bit you." A guess they can correct often beats a question.
- Ground to cover (territory, never a questionnaire read aloud): what kind of thing and what makes it special · why now, and what success looks like · goals, non-goals, and anti-goals (what would make this a failure even if it works) · prior art they loved or hated · the details they care about. How-it-gets-made choices (stack, libraries): find out early which they want to decide and which they hand to you — a default they never heard is one they couldn't reject.
- **Play it back as you go**: as soon as one part is understood, describe it back in 200–300 words, mark guesses as guesses, end by asking what's wrong or missing.
- **Size the work** and say it in plain words: a quick clear task (do it) · a small change (chat-level, normal workflow) · a project (a written design a builder could plan from — covering intent, goals/non-goals/anti-goals, constraints, decided-how choices, what's left to the builder). If it grows mid-task, stop, say so, step up a size.
- **HARD GATE: nothing gets built until the human approves** — the chat description for small work, the written design for a project. Building includes scaffolding, dependencies, and product code. Reading and exploring are fine.

## Phase 2 — Plan: decisions the implementer can't make alone

A plan is for an engineer who has not seen this codebase or this spec. Assume they write idiomatic code once they know the exact interface and the exact test; what they cannot know is what you decided: which files, which names and signatures, which tests prove each task.

- **Bite-sized tasks** (2–5 minutes each), each ending in an independently testable deliverable; each task states Files (exact paths), Interfaces (consumes/produces — exact signatures), and steps.
- **A step is one action with a checkable result**: "write the failing test" · "run it, verify it fails for the right reason" · "implement the minimal code" · "run it, verify pass" · "commit". A step is done when the implementer can write exactly one reasonable thing from it — unambiguous, not complete.
- Header carries Global Constraints (spec's project-wide rules verbatim) and a **Review Focus**: the input classes the spec implies but no task's tests exercise — the five most likely to bite a user, each pinned to a test in the task that owns it.
- **Self-review before handoff**: spec coverage (every requirement has a task) · no step that decides nothing ("handle edge cases" is a gap) and no code body the signature+tests already determine (a transcript) · type consistency across tasks · proportion (a plan several times longer than the spec has written the code instead).
- Handoff: the human reviews the plan and picks the execution approach — **subagent-driven** (fresh implementer + fresh reviewer per task; most thorough) or **inline** (one context, one final fresh review; cheapest). The plan's interface density decides it.

## Phase 3 — Execute: TDD is the per-task gate

**The Iron Law: no production code without a failing test first.**

1. **RED** — write one minimal test with a clear name, real code (no mocks unless unavoidable), asserting the spec's exact values.
2. **Verify RED** — run it, *watch it fail*, confirm it fails because the feature is missing (not a typo). A test that passes before the implementation exists is a finding about the test. **Skip this step and you know nothing about whether the test tests the right thing.**
3. **GREEN** — the simplest code that passes. No "while I'm here", no options object nobody asked for (YAGNI).
4. **Verify GREEN** — the test passes, **and the project's whole suite passes**, output read (not scrolled past). A red test watched scroll past and unmentioned is a report falsified by omission.
5. **REFACTOR** — after green only: remove duplication, improve names. Tests stay green.
6. **Commit.** Frequent, small.

**Code written before its test gets deleted, not "adapted" or "kept as reference."** Deleting means delete. Exceptions (throwaway spikes, config) are stated, not assumed. The rationalizations all die the same death: "I'll test after" (tests-after verify the cases you remembered, never the ones you'd have discovered), "too simple to test" (simple code breaks), "TDD will slow me down" (guess-and-check debugs in production — slower).

**Inline execution discipline** (when running the plan yourself): the plan already did the thinking — execute it exactly. **Rulings, not stalls**: conflicts and plan defects get decided, recorded as `Ruling: <decision> — <why> — <cost if wrong>` in a progress ledger, and execution continues; an unledgered deviation is a decision made in secret. Progress lives in a ledger file, not memory — a compacted session that re-implements tasks whose commits already exist paid for its amnesia. Only four things stop execution: irreversible/destructive operations, security-sensitive actions, side effects outside the workspace (merge, push, publish), and a plan so broken every path is a guess.

**Dispatching parallel agents** applies only to genuinely independent tasks (no shared state, no sequential dependencies); shared files mean no parallelism.

## Phase 4 — Debug: root cause before any fix

**The Iron Law: no fixes without root-cause investigation first.** Symptom fixes are failure.

1. **Root cause** — read the error completely (it often contains the solution); reproduce consistently (not reproducible = gather data, don't guess); check recent changes (git diff, new deps); in multi-component systems, instrument the boundaries — log what enters and exits each layer, run once, see WHERE it breaks, then investigate that layer; trace bad values upstream to their source and fix at the source.
2. **Pattern** — find working examples of the same thing in the codebase; list every difference from the broken one, however small.
3. **Hypothesis** — one at a time, stated ("I think X because Y"), tested with the smallest possible change. Didn't work → new hypothesis, never another fix stacked on top.
4. **Implementation** — failing test reproducing the bug FIRST (TDD applies to fixes), one change, verify the fix, verify nothing else broke.

**If 3+ fix attempts have failed: STOP — that is an architecture problem, not a hypothesis problem.** Each fix revealing a new shared-state or coupling issue somewhere else is the signature. Question the pattern itself, with the human, before attempting fix #4. "It's probably X, let me fix that" and "quick fix now, investigate later" are Phase-1 recall notices.

## Phase 5 — Review: fresh eyes, crafted context

Request review after each task (subagent mode), after major features, and before any merge. **The reviewer gets precisely crafted context, never your session's history**: what was built, the requirements, BASE_SHA..HEAD_SHA. You are the coordinator — reviewing your own diff inline burns the context you need to keep driving; dispatch the review so the diff and the evaluation live in a fresh context and only the findings come back.

Act on findings by severity: **Critical** blocks progress (fix now), **Important** fixes before proceeding, **Minor** notes for later. Re-grade before acting: a finding's real grade is what a user of the software gets if it ships — not whether the spec happened to mention the input that triggers it.

**Receiving review** (from humans or reviewers): technical evaluation, not emotional performance. **Never performative agreement** — "You're absolutely right!", "Great point!", gratitude rituals — restate the requirement or just fix it and let the code show you heard. Verify before implementing: is this correct for THIS codebase, does it break anything, does the reviewer have full context? **Unclear items stop everything** — clarify first, because items may be related and partial understanding is wrong implementation. Push back with technical reasoning when the suggestion is wrong (breaks function, YAGNI — grep for actual usage: "nothing calls this; remove it instead?", legacy constraints, conflicts with the human's architecture). When you pushed back and were wrong: state the correction factually, no apology theater, move on.

## Phase 6 — Verify: evidence before claims, always

**The Iron Law: no completion claims without fresh verification evidence.** If you haven't run the command in this message, you cannot claim it passes.

| Claim | Requires | Not sufficient |
| --- | --- | --- |
| Tests pass | Command output: 0 failures, this run | Previous run, "should pass" |
| Bug fixed | Original symptom tested and passing | "Code changed" |
| Build succeeds | Exit 0 | Linter passing |
| Subagent finished | VCS diff checked | Agent says "success" |
| Requirements met | Line-by-line checklist | Tests passing |

"Should", "probably", "seems to", satisfaction expressed before verification — all recall notices. This is the code-side sibling of the craft contract's *verify the built result, not the intention*.

## Phase 7 — Finish: integration is the human's decision

Tests green on the tree about to be integrated (a green run only proves the tree it ran on) → present the menu exactly: **1. merge locally** (then verify tests on the merged result) · **2. push and open a PR** (worktree stays for feedback fixes) · **3. keep as-is**. Wait for the answer. Discarding work happens only on an explicit request, confirmed by the typed word. Never force-push, never clean up worktrees that aren't yours, never "obviously they want it merged".

## Why this track lives beside the code track

The S-taxonomy flags the artifact; the process prevents the next one. S3 god functions happen when nothing forces boundaries at planning time; S9 swallowed errors happen when "it should work" replaced a watched-failing test; S13 TODO graveyards happen when work stopped being ledgered; S14 uniformity happens when no ruling was ever recorded or deviated from on purpose. Run this loop and the taxonomy finds less to flag — that is the point.
