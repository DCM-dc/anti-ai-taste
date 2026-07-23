# 05-workflow / 03 · Validation

> The framework can self-check its output (`02-self-check.md`), but a
> self-check performed by the same agent that produced the output is
> circular. This file defines the external, human-runnable validation
> methods that close the loop.

## Why a separate validation layer exists

`02-self-check.md` answers: *can the agent defend each choice?*
That question catches defaults and hallucinated sources, but it cannot
catch the broader failure mode: **the agent defends choices well, and
the output still reads as AI to a human.**

A defense is not a guarantee. The agent can pass every self-check
question and still ship something that a human reads as "this was
written by a model." The self-check is necessary; it is not
sufficient. Validation is the missing second loop.

Validation is also the only honest answer to the philosophical
question raised in user feedback: *how do you know "anti-AI taste"
worked?* Without a validation method, the framework is unfalsifiable.
With one, the user can actually measure whether the guide helps.

---

## The validation principles

1. **A human, not the producing agent, runs validation.**
   The producing agent has too much investment in its own choices to
   judge them. Validation is external by definition.

2. **The human does not need to know the framework.**
   If validation only works for readers of this repo, it's circular.
   The methods below work on any reader — a colleague, a friend, a
   stranger on a forum.

3. **The output is judged against real human work, not against an
   ideal.**
   "Does this look AI?" is a leading question. "Which of these two
   did a person write?" is a fair one. Compare against actual human
   references, not against a platonic ideal of "human-feeling" prose.

4. **Defaults should be labeled before validation, not after.**
   If the agent labeled 7 of 10 choices as defaults (per
   `07-paradoxes/03-thin-input-protocol.md`), the validator already
   knows where to look. Honest labels make validation sharper.

---

## Method 1 — The side-by-side (cheapest, fastest)

**Setup.** Take the agent's output. Find one piece of real human
work in the same genre (a real landing page for a similar product,
a real essay on a similar topic, a real README for a similar tool).
Put them side by side. Don't label which is which.

**Run.** Show both to 2–3 humans who haven't seen either. Ask:

> "Two pieces of work on the same topic. Which one was written by
> a person, and which by an AI? Point to the specific choices that
> tipped you off."

**Read the result.**

- If the humans can't tell, the output passed validation. Good.
- If the humans correctly identify the AI output, ask them *which
  specific choices* tipped them off. Those choices are the defaults
  the self-check missed.

**Cost.** 5 minutes per validator, no tools needed.

**Limitation.** The comparison is only as good as the human reference
you pick. If you compare against another AI-written piece (or against
a piece written by someone who has internalized AI defaults), the
test becomes "which AI is less AI."

**Mitigation.** Use real, dated, attributable human work: a known
author's essay, a company's actual landing page captured before
2022, a published book's first chapter. If you can't find a real
human reference, you don't have a comparison — you have two AI
outputs in a trench coat.

---

## Method 2 — The annotation audit (deepest)

**Setup.** Take the agent's output with all its source annotations
intact (per `01-process.md` Stage 4 — every decision has a `/* source:
… */` comment). Hand the annotated output to a human who has not read
this repo. Do not explain the framework.

**Run.** Ask the human to do one thing:

> "For each annotation, mark it as: (a) I buy this source, (b) I
> don't buy this source, (c) I can't tell. For each (b), say why."

**Read the result.**

The annotations that come back as (b) are the failures. They fall
into two patterns:

1. **Hallucinated sources dressed as Tier 1/2.** The agent claimed
   "from the user's stated brand color" when the user stated no such
   thing. The validator smells it but can't name it; the (b) marks
   it.
2. **Generic sources that don't actually constrain the choice.**
   "Palette: warm cream, source: hand-made ceramics aesthetic."
   The validator reads this and thinks: "the source doesn't explain
   why cream instead of any other warm tone." The source is real but
   load-bearing-weak — see `07-paradoxes/01-second-order-convergence.md`.

**Cost.** 15–30 minutes per output, depending on length. Requires
a human willing to read carefully.

**Strength.** This is the only method that surfaces
hallucinated-but-plausible-sounding sources. A side-by-side test
might miss them (the output reads fine in isolation). The annotation
audit catches the gap between *claimed source* and *actual source*.

---

## Method 3 — The adversarial rewrite (cheapest solo method)

**Setup.** No human available. Use a second agent instance — ideally
a different model from the one that produced the output, to avoid
shared training defaults.

**Run.** Give the second agent the original output and this prompt:

```
This text was produced to avoid "AI smell." Your job is to find every
choice that still reads as AI. For each, name the specific tell
(word choice, sentence shape, palette, layout grammar, rhetorical
move) and propose the most specific alternative a real human would
plausibly make.

Do not propose generic alternatives ("use a warmer color"). Propose
specific ones ("replace the indigo-to-violet gradient with a single
flat brand color #2d4a3e, sourced from the logo").

Do not propose anti-AI defaults (burnt sienna, Fraunces, 7/5 grid,
"I went back to bed" endings). Those are a new centroid, not an
escape.
```

**Read the result.**

The second agent will find things the first agent missed —
*particularly* shared training-distribution defaults the first agent
couldn't see because they're its own water. Use its findings as
candidates to investigate, not as commands to apply.

**Cost.** One additional LLM call.

**Limitation.** A second LLM shares much of the first LLM's training
distribution. It will catch surface tells but may miss structural
ones (e.g., the assumption that every landing page needs a pricing
section). Run Method 1 or 2 periodically to calibrate.

---

## Method 4 — The longitudinal sniff (most honest, slowest)

**Setup.** Six months after producing the output, look at it again.

**Run.** Ask: *does this still read as AI?*

**Why this works.** AI tells shift. The indigo gradient was the
tell in 2023; by 2025 it had migrated. What looks "non-default"
today (burnt sienna, Fraunces, 7/5 grid) will be the default of
tomorrow — see `07-paradoxes/04-structural-vs-surface.md`.

If you re-read your output six months later and it still doesn't
smell, you found structural choices. If it suddenly smells again,
your choices were surface — the model's defaults moved, and your
output moved with them.

**Cost.** Free. Slow.

**When to use.** On work you care about long-term (a portfolio site,
a published essay, a design system). Not worth running on throwaway
emails.

---

## What validation is NOT

### Not a score

The framework doesn't assign a number. "8/10 anti-AI" is meaningless.
Validation produces a list of specific tells the validator found,
each tied to a specific decision the agent made. That list is the
output, not a score.

### Not a pass/fail gate

The agent can ship work that fails validation. The point is to know
*what failed and why*, not to block delivery. A failed validation
with a clear list of tells is more useful than a passing validation
with no findings.

### Not a substitute for sourcing

Validation catches what slipped through. It does not replace the
upstream work of sourcing each decision. If the agent skips
`00-task-analysis.md` and `01-process.md` and runs validation
instead, it will get a long list of tells and no idea how to fix
them — because the fix is upstream, not downstream.

---

## How to use validation in the workflow

```
Stage 0  Task analysis          (00-task-analysis.md)
Stage 1  Ask (3 sharp questions) (01-process.md)
Stage 2  3 candidates            (01-process.md)
Stage 3  Pick with reason        (01-process.md)
Stage 4  Produce with annotations(01-process.md)
Stage 5  Self-check              (02-self-check.md)
Stage 6  Deliver
Stage 7  Validate (this file)    ← optional but recommended
Stage 8  If validation found tells → re-source those specific
         decisions, not just patch the surface
```

The crucial detail: **when validation finds a tell, fix the source,
not the symptom.**

```
✗  Validator: "The headline 'Build the future of battery monitoring'
   reads as AI."
   Agent: [rewrites headline to "Power your batteries, smarter."]
   ← This is patching the symptom. The new headline is also AI.

✓  Validator: "The headline 'Build the future of battery monitoring'
   reads as AI."
   Agent: [re-sources the headline from the task analysis: the user
   is a field tech, the value prop is "the number, instantly." New
   headline: "Live readout. Always." ← from the actual product
   behavior, not from a marketing-template headline.]
   ← This is fixing the source.
```

---

## The honest disclosure

No validation method can prove an output is "AI-free." That's not
the goal. The goal is: **does this output escape the recognizable
centroid of AI work for this genre, in this period, for this
audience?**

Validation answers that question with evidence (specific tells a
human pointed to) rather than assertion ("I think it's good").

If validation consistently finds tells the self-check missed, the
self-check needs updating — see `CONTRIBUTING.md` for how to feed
those findings back into the framework.

---

## Heuristic questions

1. **Did you run any validation method on the output before
   declaring it done?**
   If not, you're trusting the self-check, which is circular. Run
   at least Method 1 or 3.
2. **Did you compare against a real, attributable human reference?**
   If your reference is also AI-written, your test is meaningless.
3. **Did you ask validators for specific tells, not for a verdict?**
   "Looks AI" is useless. "The 3-col features with Lucide icons
   reads as AI" is useful.
4. **When validation found tells, did you re-source or patch?**
   Patching the symptom produces a new default. Re-sourcing escapes.
5. **If you used Method 3 (adversarial rewrite), did you avoid
   anti-AI defaults in the proposed alternatives?**
   The second agent will reach for burnt sienna / Fraunces / 7/5
   grid if you don't tell it not to.
6. **For long-lived work, did you schedule a re-validation in
   6 months?**
   If not, you can't tell structural from surface tells.

---

## Instruction template

```
After Stage 5 (Self-check) and Stage 6 (Deliver), run validation:

METHOD 1 — Side-by-side (recommended for any non-trivial output):
  [ ] Find one real, attributable human work in the same genre
  [ ] Put agent output and human work side by side, unlabeled
  [ ] Show to 2–3 humans
  [ ] Ask: "Which was written by AI? Point to specific tells."
  [ ] Record the tells

METHOD 3 — Adversarial rewrite (if no human available):
  [ ] Use a different model instance
  [ ] Prompt: "Find every choice that still reads as AI. For each,
      name the tell and propose a specific, sourced alternative.
      No anti-AI defaults."
  [ ] Treat findings as candidates, not commands

WHEN VALIDATION FINDS TELLS:
  [ ] For each tell, identify the underlying decision
  [ ] Re-source that decision (don't patch the surface)
  [ ] Re-run self-check (02-self-check.md) on the re-sourced version
  [ ] Re-validate if the change was load-bearing

FOR LONG-LIVED WORK (portfolio, published, design system):
  [ ] Schedule re-validation in 6 months
  [ ] On re-validation: tells that disappeared = structural choices.
      Tells that are new = surface choices; the centroid moved.
```
