# 03-language / 02 · Syntax

## Default reflex

- **Sentence length uniformity**: most sentences 15–25 words, all paragraphs similar shape
- **"Not X, but Y"** negation-parallel structure, used as a default reflex for any contrast
- **"Not only X, but also Y"** as the default escalation
- **Three-part parallelism** ("We build. We ship. We scale.") as the default rhythmic flourish
- **"X is the Y of Z"** definitional metaphor as the default philosophical flourish
- **Passive voice in technical descriptions** ("is optimized," "are designed to")
- **Subject-verb openings** with no variety: "The system... The platform... The user..."
- **Hedge stacking**: "It is important to note that, in many cases, ..."

## Why the reflex exists

LLMs predict the next token. The most probable continuation of any
contrast setup is the "not X, but Y" structure — it's the modal pattern
in the training corpus. Same with three-part parallelism: it's the
modal rhythmic flourish in marketing, academic, and corporate writing.

These structures are **syntactically safe** — they sound polished, they
balance well, they fill space. They're also the structures human writers
use **sparingly**, because using them constantly drains them of force.

## Bad example (the default, annotated)

> The new platform **is not just a tool, but a paradigm shift** in how
> teams collaborate. **It is not only faster, but also more intuitive.**
> **We don't just build features — we craft experiences.** The system
> **is designed to** scale seamlessly, **is optimized for** performance,
> and **is built around** the user. **In today's fast-paced world**,
> **it is important to note that** success **is not about** working
> harder, **but about** working smarter.
>
> **The platform empowers teams.**
> **The system delivers results.**
> **The user benefits.**
> <!-- ↑ three-part parallelism, identical sentence structure -->

**Why this smells:**
- Three "not X, but Y" structures in 6 sentences.
- Three passive constructions in a row ("is designed," "is optimized," "is built").
- Three subject-verb sentences in a row at the end ("The X verbs.")
- All sentences are 12–22 words. Zero variance in length.
- Hedge stacking ("it is important to note that, in many cases") — padding.
- The parallelism is decorative, not load-bearing.

## Good example (source-driven, annotated)

> We rewrote the PR bot last week. The old version called GPT-4o for every
> diff; the new one batches 8 diffs per call, which cut our API spend from
> $1,200/mo to $340. Latency dropped too — most PRs now get a description
> in 4 seconds instead of 11.
>
> The tradeoff: batching means if one diff in the batch is malformed, all 8
> fail. We catch this with a validator that runs before the batch is sent.
> It's 40 lines of Python.
>
> Worth it? For us, yes. We're a 12-person team. If you're at 200 people,
> the failure mode might matter more.

**Why this doesn't smell:**
- Sentence lengths vary: 6, 19, 18, 11, 13, 5, 14, 4, 9, 5, 4, 8, 10.
- No "not X, but Y" structures.
- No three-part parallelism.
- Active voice throughout ("we rewrote," "the new one batches," "we catch").
- Varied sentence openings ("We...", "The old version...", "The new one...",
  "Latency...", "The tradeoff:", "Batching means...", "We catch...",
  "It's...", "Worth it?", "For us, yes.", "If you're...").
- Hedge is specific, not stacked ("might matter more" — one hedge, with a reason).
- The parallelism that exists is **load-bearing** ("if you're at 200 people,
  the failure mode might matter more" — the contrast carries information).

## The "not X, but Y" rule

This structure is the single most-recognizable syntactic tell in AI
writing. It's not banned — sometimes it's the right move. But:

- **Use it once per piece, maximum.**
- **Use it only when the contrast is genuinely surprising.** "It's not
  a tool, it's a paradigm" is not surprising. "It's not a bug, it's a
  race condition we can't fix without rewriting the scheduler" is surprising.
- **Never use it as a default reflex for any contrast.** Most contrasts
  are better expressed with "but," "however," or just two sentences.

| Reflex (bad) | Surprising (acceptable) |
|---|---|
| "It's not just a tool, it's a paradigm." | "It's not a memory leak — it's the GC taking 3 seconds because we're allocating 4MB per request." |
| "We don't just build features, we craft experiences." | (just delete this) |

## The three-part parallelism rule

Three-part parallelism ("We build. We ship. We scale.") is the modal
rhythmic flourish in AI marketing copy. It's not banned, but:

- **Use it once per piece, maximum.**
- **Each part must carry information.** "We build. We ship. We scale."
  carries none. "We write the diff. We ship the PR. We revert at 3am when
  the pager goes off." carries three pieces of information.
- **Vary the structure** rather than copying "Subject verb. Subject verb. Subject verb."

## The passive-voice rule

Passive voice ("is designed to," "is optimized for") is the model's default
for technical description because it sounds objective. But it's also a
tell, and it usually **hides the actor** — which hides information.

| Passive (hides actor) | Active (reveals actor) |
|---|---|
| "The system is optimized for low latency." | "We tuned the GC pause target to 50ms." |
| "Errors are logged to stderr." | "The wrapper logs errors to stderr." |
| "It is recommended that..." | "We recommend..." or just state the recommendation. |

Active voice isn't always right — passive is fine when the actor is
genuinely irrelevant ("the package was deployed at 3am"). But default to
active; switch to passive only with a reason.

## The sentence-opening rule

If three sentences in a row start with the same structure (subject-verb,
or "The X..."), the prose is mechanical. Vary openings:

- Subject-verb ("We rewrote the bot.")
- Prepositional phrase ("After the rewrite, latency dropped.")
- Adverb ("Yesterday, we shipped.")
- Dependent clause ("When the batch fails, we retry individually.")
- Question ("Worth it? For us, yes.")
- Fragment ("Mostly.")
- Conjunction ("But the tradeoff is real.")

Variety in openings is one of the strongest human-text signals.

## The hedge rule

AI writing stacks hedges: "It is important to note that, in many cases,
it may be possible to..." Each hedge is polite; stacked, they read as
evasive. Pick one hedge per claim, maximum. Often, zero is right.

| Stacked hedges (AI) | One hedge or none (human) |
|---|---|
| "It is important to note that, in many cases, it may be possible to..." | "Sometimes you can..." |
| "It is worth considering that, depending on context, ..." | "Depends on context." |

## The "load-bearing structure" rule

Syntactic structures (parallelism, contrast, metaphor) are tools. They
earn their place by **carrying information that flat prose couldn't**.

| Structure | Decorative (bad) | Load-bearing (good) |
|---|---|---|
| Three-part parallelism | "We build. We ship. We scale." | "We write the diff. We ship the PR. We revert at 3am." |
| "Not X, but Y" | "Not just a tool, but a paradigm." | "Not a memory leak — a 3-second GC pause." |
| Definitional metaphor | "AI is the electricity of the 21st century." | (delete; explain what AI does in this specific case) |

If a structure could be removed without losing information, it's
decorative. Remove it.

## Heuristic questions

1. **Count "not X, but Y" structures in the piece.**
   If more than 1, rewrite the extras.
2. **Count three-part parallelism instances.**
   If more than 1, rewrite the extras.
3. **List sentence openings for the first 5 sentences of each paragraph.**
   If 3+ start the same way, rewrite.
4. **List sentence lengths.** What's the shortest? The longest? Their ratio?
   If shortest ≥ 12 words or longest ≤ 25, the prose is too uniform.
5. **Count passive constructions per 500 words.**
   If more than 5, switch most to active.
6. **Count hedge stacks ("it is important to note that, in many cases, ...").**
   If any stack has 2+ hedges, cut to 1.
7. **For each syntactic flourish, what information does it carry?**
   If none, it's decorative. Remove.

## Anti-pattern: structure swap

Replacing "not X, but Y" with "X, however Y" is not escaping the tell.
Both are AI-shaped contrast structures. The cure is **fewer contrast
structures**, not different ones.

```
Bad:    "Don't use 'not X but Y,' use 'X, however Y' instead."  ← same reflex
Good:   "Use contrast structures at most once per piece.
        Most contrasts are better as two flat sentences:
        'The old version called GPT-4o per diff. The new one
        batches 8 per call.'"                                   ← flat, specific
```

## Instruction template

```
Choose sentence syntax. Before producing, answer:

1. Count of "not X, but Y" structures in the piece:
   __. If > 1, rewrite extras as flat sentences.

2. Count of three-part parallelism:
   __. If > 1, rewrite extras.

3. Sentence openings (first 5 of each paragraph):
   Do 3+ start the same way? If yes, vary.

4. Sentence lengths:
   Shortest: __ words. Longest: __ words.
   If shortest > 12 or longest < 25, the prose is too uniform.
   Add a 4-word sentence. Add a 35-word sentence.

5. Passive constructions per 500 words:
   __. If > 5, switch most to active.

6. Hedge stacks:
   List any sentence with 2+ hedges. Cut to 1.

7. For each syntactic flourish (parallelism, contrast, metaphor):
   What information does it carry? If none, remove.

Then produce the text. Read aloud. Mark any sentence that sounds
"too balanced" — those are usually defaults. Break the balance.
```
