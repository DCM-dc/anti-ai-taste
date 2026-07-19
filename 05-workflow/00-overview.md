# 05-workflow / 00 · Overview

The workflow layer is where the rubber meets the road. The previous
sections cover **what** to choose; this section covers **how to make the
choices** in practice.

Even with the best principles, an LLM will default to defaults if asked
to produce output in a single shot. The workflow must **force** the
model to escape its first guesses. This happens through:

1. **Process** — multi-step workflows that prevent one-shot defaulting
2. **Self-check** — heuristic questions that catch defaults before delivery

---

## The shared rule

For every workflow, the agent must:

1. **Ask before producing.** Don't generate output until you've gathered
   the sources that will drive the choices.
2. **Produce multiple candidates.** Single outputs are first guesses.
   Multiple candidates force the model to explore.
3. **Self-critique before delivering.** Run the heuristic questions from
   `02-self-check.md` on the output. Anything you can't answer for → redo.

---

## Why this layer matters most

You can read every principle in this repo and still produce AI-smelling
work. The principles only matter if the workflow forces you to apply them.

The default LLM workflow is: **user asks → model produces → user gets
output.** This is one-shot generation, and one-shot generation always
defaults to defaults. The model has no time to consider alternatives,
no reason to ask for sources, no checkpoint to catch its first guesses.

A guided workflow inserts friction:

```
user asks
  → model asks 3–5 questions about sources
  → user answers
  → model produces 3 candidates in different directions
  → model self-critiques against heuristics
  → model picks one and rewrites
  → model self-critiques again
  → user gets output
```

This is slower. It's also dramatically less default-y. The friction is
the point.

---

## The two sub-layers

Read both before producing any output:

- **01-process.md** — the multi-step workflow
- **02-self-check.md** — the heuristic questions to run before delivery

The process is the **preventive** layer; it shapes how you produce.
The self-check is the **corrective** layer; it catches what slipped through.

Both are necessary. Process without self-check produces varied but
still-default-y output. Self-check without process catches some defaults
but doesn't prevent the model from generating them in the first place.

---

## How to read this layer

Each file has the same structure as the previous layers:

- **Default reflex** — what the model reaches for
- **Why the reflex exists** — the training-data mechanism
- **Bad example** — the default, annotated
- **Good example** — a source-driven alternative, annotated
- **Heuristic questions** — to ask during the decision
- **Instruction template** — to give to the agent

Read both before producing any output for users who care about AI smell.
