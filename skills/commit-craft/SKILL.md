---
name: commit-craft
description: "Use when the user wants to write, improve, or audit git communications: commit messages, PR descriptions, release notes, changelogs, or branch names. Covers Conventional Commits (feat/fix/docs/refactor/perf/test/chore/build/ci/style/revert), structured PR descriptions (summary, motivation, changes, testing, screenshots, breaking changes, rollback plan), semantic versioning decisions (patch/minor/major), Keep-a-Changelog format, and branch naming conventions (git-flow, GitHub flow, trunk-based). Apply whenever the user is about to commit, open a PR, cut a release, or prepare a changelog — even if they don't explicitly ask for 'crafting' or 'polishing' the message. Also use for reviewing someone else's commit history to make it more reviewable and bisectable. Inherits anti-slop principles from stop-slop: commit messages and PR descriptions are prose too, and AI tells in git history are particularly embarrassing. Not for code changes themselves (use code-impeccable) or for general prose (use stop-slop)."
---

# commit-craft — git communications that age well

`commit-craft` is the skill for writing the human-facing parts of git: commit messages, PR descriptions, release notes, changelogs. These artifacts live forever in the history — they should be as readable in 18 months as they are today.

## When to use

- The user is about to commit and asks for a commit message.
- The user is opening a PR and asks for the description.
- The user is cutting a release and asks for release notes.
- The user is reviewing a messy commit history and wants to clean it up (interactive rebase, squashing).
- The user asks "is this a good commit message?".

## Core principles

1. **The commit message is for the next reader, not for you.** Six months from now, someone (maybe you) will run `git blame` on a line and read the commit message to understand *why* this line exists. Write for that person.
2. **Subject line: what changed, in imperative mood.** "Add JWT auth to user API" — not "added" (past tense, redundant with the commit), not "adds" (third person), not "I added" (no first person).
3. **Body: why it changed, what the alternatives were, what the side effects are.** The diff already shows *what*; the body explains *why* — the context that's invisible in the code.
4. **PR description: the pitch.** Reviewers shouldn't have to reverse-engineer your intent from the diff. Tell them what you're trying to do, why, how you did it, how you tested, and what they should look at.
5. **No AI tells.** Commit messages that say "leverage", "seamlessly", "robust solution" are embarrassing in `git log`. Inherit `stop-slop`'s principles — apply them to the constrained format of git communications.

## How to use

### For commit messages

1. Read the diff. Group the changes into logical commits if there's more than one concern mixed in (a common problem). Suggest splitting with `git add -p` if needed.
2. Identify the primary change type for the Conventional Commits prefix:
   - `feat` — new user-facing capability
   - `fix` — bug fix
   - `docs` — documentation only
   - `refactor` — code change that neither fixes a bug nor adds a feature
   - `perf` — code change that improves performance
   - `test` — adding or correcting tests
   - `chore` — build, deps, config, tooling
   - `build` — build system or external dependencies
   - `ci` — CI configuration
   - `style` — formatting, whitespace (no code logic change)
   - `revert` — reverting a previous commit
3. Identify the scope (optional but encouraged): `feat(auth):`, `fix(parser):`, `docs(readme):`. The scope should be a single noun identifying the part of the codebase.
4. Write the subject line:
   - Imperative mood: "Add", "Fix", "Refactor", "Remove".
   - ≤50 characters (soft limit; ≤72 hard).
   - No trailing period.
   - Specific: "Add JWT auth" not "Update auth".
5. Write the body (if the change needs explanation):
   - Wrap at 72 characters.
   - Blank line between subject and body.
   - Answer: why is this change necessary? What does it do? How does it differ from the previous behavior? What alternatives were considered?
   - Reference issues: `Fixes #123`, `Refs #456`, `Closes #789`.
6. Add a footer for breaking changes or co-authors:
   - `BREAKING CHANGE: <description>` (or `BREAKING CHANGE:` in the footer for Conventional Commits 1.0).
   - `Co-Authored-By: Name <email>` for pair-programmed commits.

**Example — good:**

```
fix(auth): reject expired JWTs before decoding

Previously, the auth middleware decoded the JWT before checking the
`exp` claim. An expired token signed with a valid key would pass the
signature check and reach the application, which then failed
downstream with a confusing "user not found" error.

This moves the `exp` check to before the decode step, returning a
401 immediately for expired tokens. Behavior for valid and
malformed tokens is unchanged.

Fixes #482
```

**Example — bad (do not do this):**

```
Update auth

In today's fast-paced world, security is paramount. This commit
leverages a robust solution to seamlessly enhance the auth flow,
delivering a truly remarkable improvement to the user experience.
```

### For PR descriptions

A good PR description has these sections (omit any that don't apply):

1. **Summary** — one paragraph, plain language. What does this PR do?
2. **Motivation** — why is this change needed? Link the issue/ticket.
3. **Changes** — bullet list of the concrete changes, grouped logically.
4. **Testing** — how did you verify this works? Include test commands, screenshots, or recording.
5. **Screenshots / Recordings** — for UI changes, always.
6. **Breaking changes** — explicitly call out anything that breaks downstream.
7. **Rollout plan** — for risky changes, how do we roll out? Feature flag? Staged?
8. **Rollback plan** — if this needs to be reverted, what's the procedure?
9. **Reviewers** — what specifically should reviewers focus on? "General review" is not actionable.

### For release notes / changelogs

Use Keep-a-Changelog format:

```markdown
## [1.2.0] - 2026-10-12

### Added
- JWT auth on the user API.
- Dark mode for the dashboard.

### Changed
- Refactored invoice parser to use a state machine. Behavior unchanged.

### Deprecated
- The `legacyAuth` flag will be removed in 2.0. Migrate to `authMode: 'jwt'`.

### Removed
- The `v1/users` endpoint (deprecated since 0.9).

### Fixed
- Expired JWTs no longer pass the signature check.

### Security
- Bumped `jsonwebtoken` to 9.0.0 (CVE-2024-XXXX).
```

### For semantic versioning

- **Patch (0.0.X)** — bug fixes only, no new features, no breaking changes.
- **Minor (0.X.0)** — new features, backward-compatible.
- **Major (X.0.0)** — breaking changes.

Pre-1.0 versions (0.x.y) are exempt from the strict breaking-change rule — minors can include breaking changes. Once you hit 1.0, the rules apply.

## Common anti-patterns to flag

- **"Update X"** as a commit subject — tells the reader nothing they couldn't infer from the file list. Replace with what *about* X changed.
- **Mixing concerns in one commit** — a refactor + a feature + a fix all in one commit. Split into three.
- **Commit message that just says "fix"** — the diff is the "what", the message is the "why".
- **PR description with no testing section** — reviewers shouldn't have to ask "did you test this?".
- **Release notes that list every commit** — changelog is for *users*, not for *developers*. Group and rephrase from the user's perspective.
- **AI tells in commit messages** — "leverage", "seamlessly", "robust" — these live forever in `git log` and age badly.
- **Squash-merges without rewriting the message** — the squashed commit gets a list of all the intermediate messages, which is noise. Rewrite the final message before squash-merging.

## When NOT to use

- Polishing the code itself — that's `code-impeccable`.
- General prose (README content, blog posts) — that's `stop-slop`.
- UI changes — that's `impeccable` (though the *commit message* for a UI change is this skill's domain).

## References

Place deeper reference docs in `references/` — e.g., `references/conventional-commits-spec.md`, `references/keep-a-changelog.md`, `references/rebase-recipes.md` for interactive rebase workflows to clean up history before push. Load when the user asks for spec details or for rebase/squash workflows.
