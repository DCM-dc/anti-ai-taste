# 01 · Philosophy — Why guide, not ban

> Read this first. Everything else in the repo is an application of this file.

---

## The diagnosis

AI-generated work smells like AI. This is not a subjective complaint; it is
a measurable statistical phenomenon. When a language model is asked to produce
something without constraints, it returns the **centroid of its training
distribution** — the most probable sequence of tokens given the prompt. That
centroid is recognizable because it is the same centroid everyone else gets.

The smell is composed of:

- **Visual defaults** — indigo→violet gradients, Inter on white, three equal
  feature cards, `rounded-2xl` everywhere, `transition-all duration-300 ease-in-out`.
- **Lexical defaults** — *delve, leverage, foster, seamless, robust, paradigm*;
  至关重要, 综上所述, 赋能, 与此同时.
- **Syntactic defaults** — uniform sentence length, "not X but Y," forced
  three-part parallelism.
- **Strategic defaults** — quote a famous person, summarize at every paragraph
  end, coin a term to sound deep, force an uplifting conclusion.

Each of these is the model's **first guess**. Stacked together, first guesses
produce a recognizable fingerprint.

---

## Why ban lists fail

The most common response to AI smell is a ban list: *"don't use indigo, don't
use Inter, don't write 'delve,' don't end with 'in conclusion.'"*

Ban lists fail in four ways.

### 1. Ban lists are themselves AI-shaped

A ban list is a low-entropy, hedge-free, list-structured document. It is
written in the exact register it's trying to prohibit. Using the AI register
to fight the AI register is incoherent.

### 2. Banning shifts, doesn't escape

The training distribution is a probability mass. Banning `indigo` removes one
mode; the next-most-probable mode (`violet`, then `fuchsia`, then `blue-600`)
immediately fills the gap. The model is still inside the distribution — just
at a slightly different coordinate.

```
ban: indigo       → model picks violet
ban: violet       → model picks fuchsia
ban: fuchsia      → model picks blue-600
ban: blue-600     → model picks emerald-500
...you're playing whack-a-mole with the median.
```

### 3. Ban lists cause second-order convergence

If every designer reads the same ban list and bans the same defaults, output
converges on a *new* median. The burnt-sienna-and-Fraunces look becomes the
new indigo-and-Inter. The smell returns, just dressed differently. This is
the homogenization risk the IOV Labs paper closes on.

### 4. Ban lists tell you what not to do, not how to decide

A ban list is purely negative. It doesn't teach the model **how to choose**.
So in every region the ban list doesn't cover, the model still defaults.
You've patch-fixed 20 tells and left 7 unaddressed.

---

## The alternative: guide by source

The opposite of "ban defaults" is not "allow everything." It is
**require every choice to come from a named source.**

A source is anything that is not the training distribution:

| Source type | Example |
|---|---|
| Brand assets | "The company logo is moss green; the palette extends from that." |
| Locale | "The product is for coastal Japan; the palette comes from Setouchi haze." |
| Content semantics | "This is a fintech for kids; the palette is candy, not banking blue." |
| User constraint | "The user said 'warm and quiet'; the palette is cream + ember." |
| Reference | "Match the asymmetry of linear.app and the warmth of stripe.com." |
| Material reality | "The product is hand-made ceramics; the texture comes from unglazed clay." |
| Structural logic | "Three blocks of unequal weight → unequal grid columns." |

When a choice has a source, it is by definition **not the centroid** of the
distribution. It is conditional on something specific. Conditionality is the
opposite of statistical default.

---

## The operating question

For every decision, large or small, the agent must answer:

> **Is this my first guess, or a choice I can defend?**

First guesses are not always wrong. Sometimes the first guess is also the
right answer. But the agent must **know it's a first guess** and be able to
say what the second and third guesses would have been. If the agent cannot
generate alternatives, it is not choosing — it is defaulting.

This is why the workflow (see `05-workflow/01-process.md`) requires
**three candidates in different directions** before committing. The act of
generating alternatives is the act of escaping the default.

---

## What this looks like in practice

### Bad (ban-list thinking)

```
Prompt:  Make me a SaaS landing page. Don't use indigo. Don't use Inter.
         Don't use rounded-2xl.

Agent:   [picks violet, Roboto, rounded-xl]
         [still smells like AI, just a different shade]
```

### Good (source-driven thinking)

```
Prompt:  Make me a SaaS landing page. The product is a battery-monitoring
         tool for solar installers. Brand color is in the logo: deep cycle
         battery green. Target user is a field technician reading on phone
         in bright sun.

Agent:   [asks: what's the logo hex? any reference sites?]
         [derives: palette from battery green + sun-readable high contrast]
         [derives: typography from field-manual heritage (monospace data,
                   humanist sans body) — not Inter, because field techs
                   reading in glare need higher x-height and weight contrast]
         [derives: layout from "data first" — single-column dashboard,
                   not centered marketing hero, because the user wants
                   the number, not the pitch]
         [generates 3 candidates with different hero strategies:
            (a) live battery voltage readout as hero
            (b) field photo with overlaid telemetry
            (c) quote from an installer with link to case study
          picks (a) because the user is data-first]
```

The second agent's output will not smell like AI, because nothing in it came
from the training distribution's centroid. Everything came from a source.

---

## The single rule, restated

> **Every choice must have a source that is not the training distribution.**

If you cannot name the source, you are using a default. Defaults are the
smell. Sources are the cure.

The rest of this repo is the application of this rule to specific decision
domains: color, typography, layout, surface, motion, icons, vocabulary,
syntax, rhythm, quotation, summarization, concept-coining, process.

Read the relevant layer end-to-end before producing.
