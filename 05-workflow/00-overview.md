# 05-workflow / 00 · Overview

The workflow layer is where the rubber meets the road. The previous
sections cover **what** to choose; this section covers **how to make the
choices** in practice.

Even with the best principles, an LLM will default to defaults if asked
to produce output in a single shot. The workflow must **force** the
model to escape its first guesses. This happens through four stages:

1. **Task analysis** — extract implicit sources from the task itself,
   before asking the user anything
2. **Process** — multi-step workflow that prevents one-shot defaulting
3. **Self-check** — heuristic questions that catch defaults before delivery
4. **Validation** — external methods that close the loop the self-check
   can't (because the producing agent can't objectively judge its own
   output)

---

## The shared rule

For every workflow, the agent must:

1. **Extract before asking.** Run the four-pass task analysis to surface
   candidates and predicted defaults. Don't ask the user what you can
   derive.
2. **Ask only what extraction couldn't resolve.** Cap at 3 sharp
   questions, not 5 generic ones.
3. **Produce multiple candidates.** Single outputs are first guesses.
   Multiple candidates force the model to explore.
4. **Self-critique before delivering.** Run the heuristic questions from
   `02-self-check.md` on the output. Anything you can't answer for → redo.
5. **Validate externally when stakes are high.** The self-check is
   circular; `03-validation.md` defines the methods that aren't.

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
  → model runs task analysis (4 passes: domain, audience, constraints,
     predicted first guess)
  → model surfaces candidates + predicted default
  → model asks 3 sharp questions (only what extraction couldn't resolve)
  → user answers
  → model produces 3 candidates in different directions, seeded by analysis
  → model self-critiques against heuristics
  → model picks one and rewrites
  → model self-critiques again
  → user gets output
  → (for high-stakes work) external validation
```

This is slower. It's also dramatically less default-y. The friction is
the point.

---

## The four sub-layers

Read all four before producing any output:

- **00-task-analysis.md** — the four-pass extraction (domain, audience,
  constraints, predicted first guess). Run this **before** `01-process.md`
  Stage 1.
- **01-process.md** — the multi-step workflow (ask → 3 candidates → pick
  with reason → produce with annotations → self-check)
- **02-self-check.md** — the 10 heuristic questions to run before delivery
- **03-validation.md** — external validation methods (side-by-side,
  annotation audit, adversarial rewrite, longitudinal sniff). Optional
  but recommended for non-trivial output.

The task analysis is the **input-shaping** layer; it determines what
you're working with before you ask for more.
The process is the **preventive** layer; it shapes how you produce.
The self-check is the **corrective** layer; it catches what slipped through.
The validation is the **external** layer; it closes the loop the agent
can't close on itself.

All four are necessary at scale. Skipping any one produces a known
failure mode:

- Skip task analysis → you ask 5 generic questions, get vague answers,
  fall through to hallucinated sources.
- Skip process → one-shot output, defaults everywhere.
- Skip self-check → varied but still-default-y output.
- Skip validation → you ship work the producing agent defends well but
  that humans still read as AI.

---

## How to read this layer

Each file has the same structure as the previous layers:

- **Default reflex** — what the model reaches for
- **Why the reflex exists** — the training-data mechanism
- **Bad example** — the default, annotated
- **Good example** — a source-driven alternative, annotated
- **Heuristic questions** — to ask during the decision
- **Instruction template** — to give to the agent

Read all four before producing any output for users who care about AI smell.
