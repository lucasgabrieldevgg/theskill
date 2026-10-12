# anti-vibe-code — the code track

> Merged from: this repo's `code-impeccable` (original), `vibe-slop-detector` TAXONOMY.md (ericchen931209, MIT), and detection research from Pangram Labs' code-forensics writeups. Upstream licenses apply to their material — see ATTRIBUTION.md.

The code this track produces should read like it was written by someone who has shipped in this domain for years: names that carry domain meaning, comments only where understanding is genuinely at stake, errors that fail loudly with a path to recovery, and structure sized to the problem.

## Why AI code is recognizable

Programming languages have fewer degrees of freedom than prose, so the tells are *structural*, not stylistic: the distribution of names, the ratio of comments to code, the shape of error handling, the uniformity of style. Detectors pick up on statistical regularities that human code violates naturally. The fourteen patterns below cover nearly everything that makes code read as generated. Severity levels mirror the upstream taxonomy: **HIGH** (strong AI signal or actively harmful), **MEDIUM** (common slop, context-dependent), **LOW** (minor signal).

## The 14-pattern slop taxonomy

### S1 — Ghost Comment (MEDIUM)
A comment that restates what the adjacent code obviously does. Adds zero information; announces that nobody was thinking when it was written.

```python
# Slop
counter += 1        # increment counter by 1
return result       # return the result

# Craft
counter += 1
return result
```

**Signal:** comment content maps 1:1 to the expression on the same or next line.

### S2 — AI Signature Phrase (HIGH)
Assistant phrases that leaked into comments, docstrings, or string literals.

```python
# Slop
# Certainly! Here's the implementation:
# Of course, I'd be happy to help with that.

# Craft — no comment at all, or a real one:
# Billing rounds half-up because the ledger must never undercharge.
```

**Signal:** regex hits on `certainly`, `of course`, `as an ai`, `i'd be happy`, `i cannot`, `i'm sorry`, `sure!`, plus section-divider comment banners (`# ===== Helpers =====`) and emoji-headed comment blocks.

### S3 — God Function (HIGH)
One function doing fetch, validate, transform, persist, notify, and log in 120 lines. Generation dumps logic into a single block because nothing forces a boundary.

**Thresholds:** body > 50 lines = MEDIUM, > 100 lines = HIGH; > 7 parameters = MEDIUM.

**Craft:** split at the seams where a test would want to assert independently — parse, decide, act, report. Each piece becomes namable and testable.

### S4 — Dead Import (LOW)
Modules imported and never referenced. Generated code carries speculative imports the way a tourist over-packs.

**Signal:** AST import nodes with zero name references in the file. Delete them; the linter that would have caught this was clearly not run.

### S5 — Copy-Paste Clone (HIGH)
Near-identical blocks duplicated in the same file. Generation rewrites the same idea instead of factoring it — it does not *notice* similarity.

**Signal:** token-level similarity > 80% between two function bodies. Exception: coincidental similarity (looks the same, means different things) stays separate — forcing a shared abstraction makes both call sites harder to read.

### S6 — Generic Naming (MEDIUM)
The empty-name set: `data`, `result`, `temp`, `tmp`, `info`, `obj`, `val`, `value`, `item`, `thing`, `manager`, `handler`, `helper`, `utils`, `util`, `processor`, `service`, `controller`. Generation defaults to these when it lacks domain context — which is exactly when it should have gone looking for the domain's vocabulary instead.

```python
# Slop
def process(data):
    result = []
    for item in data:
        temp = item.get("value")
        result.append(temp)
    return result

# Craft — the domain appears in the names
def extract_prices(products):
    return [p["price"] for p in products]
```

**Naming discipline (from code-impeccable):**
- `data` → `userProfiles`; `processItem` → `validateInvoice`; `flag` → `isAuthenticated` (booleans read as questions).
- Single-letter names only inside 3-line lambdas.
- File names carry the artifact, not the pattern: `invoice_due_dates.py`, not `utils2.py`.
- A name is finished when a newcomer can guess the unit and the domain from it: `dunningLevel`, `writeOffWindow`, `vatRateForCountry`.

### S7 — Void Abstraction (LOW)
A function whose entire body is one pass-through call: `def get_user_name(user): return user.name`. Adds a layer and no value. Exception: single-line adapters that perform real coercion or isolate a contract worth isolating — those earn their line.

### S8 — Magic Number (MEDIUM)
Bare literals in logic: `if response.status == 200`, `time.sleep(3)`, `len(data) > 1000`. Name the concept the number represents: `HTTP_OK`, `RETRY_DELAY_SECONDS`, `MAX_BATCH_SIZE`. Exceptions: `0`, `1`, `-1` and obvious idioms (`2` for halves).

### S9 — False Safety Net (HIGH)
The signature AI failure: error handling that "handles" by swallowing.

```python
# Slop — three faces of the same failure
try:
    risky_operation()
except:
    pass

try:
    risky_operation()
except Exception as e:
    print(e)          # log-and-continue is still a swallow

try:
    risky_operation()
except Exception:
    pass
```

**Craft:** errors either (a) get handled with a real recovery the caller can use, (b) get wrapped and re-raised with the context the next layer needs, or (c) crash loudly because failing fast is correct. A bare `except:` catching `BaseException` including `KeyboardInterrupt` is never right.

### S10 — Verbosity Inflation (MEDIUM)
Simple task, exploded logic.

```python
# Slop
def is_even(n):
    remainder = n % 2
    if remainder == 0:
        return True
    else:
        return False

# Craft
def is_even(n):
    return n % 2 == 0
```

Intermediate variables with no explanatory value, `if x: return True else: return False` — all of it reads as padding. Conciseness here is not golf; it is the honest size of the idea.

### S11 — Redundant Docstring (LOW)
`def add(a, b): """Add a and b."""` — the docstring restates the signature. A docstring earns its lines when it carries what the signature cannot: units, invariants, side effects, why it wraps what it wraps. `"""Compute element-wise addition; wraps numpy.add for type-safe inputs."""` is worth keeping.

### S12 — Defensive Over-checking (LOW)
Guarding states the control flow already rules out: `if x is not None and x != None`, `if len(arr) > 0` where `if arr:` is the idiom, `== True`, checking types the type system already proves. Defensive checks against *documented* external input are craft; defensive checks against your own invariants announce that nobody trusts the code — including its author.

### S13 — TODO Graveyard (LOW)
`# TODO: add error handling`, `# FIXME: might break on edge cases`, `# HACK: temporary` — placeholders the generator never intended to fill. **Threshold:** 3+ per file = LOW signal, 7+ = MEDIUM. Either resolve it now or write a real issue link: `# TODO(ln-241): retry budget, tracked in BILL-1187`.

### S14 — Uniform Machine Signature (MEDIUM)
The inverse tell: *too perfect*. Every function has a docstring; every comment is the same voice and length; naming convention applies with zero local exceptions; every file is the same length. Human codebases have sediment: local idioms, a first-person comment where that section was fought over, one function that is 80 lines because the domain there is genuinely gnarly. Calibrate: match the surrounding codebase's *existing* dialect, and where you deviate deliberately, do it once and own it. A TODO with a ticket number is human; a TODO without one is slop.

## Language idioms (craft floor per stack)

Fullstack coverage, condensed from code-impeccable's layer 5. The test for every item: does this read like the language's native speakers wrote it?

- **TypeScript/JavaScript:** `type` for unions, `interface` for object shapes; no `any` — `unknown` plus narrowing for untrusted input; early returns over nested conditionals; async/await over raw promise chains; result-typed errors at API boundaries.
- **Python:** comprehensions over accumulate-loops where the result is the point; `if __name__ == "__main__":`; type hints on public APIs (and only public — hinting every private helper is a uniformity tell); `pathlib` over string paths; `logging` over `print` in anything that ships.
- **Go:** error wrapping with `%w`; early returns; table-driven tests; no empty `interface{}` when a concrete type fits; `context.Context` as first parameter on anything that can block.
- **Rust:** `?` for propagation; no `.unwrap()` outside tests; `match` with meaningful arms, not `_ => {}` swallowing the rest; ownership that reads like the design, not like a fight with the borrow checker.
- **SQL:** explicit column lists, never `SELECT *` in shipped code; JOINs that the query plan can actually use; constraints in DDL, not in hope.
- **Java/C#:** records/DTOs for data, not god-objects; nullability expressed in the type system, not in Javadoc apologies.

## Comments — the complete rule

Comments should explain *why*, never *what*. Delete what-comments and let names carry them. Keep and write why-comments for: business rules with invisible logic ("VAT is charged on delivery address, not billing"), performance trade-offs ("single query: the list view is called 40x more than the detail view"), workaround context with links ("upstream bug, see LIB-987; remove at v3"), and warnings ("not thread-safe: the scheduler calls this from two threads"). First person is fine where the codebase already writes that way. Section-divider banners and emoji headers: delete.

## Structure — diagnosing before cutting

Walk in this order, flagging without fixing (from code-impeccable's layered diagnosis): **naming → dead code (unreachable branches, unused params, commented-out blocks) → structure (functions > ~30 lines hiding a missing abstraction, complexity > ~10, nesting 3+ wanting a guard) → duplication (true / near / coincidental — only the first two merge) → idioms → comments.** Then prescribe the smallest diff per finding, grouped: all renames in one batch, all dead code in another. A bug found mid-polish is *flagged*, never fixed in the same change — mixing polish with behavior changes makes the diff unreviewable and destroys trust in the polish pass.

## Before/after — a full pass

```typescript
// Slop — S6, S9, S10, S1, S14 all at once
// Helper function to process the data
async function processUserData(userId: string) {
  let result: any = null;
  try {
    const data = await fetchUser(userId);
    const isValid = await validateUserData(data);
    if (isValid == true) {
      result = await saveUserData(data);
      return true;
    } else {
      return false;
    }
  } catch (e) {
    console.error(e);
    return false;
  }
}
```

```typescript
// Craft — the domain shows up, errors mean something
export async function activateAccount(
  userId: string,
): Promise<ActivationResult> {
  const user = await fetchUser(userId); // throws UserNotFound — caller shows the 404

  if (!user.emailVerified) {
    return { status: "rejected", reason: "email-unverified" };
  }

  await grantAccess(user.id, Role.member);
  return { status: "activated", role: Role.member };
}
```

What changed and why it reads human: the name is a domain action, not a pattern; the boolean soup became a typed result the caller can switch on; the swallow became a documented throw plus an explicit rejection path; the `== true` and intermediate flags are gone because the code now says what it means. Nothing here needed a comment — except the throw note, which explains a *contract*, not the code.

## Pre-flight for code

Before calling any code done, check:
- [ ] Zero hits on the hard-ban list (S2 phrases, silent swallows, commented-out code, empty-set names with domain names available).
- [ ] Every comment in the diff explains why or states a contract; nothing narrates.
- [ ] Error paths: every failure either recovers, rethrows with context, or fails fast on purpose — none print-and-continue.
- [ ] The diff contains no behavior change mixed into polish.
- [ ] Read the diff as `git log --oneline` will show it: could a reviewer guess *why* for each hunk?
- [ ] One deliberate inconsistency is allowed and documented; accidental ones are fixed.

Score concept (from the upstream detector): HIGH findings weigh 10, MEDIUM 5, LOW 2, normalized per 100 lines. **0–20 clean, 21–40 slightly sloppy, 41+ is not shippable under this skill.**
