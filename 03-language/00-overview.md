# 03-language / 00 · Overview

The language layer is where AI smell is most insidious. Visual defaults are
visible at a glance; language defaults are visible only when you read.
But once you can read them, you can't unsee them.

This layer covers three decision domains:

1. **Vocabulary** — which words to reach for, which to refuse
2. **Syntax** — sentence patterns and their traps
3. **Rhythm** — burstiness, paragraph shape, the music of prose

---

## The shared rule

For every word, sentence, and paragraph, the agent must answer:

> **Is this the most specific option, or the safest option?**

LLMs generate text by predicting the most likely next token. The most
likely token is, by definition, the **safest** — the one that fits the
most contexts. Safety is the smell. Specificity is the cure.

A safe text reads:
> "Leveraging AI to foster seamless collaboration across teams."

A specific text reads:
> "We use a fine-tuned model to draft PR descriptions from commit diffs,
> so reviewers spend less time on summary text and more on the actual change."

The first could appear in 100,000 documents. The second could appear in
exactly one. That's the difference.

---

## The two underlying signals

Every detector measures two things:

| Signal | Definition | AI | Human |
|---|---|---|---|
| **Perplexity** | How predictable each word is | 5–10 | 20–50 |
| **Burstiness** | Sentence-length variance | Low (uniform 15–25 word sentences) | High (4-word sentence next to 45-word sentence) |

AI text is **low-entropy**: every word is the most probable one, every
sentence is the most probable length. Human text is **high-entropy**:
surprising words appear, sentence length varies with thought.

You don't need to compute these numbers. You need to **feel** them. When
prose reads as "smooth and even," it's low-entropy. When prose reads as
"lumpy, with surprises," it's high-entropy. Aim for lumpy.

---

## The three sub-layers

Read all three before producing text. They interact:

- Vocabulary without rhythm is still flat (sign-word-free but uniform).
- Rhythm without vocabulary is still safe (varied sentence length but generic words).
- Syntax without either is still default-y (varied structure but center-hugging content).

The combination is what escapes the smell. A specific word in a varied
sentence in a non-uniform paragraph — that's human-shaped prose.

---

## How to read this layer

Each file has the same structure as the visual layer:

- **Default reflex** — what the model reaches for
- **Why the reflex exists** — the training-data mechanism
- **Bad example** — the default, annotated
- **Good example** — a source-driven alternative, annotated
- **Heuristic questions** — to ask during the decision
- **Instruction template** — to give to the agent

Read all three before producing text output.
