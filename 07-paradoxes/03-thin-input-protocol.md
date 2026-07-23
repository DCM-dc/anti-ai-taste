# 07-paradoxes / 03 · Thin-input protocol

## The failure mode

The guide assumes the user provides sources: brand assets, target
audience, locale, content semantics, references. The workflow
(`05-workflow/01-process.md`) says "ask 5 questions before producing."

But most users don't provide context. Most prompts are:

> "Make me a website."
> "Write me an article about X."
> "Design a landing page."

When input is thin, the framework's "name a source" rule forces the
agent into one of two failure modes:

1. **Hallucinate sources** — invent brand heritage, user personas,
   reading contexts that weren't provided. (Caught by `02-source-verification.md`.)
2. **Refuse to produce** — stall forever asking questions the user
   won't answer. (Useless.)

Neither is acceptable. This file defines the third path.

---

## The three-path protocol

When input is thin, the agent picks one of three paths, explicitly:

### Path A: Ask (if user will engage)

If the user's prompt suggests they'll answer questions, ask 3–5
questions about sources. But:

- **Cap the questions at 5.** More feels like stalling.
- **Make questions specific, not generic.** Not "who's your audience?"
  but "is the user reading this on phone in sun, or desktop in office?"
- **Provide a default** for each question, so the user can answer
  "default" if they don't care.

```
I can produce this, but the output will be much better with 3 pieces
of context. Answer any you have; the rest I'll default:

1. Brand color (if any)? [default: none, I'll pick]
2. Who reads this, where? [default: desktop, office]
3. One site you like, one you don't? [default: I'll reference linear.app]
```

### Path B: Diverge (if user wants one-shot but no context)

If the user wants one-shot output and won't answer questions, produce
**3 candidates in wildly different directions** rather than 1 default.

The point: when you can't source, **diverge** so at least the output
isn't the single centroid. Three random seeds produce more variety
than one optimized guess.

```
You didn't provide context, so I'm giving you 3 directions that are
intentionally different. Pick one and I'll refine:

Direction A: [palette X, font Y, layout Z]
Direction B: [palette X', font Y', layout Z']
Direction C: [palette X'', font Y'', layout Z'']

All three use unsourced defaults. Provide context to escape defaults.
```

The candidates must be **structurally different** — different palette
logic, different layout grammar, different voice. Not 3 variations of
the same template.

### Path C: Label (if user wants one-shot, one-output, no context)

If the user wants exactly one output with no context, produce it — but
**explicitly label it as unsourced defaults**. Do not dress defaults
as sourced choices.

```
Here's the landing page.

NOTE: 7 of 10 design choices in this output are unsourced defaults.
The palette, font, layout, motion, and copy register are all first
guesses. This output will read as "AI style" because no sources were
provided.

To improve:
- Provide brand color → palette becomes sourced
- Provide target user → layout becomes sourced
- Provide reference site → typography becomes sourced
```

This is honest. The user gets their one-shot output, but they know
exactly what they're getting and how to improve it.

---

## What NEVER to do

### Never: fabricate sources to satisfy the framework

If the user didn't provide a brand, do not invent one. If the user
didn't state a locale, do not claim "coastal Japan haze." If the user
didn't name a reference, do not cite one.

```
✗ "Palette: warm cream, evoking the user's hand-made ceramics brand."
  [User said nothing about ceramics. Hallucination.]

✓ "Palette: warm cream. First guess; no brand asset provided."
  [Honest.]
```

Fabricating sources is worse than defaulting. Defaults are visible;
hallucinated sources hide defaults behind fake reasoning.

### Never: stall past 5 questions

If the user has answered 5 questions and you still "need more context,"
you're stalling. Produce with what you have. Mark gaps as defaults.

### Never: refuse to produce

If the user wants output, produce output. The guide's principles are
for shaping output, not for refusing to produce. A labeled default
output is more useful than no output.

---

## The "input floor"

The minimum input that allows sourced output:

| Decision | Minimum input to source |
|---|---|
| Palette | Brand color OR locale OR user emotion keyword |
| Typography | Content type (long-form / marketing / data) OR reference site |
| Layout | Content inventory with weights OR user reading pattern |
| Copy register | Target audience OR writer's voice sample |
| Motion | Product personality (tool / marketing / playful) |

If the user provides none of these, **all five decisions are unsourced
defaults.** Label them. Do not fabricate sources.

If the user provides one (e.g., content type = "long-form essay"),
**only typography can be sourced.** The other four remain defaults.
Label them. Do not let the one sourced decision create the illusion
that all five are sourced.

---

## How this fails if applied naively

If the agent treats "ask questions" as a ritual rather than a real
input-gathering step, it will:

- Ask 5 questions.
- Get vague answers ("modern, professional").
- Proceed as if it had rich sources, fabricating the specificity.

This is Path A done wrong. The cure: if the user's answers are vague,
**treat them as no answers** and fall through to Path B or C.

```
✗ User: "Make it modern and professional."
  Agent: [proceeds as if "modern and professional" were rich context,
         fabricates brand heritage]

✓ User: "Make it modern and professional."
  Agent: "Modern and professional is too vague to source from. I'll
         produce 3 directions with different interpretations of
         'modern and professional.' Pick one."
```

---

## Heuristic questions

1. **What did the user actually provide?**
   List the concrete sources (brand asset, user statement, reference, content type).
2. **What did the user NOT provide?**
   List the gaps. For each gap, the corresponding decision is a default.
3. **Are you fabricating any sources?**
   If you claimed a source the user didn't provide, remove it. Admit as default.
4. **Did you ask, diverge, or label?**
   If none of the three, you're in the failure mode. Pick a path.
5. **If you asked and got vague answers, did you treat them as no answers?**
   "Modern and professional" is not a source. Fall through.
6. **Are your 3 divergent candidates actually different?**
   If they share palette logic, layout grammar, or voice, they're not divergent.
7. **Does your output honestly label which choices are sourced vs default?**
   If you dress defaults as sourced, you're hallucinating.

---

## Instruction template

```
Before producing, assess input quality:

INPUT PROVIDED:
  - brand asset? [yes / no]
  - target user? [yes / no]
  - content type? [yes / no]
  - reference site? [yes / no]
  - locale? [yes / no]

PATH SELECTION:
  - If user will engage: Path A (ask 3–5 specific questions, capped)
  - If user wants one-shot, no context: Path B (3 divergent candidates)
  - If user wants one output, no context: Path C (produce, label defaults)

FORBIDDEN:
  - Fabricating sources the user didn't provide
  - Asking more than 5 questions
  - Refusing to produce
  - Dressing defaults as sourced choices

IF INPUT IS THIN:
  - Mark each decision as "sourced" or "default" explicitly
  - Sourced count: ___ / total decisions
  - Default count: ___ / total decisions
  - Include in output: "X of Y decisions are unsourced defaults.
    Provide [specific input] to source them."
```
