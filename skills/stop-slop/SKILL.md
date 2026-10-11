---
name: stop-slop
description: "Remove AI writing patterns from prose. Use when drafting, editing, or reviewing text to eliminate predictable AI tells. Covers the full list of common AI tells: filler openers ('In today's fast-paced world...'), hollow hedging ('It's important to note that...'), em-dash asides used as a thinking crutch, vague intensifiers ('truly', 'remarkably', 'seamlessly'), metaphor clichés ('tapestry', 'landscape', 'realm', 'delve', 'navigate'), parallelism overuse ('not just X, but Y'), numbered-list padding, fake enthusiasm, empty transitions ('Furthermore', 'Moreover', 'Additionally' used to glue underdeveloped paragraphs), and the unmistakable ChatGPT/Claude/GPT rhythm where every paragraph is the same length and every sentence ends on a soft landing. Also use for translating AI-sounding drafts back into natural human voice — corporate, academic, casual, or technical. Apply to any text format: emails, blog posts, documentation, marketing copy, README files, PR descriptions, release notes, UI copy, and dialogue."
---

# stop-slop — kill AI writing tells

`stop-slop` is the skill for taking AI-flavored prose and making it sound like a human wrote it. Most AI-generated or AI-edited text has recognizable patterns — "tells" — that readers pick up on unconsciously. This skill identifies and removes them.

## When to use

- The user says "this sounds like AI" or "rewrite this to sound human".
- The user is editing a draft and asks to "tighten it up" or "make it less generic".
- You're reviewing prose and notice the rhythm feels mechanical.
- The user wants to translate corporate/AI speak into a more natural voice.

## How to use

### Step 1 — Identify the tells

Read the text once and flag every instance of these patterns. Most AI-sounding text has 5+ tells per page.

**Lexical tells** (specific words and phrases that signal AI authorship):

- "delve into", "dive into", "let's explore" — overused AI openers.
- "tapestry", "landscape", "realm", "sphere" — cliché metaphors for "field" or "domain".
- "navigate" used metaphorically ("navigate the complexities of...").
- "in today's fast-paced world", "in the ever-evolving landscape of..." — filler openers.
- "seamlessly", "effortlessly", "robustly" — adverbs AI loves; humans rarely use.
- "leverage" as a verb ("leverage our strengths") — corporate-speak.
- "myriad", "plethora" — literary words used in mundane contexts.
- "it's important to note that", "it's worth mentioning that" — empty hedges.
- "not just X, but Y" — parallelism AI overuses.
- "Furthermore", "Moreover", "Additionally" as paragraph glue.

**Structural tells** (how the text is built):

- Every paragraph the same length (3 sentences, ~50 words).
- Every paragraph opens with a topic sentence and ends with a soft summary.
- Numbered lists used to pad rather than to enumerate genuine parallel items.
- Headings like "Introduction", "Conclusion", "Key Takeaways" in short pieces that don't need them.
- Em-dashes used as a thinking crutch — multiple per paragraph.
- "In conclusion", "To summarize" at the end of a short piece.

**Tone tells**:

- Fake enthusiasm ("excited to share", "thrilled to announce").
- Hollow empathy ("we understand that this can be challenging").
- Vague intensifiers without substance ("truly remarkable", "genuinely transformative").
- The ChatGPT closing rhythm: a balanced, vaguely uplifting final sentence.

### Step 2 — Diagnose the voice

Before rewriting, identify what the text is supposed to sound like. Different contexts need different voices:

- **Corporate/professional** — direct, confident, no hedging. Short sentences. Active voice.
- **Technical/documentation** — terse, precise, no decoration. The reader wants information, not experience.
- **Casual/blog** — varied sentence length, occasional fragments, first person, contractions.
- **Academic** — formal but not inflated; precise terminology, no filler.
- **Marketing** — punchy, specific, no abstractions. Concrete claims over vague promises.

If the user didn't specify, infer from context (a README is technical; a launch announcement is marketing) and state your inference.

### Step 3 — Rewrite

Apply these transforms:

1. **Cut the opener.** Delete the first sentence if it's a "in today's world" warm-up. Start with the actual point.
2. **Vary paragraph length.** Mix 1-sentence paragraphs with 4-sentence ones. The rhythm itself signals human authorship.
3. **Replace abstractions with specifics.** "Many users" → "the 3,000 beta users from Q3". "Improved performance" → "cut p95 latency from 800ms to 120ms".
4. **Kill the hedges.** "It's important to note that X" → "X". "It's worth mentioning that Y" → "Y". The reader knows what's important by where you put it.
5. **Break parallelism.** If three sentences in a row have the same structure ("not just X, but Y"), rewrite one of them.
6. **Remove fake enthusiasm.** "We're excited to announce..." → "Today we're shipping...". Excitement should be earned by the substance, not declared.
7. **Cut transition words.** "Furthermore", "Moreover", "Additionally" — delete and see if the paragraph still works. It usually does.
8. **End on substance, not uplift.** The last sentence should leave the reader with a specific next step, a specific fact, or a specific tension — not a soft "and that's what makes X great" landing.

### Step 4 — Preserve meaning

When cutting tells, don't cut content. Every factual claim, every specific number, every name, every link should survive the rewrite. The goal is to change how it sounds, not what it says. If you find yourself cutting substance to fix style, slow down — you're editing, not rewriting.

### Step 5 — Verify with a read-aloud check

Mentally read the result aloud. If a sentence makes you stumble or sounds like something you'd never say in conversation, it still has tells. Fix it.

## Common anti-patterns (don't do these)

- **Don't replace AI tells with new AI tells.** Replacing "delve" with "let's explore" is the same problem in a different hat.
- **Don't over-correct into choppy fragments.** Varying length doesn't mean every sentence is short.
- **Don't strip personality.** If the original had a real voice (the author's actual style, brand voice), preserve it. You're removing AI patterns, not flattening style.
- **Don't add your own hedging.** "I think this version sounds more natural" — just present the rewrite.

## When NOT to use

- Code (use `code-impeccable`).
- UI/visual artifacts (use `impeccable`).
- Commit messages and PR descriptions — use `commit-craft`, which inherits anti-slop principles but applies them to the constrained format of git communications.

## References

Place deeper reference docs in `references/` — e.g., `references/ai-tells-catalog.md` with the full lexical/structural/tone taxonomy, `references/voice-examples.md` with before/after pairs across different contexts. Load when the user asks for examples or for a deeper reference pass.
