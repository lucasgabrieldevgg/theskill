---
name: code-impeccable
description: "Use when the user wants to polish, refine, tighten, audit, or refactor source code WITHOUT changing its observable behavior. Covers naming (variables, functions, types, files), dead code removal, structural improvements (function size, cyclomatic complexity, single-responsibility), idiomatic patterns for the language at hand, readability (comments that explain why not what, clear control flow, obvious data shapes), duplication removal, and signature simplification. Apply to any language: TypeScript/JavaScript, Python, Go, Rust, Java, C#, Ruby, Swift, Kotlin, SQL, shell. Also use when reviewing a PR for code quality (not correctness), preparing code for open-source release, paying down technical debt in a focused pass, or onboarding-friendly refactors. Not for fixing bugs, adding features, or changing runtime behavior — that's regular development work, not polish. Not for UI/visual concerns (use impeccable) or commit-message quality (use commit-craft)."
---

# code-impeccable — code polish without behavior change

`code-impeccable` is the skill for making code read like it was written by someone who cares. The contract is strict: the observable behavior must not change. Polish is about clarity, not correctness.

## When to use

- The user says "this code is messy", "tighten this up", "refactor for readability", "clean this up".
- Preparing code for review, open-source release, or onboarding new contributors.
- Paying down technical debt in a focused, low-risk pass.
- Reviewing a PR for code quality (not correctness — that's a different review).

## The non-negotiable rule

**Behavior is preserved.** Every refactor in this skill is a behavior-preserving transformation. If you're tempted to "fix" a bug while polishing, stop — flag it for a separate change. Mixing polish with behavior changes makes review impossible and breaks trust in the polish pass.

## How to use

### Step 1 — Understand the code's job

Before changing anything, articulate (to yourself, then to the user) what this code does. If you can't describe it in one sentence, you don't understand it well enough to polish it. Read the tests if any exist — they're the spec.

### Step 2 — Diagnose in layers

Walk through the code in this order. Each layer is independent — flag issues at one before moving to the next.

1. **Naming** — Are names accurate, specific, and unambiguous?
   - `data` → `userProfiles` (specific)
   - `processItem` → `validateInvoice` (reveals intent)
   - `flag` → `isAuthenticated` (boolean reads as a question)
   - `tmp` → delete or rename to its actual role
   - Single-letter variables only inside 3-line lambdas, nowhere else.

2. **Dead code** — Anything not reachable or not used.
   - Commented-out code (delete — git remembers).
   - Unused imports, variables, private functions.
   - Unreachable branches after early returns.
   - Parameters that are always ignored.

3. **Structure** — How the code is organized.
   - Functions longer than ~30 lines usually hide a missing abstraction.
   - Cyclomatic complexity above ~10 usually means a function is doing too much.
   - Deep nesting (3+ levels) usually wants an early return or a guard clause.
   - A function whose name doesn't match what it does — rename or split.

4. **Duplication** — Same logic appearing multiple times.
   - True duplication: extract to a shared function.
   - Near-duplication: parametrize, but only if the parametrized version is genuinely clearer than the originals.
   - Coincidental similarity (looks the same, means different things): leave alone — forcing a shared abstraction makes both call sites harder to read.

5. **Idioms** — Is the code written in the language's idiomatic style?
   - Python: list/dict comprehensions over loops where appropriate, `if __name__ == "__main__":`, type hints on public APIs.
   - TypeScript: prefer `type` for unions and `interface` for objects, avoid `any`, use `unknown` + narrowing for untrusted input.
   - Go: early returns, error wrapping with `%w`, table-driven tests, no chained ternaries (they don't exist).
   - Rust: borrow checker-friendly patterns, `?` for error propagation, avoid `unwrap()` in non-test code.

6. **Comments** — Comments should explain *why*, not *what*.
   - Delete comments that restate the code: `// increment i` over `i += 1`.
   - Keep comments that explain non-obvious *why*: business rules, performance trade-offs, workaround context.
   - Convert "what" comments into better names whenever possible.

### Step 3 — Prescribe

For each issue, propose the smallest diff that fixes it. Group related changes (e.g., "rename `tmp` → `invoice`, `data` → `userProfiles`, `flag` → `isAuthenticated` — all in `userService.ts`"). Never bundle polish with behavior changes — if you spot a bug while polishing, note it for a separate commit, don't fix it here.

### Step 4 — Verify behavior is preserved

Before delivering, sanity-check:

- Did any function signature change in a way that affects callers? If yes, update all callers or revert.
- Did any control flow change? It shouldn't — re-extracting an early return is OK, adding a new branch is not.
- Did any test need to change? Tests should pass unchanged. If a test broke, you changed behavior — revert that part.

## Common anti-patterns to flag

- **Premature abstraction** — extracting a "shared" function that has only two call sites with divergent needs. Usually worse than the duplication.
- **Comment-as-documentation for trivial code** — `// returns true if user is admin` over `function isAdmin(user) { return user.role === 'admin'; }` is noise.
- **Defensive null checks where the type system already proves non-null** — `if (user && user.id && user.id !== null)` when the type is `User` with non-optional `id`.
- **Configuration via boolean parameters** — `createUser(data, false, true, false)` is unreadable; use an options object or split into two functions.
- **Stringly-typed enums** — `if (status === 'pending' || status === 'processing')` should be a typed enum or union with a Set lookup.
- **Catch-all exception handlers** — `catch (e) { console.error(e); }` swallows bugs. Either handle, rethrow, or fail loudly.

## When NOT to use

- Fixing bugs — that's regular development.
- Adding features — same.
- Changing runtime behavior — same.
- UI/visual polish — that's `impeccable`.
- Refactoring commit messages or PR descriptions — that's `commit-craft`.

## References

Place deeper reference docs in `references/` — e.g., `references/idioms-typescript.md`, `references/idioms-python.md`, `references/refactor-catalog.md` with the Fowler-style catalog of behavior-preserving transformations. Load when the user is working in a specific language or asking for a deeper pattern reference.
