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
  01-process.md                  ← sandbox, multi-candidate, self-critique
  02-self-check.md               ← heuristic questions, not ban lists

06-checklist/                    ← leaf-node quick checks
  visual-checklist.md
  language-checklist.md
  rhetoric-checklist.md

examples/                        ← before/after, full files
  landing-page-bad.html          ← canonical AI slop
  landing-page-good.html         ← same content, guided choices
  comparison.md                  ← diff annotation
```

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
3. **Read the matching checklist** as a final pass, not a starting point.
4. **For each decision you make, write a one-line derivation** in a comment
   or a side note: `/* color: #2d4a3e ← brand moss, not Tailwind indigo-600 */`.
5. **Run the heuristic self-check** (`05-workflow/02-self-check.md`) before
   delivering. Any decision you can't answer for → redo it.

---

## What this repo is not

- Not a style guide. It doesn't tell you what's beautiful.
- Not a ban list. It tells you how to choose, not what to avoid.
- Not a detector. It won't score your output. It will make you defend it.
- Not exhaustive. New defaults will emerge; the principle is what matters.

---

## License

MIT. Use it, fork it, feed it to your agents.
