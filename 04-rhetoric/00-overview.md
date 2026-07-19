# 04-rhetoric / 00 · Overview

The rhetoric layer is where AI smell is most seductive. Visual defaults
are obvious; lexical defaults are catchable; rhetorical defaults feel
like good writing. They are not. They are **the simulation of good
writing** — the surface without the substance.

This layer covers three strategic decisions:

1. **Quotation** — when to bring in outside voices
2. **Summarization** — when to wrap up, when to stop
3. **Concept-coining** — when to invent new terms

These three are **the same problem in three forms**: the model uses
formal structures to fake content it doesn't have. A quote fakes
authority. A summary fakes completeness. A coined term fakes insight.
All three are recognizable, and all three are reversible.

---

## The shared rule

For every quotation, every summary, and every coined term, the agent
must answer:

> **Does this carry information that flat prose couldn't?**

- A quote carries information when removing it would collapse the argument.
- A summary carries information when it crystallizes a complex thread that the reader would otherwise lose.
- A coined term carries information when existing vocabulary genuinely fails to describe the new thing.

If the answer is "no," the structure is **decoration**. Decoration is the
smell. Remove it.

---

## Why these three cluster

The three rhetorical defaults come from the same source: **RLHF training
rewards "polished, complete, authoritative" output.** Quotes add
authority. Summaries add completeness. Coined terms add insight. Each
is a cheap way to look like the kind of text raters gave high scores
to during training.

The result is text that **looks like good writing** — quoted authorities,
neat summaries, sharp concepts — but lacks the substance that earned
those structures in human writing. A human writer quotes because they
genuinely need a voice other than their own; the model quotes because
quotes correlate with quality in the training data.

This is what's meant by "form faking content." The form (quote, summary,
concept) is present without the reason for the form.

---

## The three sub-layers

Read all three before producing text. They interact:

- Quotation without summary-discipline produces text that ends with a
  quote and no landing.
- Summary without quotation-discipline produces text that ends with
  forced elevation because there's nothing left to say.
- Concept-coining without either produces text full of "X's Law" and
  "The X Model" — terms that sound deep but explain nothing.

The combination is what gives text its rhetorical shape. A piece with
no quotes, one natural summary, and no coined terms is almost certainly
better than one with all three present by default.

---

## How to read this layer

Each file has the same structure:

- **Default reflex** — what the model reaches for
- **Why the reflex exists** — the training-data mechanism
- **Bad example** — the default, annotated
- **Good example** — a source-driven alternative, annotated
- **Heuristic questions** — to ask during the decision
- **Instruction template** — to give to the agent

Read all three before producing text output.
