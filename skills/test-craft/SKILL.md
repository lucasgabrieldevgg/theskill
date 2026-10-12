---
name: test-craft
description: "Use when the user wants to write, polish, or audit tests — unit, integration, e2e, or property-based. Covers test naming (behavior-driven, not method-driven), assertion precision (exact matchers over truthy, single behavior per test), edge case coverage (null/empty/off-by-one/concurrent/large inputs), fixture design (minimal, intent-revealing, never shared for unrelated tests), test isolation (no shared mutable state, no order dependency), flakiness elimination (timeouts over sleeps, deterministic data, mocking external calls), and test pyramid discipline (more unit than integration, more integration than e2e). Apply to any language/framework: Jest/Vitest, Pytest, JUnit, Go testing, Rust #[test], RSpec, PHPUnit, Cypress, Playwright. Also use when reviewing a test suite for quality (not just coverage), eliminating redundant tests, refactoring tests alongside the production code they cover (without changing behavior), or building a testing strategy from scratch. Inherits the behavior-preservation rule from code-impeccable: polishing tests must not change what the tests assert. Not for writing production code (use code-impeccable) or polishing commit messages (use commit-craft)."
---

# test-craft — tests that age well

`test-craft` is the skill for making test suites that earn trust. A good test suite is one where a failing test immediately tells you what broke, where, and why — without you reading the test body. Most test suites fail this bar.

## When to use

- The user is writing new tests and asks "what should I test?".
- The user is reviewing a test suite and asks "is this any good?".
- The user is eliminating flaky tests.
- The user is refactoring tests alongside a production code refactor.
- The user is setting up a testing strategy from scratch on a new project.

## The non-negotiable rule

**Test behavior, not implementation.** Tests that reach into private internals (private methods, internal state, mock every collaborator) break on every refactor. Tests that go through the public API survive refactors and still catch regressions. If you must test internals, you have a missing public abstraction — extract it first, then test it.

## How to use

### Step 1 — Understand what you're testing

Identify the unit under test (function, class, module, endpoint, full flow) and its observable behavior (inputs → outputs, side effects, state transitions, error modes). If you can't describe the behavior in one sentence, the abstraction is wrong.

### Step 2 — Diagnose the suite in layers

Walk through tests in this order:

1. **Naming** — Test names should describe behavior, not implementation.
   - `testUserService()` → `createsUser_whenEmailIsValid()` (reveals intent, reads as a spec)
   - `test1()`, `test_method()` → rename to the behavior under test
   - `should*` is fine; `test*` is fine; what matters is that the name answers "what behavior, under what condition, expects what result".

2. **Assertion precision** — Vague assertions hide bugs.
   - `expect(result).toBeTruthy()` → `expect(result.id).toBe('user_123')` (specific value)
   - `expect(list.length).toBeGreaterThan(0)` → `expect(list).toEqual([expectedItem])` (exact content)
   - One assertion per behavior. Multiple assertions are OK if they assert the same behavior from different angles; not OK if they test multiple behaviors in one test.

3. **Coverage of edge cases** — Most bugs live in the edges.
   - Empty input (`[]`, `''`, `null`, `undefined`, `0`)
   - Single element (often off-by-one territory)
   - Boundary values (max int, max length, off-by-one)
   - Concurrent calls (race conditions, double-submit)
   - Large inputs (memory, pagination)
   - Invalid input (wrong type, malformed, injection attempts)
   - External failure (network down, timeout, malformed response)
   - Idempotency (calling twice should not duplicate side effects)

4. **Fixture design** — Fixtures should reveal intent, not hide it.
   - `validUser`, `expiredToken`, `adminWithNoPermissions` — names that explain the scenario.
   - `testData`, `mock1`, `fixture` — names that hide the scenario.
   - Build fixtures per-test when the test cares about specific fields; share fixtures only when the fields are irrelevant to the test.
   - Builders over factories over literals: `userBuilder().withExpiredToken().build()` is more readable than a 50-field object literal.

5. **Isolation** — Tests must not depend on each other.
   - No shared mutable state between tests.
   - No test ordering dependency (running tests in random order must still pass).
   - Each test sets up its own world and tears it down.
   - Database tests use transactions rolled back per test, or a fresh database per test.

6. **Flakiness** — A flaky test is worse than no test, because it trains the team to ignore failures.
   - Replace `await sleep(500)` with `await waitFor(() => expect(...).toBe(...))`.
   - Replace `Date.now()` with an injectable clock.
   - Replace `Math.random()` with a seeded PRNG or injected value.
   - Mock external network calls — never hit real third-party APIs in tests.
   - Replace implicit waits with explicit conditions (element visible, network idle, state updated).

7. **Test pyramid** — Most tests should be unit tests; few should be e2e.
   - **Unit** (fast, isolated, ~70% of suite) — pure logic, no I/O.
   - **Integration** (medium speed, real dependencies for one layer, ~20%) — DB, internal APIs, file system.
   - **E2E** (slow, full system, ~10%) — user flows through the real UI/API.
   - Inverted pyramid (lots of e2e, few unit tests) is the most common anti-pattern; it produces slow, flaky suites.

### Step 3 — Prescribe

For each issue, propose the smallest change that fixes it. Group related changes. Never bundle a test polish with a behavior change — if a test starts failing after polish, you changed what it asserts.

### Step 4 — Verify behavior is preserved

After polishing:
- Did any test start passing that previously failed? You weakened an assertion.
- Did any test start failing? You changed what it asserts.
- Did coverage drop? You may have removed a test for the wrong reason. (Coverage is a floor, not a ceiling — but a sudden drop signals a deleted test.)

## Common anti-patterns to flag

- **"Should not throw"** as the only assertion — tells you nothing about correctness. Replace with assertions on the actual output.
- **Testing the mock instead of the unit** — `expect(mockFunction).toHaveBeenCalledWith(...)` is fine when verifying the unit's interaction with a collaborator, but the test must also assert the unit's own return value or state change.
- **Giant tests with multiple `it()`-worth of behavior** — split into multiple tests, each with a single behavior.
- **Setup that does too much** — a `beforeEach` that builds the entire world signals the unit under test has too many collaborators. Either extract an abstraction or split the unit.
- **Snapshot testing for everything** — snapshots are good for large serialized outputs (rendered HTML, JSON); they're noise for logic. A snapshot test that fails on every minor change is no test at all.
- **`expect.assertions(N)` to "ensure" all assertions ran** — usually a sign of fragile async testing. Prefer `waitFor` or explicit await.
- **Testing private methods** — go through the public API. If the private method has complex behavior worth testing, it's probably its own class.
- **100% coverage as a goal** — 100% coverage with shallow tests is worse than 80% with deep tests on the risky paths. Cover the risky code first.

## When NOT to use

- Writing production code (use `code-impeccable` for polish, or just write the code).
- Reviewing production code quality (use `code-review`).
- Polishing commit messages for test changes (use `commit-craft`).

## References

Place deeper reference docs in `references/` — e.g., `references/frameworks/jest.md`, `references/frameworks/pytest.md`, `references/flakiness-checklist.md`, `references/test-pyramid.md`. Load when the user is working in a specific framework or asks for deeper patterns.
