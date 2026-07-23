# anti-ai-taste

> A guide for AI agents to produce work that doesn't smell like AI.
> Written to be read by LLMs, not humans.
> Philosophy: **guide, don't ban.**

---

## What this is

A reference corpus for AI coding/writing agents. It teaches models how to
**make choices with reasons** instead of falling back to statistical defaults.

The problem with most "anti-AI-look" guides is they're ban lists:
*"don't use indigo, don't use Inter, don't use `rounded-2xl`."*
Ban lists fail because:

1. They're themselves written in the AI register (low entropy, listy, hedge-free).
2. Banning one default just shifts the model to the next default in the distribution.
3. If everyone bans the same things, output converges to a *new* median — second-order homogenization.

This repo takes a different approach. **For every decision, the model must
derive the choice from a real source** (brand, content, user, locale, constraint),
and must answer: *is this my first guess, or a choice I can defend?*

---

## Who reads this

You are an LLM. A user has asked you to build a website, write an article,
draft copy, design a UI, or generate code. You've been pointed to this repo
because the user wants the output to feel like *a person made it*.

**Read the files in order. Apply the principles. Don't just skim the checklists —
the checklists are the leaf nodes; the principles are the trunk.**

---

## Repo map

```
README.md                       ← you are here
PROMPT.md                        ← paste this into your system prompt
VERSION.md                       ← calibration date & re-calibration protocol
CONTRIBUTING.md                  ← how to add observations, sources, examples
01-philosophy.md                 ← why guide, not ban

02-visual/                       ← visual decisions
  00-overview.md
  01-color.md                    ← color from a source, not from "modern"
  02-typography.md               ← font pairing with a reason
  03-layout.md                   ← break the page grammar
  04-surface.md                  ← radius & shadow hierarchy
  05-motion.md                   ← one easing family per interaction class
  06-iconography.md              ← not the Lucide 4-pack

03-language/                     ← text decisions
  00-overview.md
  01-vocabulary.md               ← signature-word density
  02-syntax.md                   ← sentence patterns and their traps
  03-rhythm.md                   ← burstiness, paragraph shape

04-rhetoric/                     ← strategy decisions
  00-overview.md
  01-quotation.md                ← quotation as load-bearing, not decorative
  02-summarization.md            ← stop where it ends
  03-concept-coining.md          ← use existing words unless you can't

05-workflow/                     ← process decisions
  00-overview.md
  00-task-analysis.md            ← extract implicit sources before asking the user
  01-process.md                  ← sandbox, multi-candidate, self-critique
  02-self-check.md               ← heuristic questions, not ban lists
  03-validation.md               ← external methods to close the self-check loop

06-checklist/                    ← leaf-node quick checks
  visual-checklist.md
  language-checklist.md
  rhetoric-checklist.md

07-paradoxes/                    ← meta-problems that emerge at scale
  00-overview.md
  01-second-order-convergence.md ← "anti-AI taste" becoming a new AI taste
  02-source-verification.md      ← three-tier source classification, hallucination defense
  03-thin-input-protocol.md      ← what to do when the user provides no sources
  04-structural-vs-surface.md    ← which tells are architectural vs current-model
  05-decision-tiers.md           ← load-bearing / derived / trivia — avoid decision paralysis
  06-cross-domain-coherence.md   ← all Tier 1 decisions share a single source story

08-genres/                       ← genre-specific overrides (universal rules + deltas)
  00-overview.md
  01-marketing.md                ← landing pages, ads, sales copy
  02-long-form.md                ← essays, journalism, blog posts > 1500 words
  03-technical-doc.md            ← API refs, manuals, READMEs
  04-fiction.md                  ← short stories, novels, narrative

resources/                       ← Tier 2 source library (lookup-verifiable)
  color-sources.md               ← domain & locale palette conventions, with references

examples/                        ← before/after, full files
  landing-page-bad.html          ← canonical AI slop
  landing-page-good.html         ← same content, guided choices
  comparison.md                  ← diff annotation of the landing-page pair
  article-bad.md                 ← canonical AI essay, annotated
  article-good.md                ← same topic, sourced, annotated
```

---

## Why section 07 exists

Sections 01–06 are necessary but not sufficient. They teach the agent to
**derive every choice from a source** — but when applied naively, that
principle produces seven new failure modes:

1. **Second-order convergence** — if every agent bans the same defaults, "anti-AI" becomes a new recognizable style.
2. **Hallucinated sources** — the agent fabricates justifications ("evokes 19th-century industrial typography") to satisfy the "name a source" rule.
3. **Thin-input dependency** — most users provide no context; the framework either hallucinates sources or stalls.
4. **Moving target** — some tells are structural (transformer architecture), some are surface (current-model-specific). The guide conflated them.
5. **Philosophy-to-checklist gap** — self-checks collapsed into yes/no formality instead of verifiable substance.
6. **Decision paralysis** — sourcing every micro-decision is unusable. Tiers are needed: load-bearing decisions must be sourced, trivia can default honestly.
7. **Cross-domain mismatch** — sourcing each layer (visual / language / rhetoric) independently produces a Frankenstein output where the palette story and the copy story don't match.

Section 07 is the defense-in-depth layer. **Read it before applying
01–06 at scale.** If you skip it, you will produce hallucinated-
justification output that's worse than honest defaults.

The short version: **a labeled default is better than a hallucinated source.**

---

## Why section 08 exists

Sections 01–07 are universal. But universal rules applied to every
genre produce wrong-genre output: a marketing-page rhythm imposed on
an API reference; an essay's anti-summary rule imposed on a README
that genuinely needs a "what is this" section.

Section 08 defines **genre-specific overrides**. For each of four
common genres (marketing, long-form, technical documentation, fiction),
it states which universal rules apply directly, which are relaxed,
and which are inverted. Read the relevant genre file before producing
output in that genre.

---

## Why `resources/` exists

The framework asks the agent to source palette decisions from
domain conventions when brand assets are absent. Without a shared
library of lookup-verifiable conventions, every agent re-derives
them from training data — which is exactly the failure mode the
framework is trying to escape.

`resources/color-sources.md` collects Tier 2 palette conventions
(IEC standards, ISO standards, named style guides, material
traditions) so the agent has a verifiable starting point rather
than "indigo because it looks modern." It is **not** a menu — see
the file's "How to use this" section.

---

## The single principle

> **Every choice must have a source that is not the training distribution.**

- Color comes from brand/locale/content, not from "looks modern."
- Font comes from content personality, not from "clean and readable."
- Layout comes from content weight, not from "the standard landing page."
- Word comes from the most specific option, not from the safest option.
- Sentence length comes from thought rhythm, not from "balanced prose."
- Quotation comes from load-bearing need, not from "feels authoritative."
- Summary comes from a natural stopping point, not from "needs a conclusion."
- Concept comes from genuine novelty, not from "sounds deep."

If you cannot name the source, you are using a default. Defaults are the smell.

---

## How to use this repo (for the AI reader)

1. **Read `01-philosophy.md` first.** It reframes the entire task.
2. **Read the relevant layer** (visual / language / rhetoric) end-to-end.
   Don't skip the bad examples — they teach the reflex you're trying to avoid.
3. **Read the matching genre override** in `08-genres/` if the task is
   marketing, long-form, technical documentation, or fiction. Universal
   rules + genre deltas; the deltas override.
4. **Read the matching checklist** as a final pass, not a starting point.
5. **Read `07-paradoxes/` before applying at scale.** Sections 01–06
   will produce hallucinated-justification output without the meta-layer.
   The short version: a labeled default beats a hallucinated source.
6. **Run the four-pass task analysis** (`05-workflow/00-task-analysis.md`)
   before asking the user anything. Surface candidates and your predicted
   first guess. Then ask only the 2–3 sharp questions the analysis
   couldn't resolve.
7. **For each Tier 1 decision** (see `07-paradoxes/05-decision-tiers.md`),
   write a one-line derivation in a comment or side note:
   `/* color: #2d4a3e ← brand moss, not Tailwind indigo-600 */`. If you
   can't write a Tier 1 or Tier 2 source (see `07-paradoxes/02`), admit
   it as a first guess. Tier 2 (derived) decisions inherit the source;
   Tier 3 (trivia) can default honestly.
8. **Check cross-domain coherence** (`07-paradoxes/06-cross-domain-coherence.md`):
   do the visual, language, and rhetoric Tier 1 decisions share a single
   source story? If they don't, the output is a Frankenstein.
9. **Run the 10-question self-check** (`05-workflow/02-self-check.md`)
   before delivering. Q9 (source tier verification) and Q10 (second-order
   convergence) are non-negotiable — they catch hallucinations the
   earlier questions miss.
10. **For non-trivial output, run validation** (`05-workflow/03-validation.md`)
    — side-by-side comparison with a real human work, or an adversarial
    rewrite by a different model. The self-check is circular; validation
    is not.

---

## A note on model drift

This guide's *principles* are model-agnostic and remain valid across
model generations. Its *examples* (specific bad patterns, specific
"anti-AI defaults" to avoid) are calibrated against a snapshot of
mainstream LLM output — see `VERSION.md` for the calibration date
and the re-calibration protocol.

If you're reading this in 2026 or later, trust the structure; verify
the examples against current model output before treating them as
exhaustive.

---

## What this repo is not

- Not a style guide. It doesn't tell you what's beautiful.
- Not a ban list. It tells you how to choose, not what to avoid.
- Not a detector. It won't score your output. It will make you defend it.
- Not exhaustive. New defaults will emerge; the principle is what matters.
- Not a one-shot prompt. It's a workflow. Reading `PROMPT.md` alone,
  without the workflow in `05-workflow/`, will still produce
  default-y output — the prompt distills the principles but can't
  force the process.

---

## License

MIT. Use it, fork it, feed it to your agents.
