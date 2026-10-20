# quality-gates — decide before building, verify before shipping

> Merged from: `shinewinsu/vibe-frontend-design` (the decide-before-building principle), `wwewtech/anti-slop-design` (MIT — 5-phase loop), this repo's `code-impeccable` + `stop-slop` (verification layers), and `obra/superpowers` verification-before-completion (MIT — evidence-before-claims gate). The UI-side gates (Design Read, Three Dials, 7-axis UI gate) moved to the `design` skill with the design track. See ATTRIBUTION.md.

Everything in this file exists to force the decisions *before* generation starts, and to catch slop *before* the user sees it. The pattern behind all AI-looking output is skipped decisions; the gates put the decisions back in.

## The one-line read (mandatory first line)

Before writing any code, output one line that pins the work. This closes the escape route to the statistical middle — once the read is stated, every choice has something to be checked against:

> **`Read: building [artifact] for [audience], in [scene], stack [key choices].`**

- `Read: building a dunning module for the billing team, in the invoicing service, stack Python + Postgres + existing ledger client.`
- `Read: building a CSV export for accountants who open it in Excel, in the reports page, stack TypeScript + streaming response.`

If the line cannot be written, the understanding is not there yet. (For UI work, the `design` skill's Design Read adds the visual world and the V/M/D dials on top of this line.)

## The phase loop

```text
Phase 1  Diagnose     scan against the slop taxonomy / the four debug phases; strip clutter
Phase 2  Foundation   state the one-line read, the module's actual job, the invariants
Phase 3  Structure    the smallest honest diff, grouped in batches, TDD where new tests apply
Phase 4  Detail       naming, comments, idioms, error contracts
Phase 5  Gate         score the axes below; any failure loops back to Phase 3 (not 4)
```

Bounded verification: build fully, inspect once with a batched pass, fix everything shown in one batch, confirm with at most one more round, stop. Open-ended self-QA burns budget and degrades the result.

## The process gate (runs on any claim of progress)

**No completion claims without fresh verification evidence.** Before saying "done", "fixed", "passing", or expressing satisfaction:

1. **Identify** the command that proves the claim. 2. **Run** it fresh and complete. 3. **Read** the full output and the exit code. 4. **Verify** the output confirms the claim — then, only then, make it, *with* the evidence.

| Claim | Requires | Not sufficient |
| --- | --- | --- |
| Tests pass | Command output: 0 failures, this run | Previous run, "should pass" |
| Bug fixed | Original symptom tested and passing | "I changed the code that does that" |
| Build succeeds | Exit 0 | Linter passing |
| Subagent finished | VCS diff checked | The agent reported "success" |
| Requirements met | Line-by-line checklist against the plan | Tests passing |

"Should", "probably", "seems to" — all are recall notices that verification was skipped. A red test watched scrolling past and not mentioned is a report falsified by omission.

## The code gate

Run the pre-flight from anti-vibe-code.md and score: HIGH findings weigh 10, MEDIUM 5, LOW 2, normalized per 100 lines. **0–20 clean; 21–40 slightly sloppy — fix the HIGHs at least; 41+ not shippable under this skill.** Plus the binary checks: behavior preserved (tests pass unchanged, signatures intact), no polish mixed with behavior change, and the `git log` test — each hunk's *why* is guessable by a reviewer.

## The prose gate

The five-dimension rubric from prose-git.md (directness, rhythm, trust, authenticity, density), 1–10 each. **≥ 35/50 to ship.** For commits and PR descriptions additionally: imperative subjects, why-bodies, no AI tells in history, testing sections present.

## The final assertion

Before delivering anything under this skill, answer honestly:

> *Does this read as crafted by a disciplined professional with extreme respect for the user's attention — or does any part of it look like it was generated from a prompt?*

If any element feels like prompt-slop: eliminate it, do not soften it. Then ship, and stop polishing. The remaining 2% is not worth the user's patience, and over-polished work starts acquiring its own uniformity tells. Craft ends at *decided and verified* — not at *perfect*.
