# prose-git — prose and git communications without the chatbot cadence

> Merged from: this repo's `stop-slop` (upstream hardikpandya/stop-slop — phrases, structures, scoring) and `commit-craft` (original). See ATTRIBUTION.md.

Prose carries AI tells as reliably as code does, and in git history they are permanent. This track applies to READMEs, docs, UI copy, commit messages, PR descriptions, and changelogs — anything a human will read later.

## The prose rules

1. **Cut filler.** Throat-clearing openers ("here's the thing", "let me be clear", "it turns out"), emphasis crutches ("full stop", "let that sink in", "make no mistake"), and all hedging adverbs ("really", "just", "literally", "genuinely", "simply", "actually", "truly", "fundamentally", "inevitably"). State the point; delete the runway.
2. **Break formulaic structures.** Binary contrasts ("not X, but Y", "the answer isn't X, it's Y", "it's not this, it's that"), negative listing ("not a X... not a Y... a Z"), dramatic fragmentation ("[Noun]. That's it. That's the [thing]."), rhetorical setups ("what if...", "think about it:", "and that's okay"). Each is a telegraphed move the reader sees coming. State Y directly.
3. **Active voice with a human subject.** Passive constructions hide the actor ("mistakes were made"). Worse: *false agency* — inanimate things doing human verbs. Complaints don't "become" fixes; someone fixes them. Decisions don't "emerge"; someone decides. Data doesn't "tell us"; someone reads it and concludes. Markets don't "reward"; buyers pay. Name the human, or use "you".
4. **Be specific.** Vague declaratives ("the reasons are structural", "the implications are significant") name nothing. Lazy extremes ("every", "always", "never") doing vague work. Replace with the specific thing, the specific number, the specific person.
5. **Reader in the room.** "You" beats "people tend to". A scene beats a lecture. Nobody-designed-this narration puts the reader above the action; put them in it.
6. **Vary rhythm.** Mix sentence lengths. Two list items beat three when three is padding. End paragraphs differently. No em-dash cadence — the AI em-dash is the single most recognized punctuation signature in English prose; restructure the sentence instead.
7. **Trust the reader.** No softening, no justification, no hand-holding, no "you already know this, but". If it sounds like a pull-quote, rewrite it.

**Business jargon swaps:** navigate → handle; unpack → explain; lean into → accept; game-changer → significant; deep dive → analysis; moving forward → next; circle back → revisit; on the same page → agreed; leverage → use; seamlessly → (delete; if it were seamless you would not need to say so).

**Sentence starters to restructure:** Wh- openers ("what makes this hard is...") → lead with the subject. Paragraph-initial "So". "Look,". Meta-joiners announcing structure ("the rest of this essay...", "in this section we'll...") → delete and let the piece move.

## The scoring rubric

Rate 1–10 per dimension before delivering any prose:

| Dimension | The question |
| --- | --- |
| Directness | Statements, or announcements of statements? |
| Rhythm | Varied, or metronomic? |
| Trust | Respects the reader's intelligence? |
| Authenticity | Could a person have written this aloud? |
| Density | Is anything cuttable? |

**Below 35/50: revise.** Most first drafts of AI prose land in the 20s; one honest pass with the seven rules above usually clears 40.

## UI copy specifically

Interface copy is prose under constraint, and the constraint helps:

- Controls name their action: "Save invoice", not "Submit" or "Confirm action".
- Errors name the problem *and the recovery*: "The invoice PDF is 12 MB; the limit is 10. Export as CSV instead, or split the batch." Not "Something went wrong".
- Empty states say what will appear here and what to do next: "No invoices yet — create the first one", not "No data" with a shrug emoji.
- No tooltip explaining a button whose label should have explained itself. Fix the label.
- Sentence case on labels and buttons. Tracked-out uppercase eyebrows are on the design banned list; they are also a prose problem — decoration standing in for hierarchy.

## Commit messages

The commit message is for the next reader, six months from now, running `git blame` at 2am. Write for that person.

**Structure:** Conventional Commits prefix (`feat` / `fix` / `docs` / `refactor` / `perf` / `test` / `chore` / `build` / `ci` / `style` / `revert`), optional scope as a single noun (`feat(auth):`), subject ≤ 50 chars in imperative mood ("Add", not "Added" / "Adds" / "I added"), no trailing period. Body wrapped at 72, separated by a blank line, answering *why* — the diff already shows what. Reference issues (`Fixes #482`). Footer for `BREAKING CHANGE:` and `Co-Authored-By:`.

**The good example:**

```
fix(auth): reject expired JWTs before decoding

Previously, the auth middleware decoded the JWT before checking the
`exp` claim. An expired token signed with a valid key passed the
signature check and reached the application, which failed downstream
with a confusing "user not found" error.

This moves the `exp` check before the decode step, returning 401
immediately for expired tokens. Behavior for valid and malformed
tokens is unchanged.

Fixes #482
```

**The slop example — never ship this:**

```
Update auth

In today's fast-paced world, security is paramount. This commit
leverages a robust solution to seamlessly enhance the auth flow,
delivering a truly remarkable improvement to the user experience.
```

The second one lives in `git log` forever, and every future reader learns exactly how that change was made. "Update X" subjects, mixing concerns in one commit, squash-merges that keep every intermediate message — all reviewability failures. Split concerns with `git add -p`; rewrite the squashed message before merging.

## PR descriptions

A PR description is a pitch, not a form. Sections in order, omitting any that do not apply:

1. **Summary** — one paragraph, plain language.
2. **Motivation** — why this change; link the issue.
3. **Changes** — grouped bullets of concrete deltas.
4. **Testing** — commands, screenshots, recordings. Reviewers must never ask "did you test this?".
5. **Screenshots** — for UI changes, always, before *and* after.
6. **Breaking changes** — explicit.
7. **Rollout / rollback** — for risky changes: the flag, the staged plan, the revert procedure.
8. **Reviewer focus** — what specifically to look at. "General review" is not actionable.

## Release notes

Keep-a-Changelog format, written for *users* (not a commit dump — the changelog is not `git log` prettied up):

```markdown
## [1.2.0] - 2026-10-13

### Added
- JWT auth on the user API.
- Dark mode for the dashboard.

### Changed
- Invoice parser now uses a state machine. Behavior unchanged.

### Deprecated
- The `legacyAuth` flag; migrate to `authMode: 'jwt'` before 2.0.

### Fixed
- Expired JWTs no longer pass the signature check.

### Security
- Bumped `jsonwebtoken` to 9.0.0 (CVE-2024-XXXX).
```

Group and rephrase from the user's perspective: what changed *for them*, not which files moved.

## Pre-flight for prose and git

- [ ] Zero throat-clearing openers, zero hedging adverbs, zero em-dash cadence.
- [ ] No "not X, but Y" constructions anywhere.
- [ ] Every sentence has an actor; no false agency ("the culture shifts", "the data tells us").
- [ ] Specifics: numbers, names, paths — at least one per paragraph where claims appear.
- [ ] Rhythm varies; no three consecutive sentences of equal length.
- [ ] Commits: imperative subjects ≤ 50 chars, bodies answer why, no AI tells in `git log`.
- [ ] PRs and notes: reviewer- and user-perspective respectively; testing section present.
- [ ] Scored ≥ 35/50 on the rubric.
