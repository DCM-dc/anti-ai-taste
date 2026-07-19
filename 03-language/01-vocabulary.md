# 03-language / 01 · Vocabulary

## Default reflex

### English signature words

> delve, leverage, utilize, foster, harness, catalyze, unlock, unleash,
> elevate, revolutionize, amplify, illuminate, elucidate, supercharge,
> resonate, navigate, embrace, embark, underscore, meticulous, pivotal,
> robust, intricate, nuanced, seamless, vibrant, unparalleled, comprehensive,
> tapestry, landscape, realm, paradigm, game-changer, furthermore, moreover,
> additionally, consequently, subsequently, nevertheless, nonetheless,
> notably, importantly, in conclusion, to sum up, at the end of the day,
> in today's fast-paced world, in the realm of, navigate the complexities of,
> harness the power of, build the future of, supercharge your, empower your team

### Chinese signature words

> 至关重要, 综上所述, 由此可见, 不难看出, 值得注意的是, 与此同时,
> 在当下时代, 在新时代背景下, 赋能, 迭代, 多措并举, 根植于, 奠定基础,
> 做出不可磨灭的贡献, 标志着……的转变, 时代的转折点, 不断变化的格局,
> 具有重要意义, 深远的影响, 行稳致远, 双向奔赴, 守正创新, 有机统一,
> 相辅相成, 鸟之两翼车之两轮, 穿越迷雾的灯塔

### The marketing 4-pack

> Build the future of work · Supercharge your workflow ·
> Harness the power of AI · Empower your team

## Why the reflex exists

These words appear with disproportionate frequency in AI-generated text
because they're statistically "safe" — they fit any context, they sound
sophisticated without being technical, they're mid-formal in register.
RLHF training reinforced them because human raters preferred "polished"
prose, and these words polish.

Max Planck Institute research found "delve" usage surged 654% in academic
papers after November 2022 — 46% of all historical "delve" uses appeared
in 15 months. Geostar's analysis of 186,000 articles found some signature
words appear **2× to 182× more frequently** in AI text than human text.

The signature words **cluster**: when one appears, others usually appear
nearby. Density is the tell, not presence.

## Bad example (the default, annotated)

> In today's fast-paced world, **harnessing** the power of AI is **crucial**
> for teams looking to **supercharge** their workflows. By **leveraging**
> cutting-edge tools, organizations can **foster seamless collaboration**
> and **unlock new possibilities**. The **intricate tapestry** of modern
> work demands **robust** solutions that **navigate the complexities** of
> **an ever-changing landscape**. **Furthermore**, **delving** into these
> **paradigm-shifting** technologies **empowers** teams to **elevate**
> their productivity to **unparalleled** heights. **At the end of the day**,
> the **pivotal** question is not whether to adopt AI, but how to **embark**
> on this **transformative journey**.

**Why this smells:**
- 17 signature words in 6 sentences (density ≈ 1 sign-word per 7 words; threshold for AI tell is ≈ 1 per 100).
- Every clause is the safest possible phrasing for its idea.
- No specific noun, no specific verb, no specific number, no specific name.
- Could describe any product in any industry. The text has no fingerprint.

## Good example (source-driven, annotated)

> We use a fine-tuned Llama-3 8B to draft PR descriptions from commit
> diffs. Reviewers on our team spent an average of 4 minutes per PR
> writing summary text; after the bot, they spend 40 seconds editing
> instead. The bot doesn't decide what to review — it just writes the
> "what changed" paragraph so the reviewer can start at the "is this
> right" question.
>
> We picked Llama-3 over GPT-4o because the diffs are short enough that
> 8B is fine, and we run it on a single 4090 we already had for the
> build farm. Total cost: the electricity.

**Why this doesn't smell:**
- Zero signature words.
- Specific nouns: Llama-3 8B, GPT-4o, 4090, build farm.
- Specific numbers: 4 minutes, 40 seconds, 8B, single 4090.
- Specific verbs: draft, spent, editing, picked, run.
- A specific reasoning chain: "we picked X over Y because Z."
- Could not appear in any other document. The text has a fingerprint.

## The density rule

A single signature word is not a tell. The tell is **density**:

| Density | Verdict |
|---|---|
| 0 signature words per 500 words | Human-shaped |
| 1 per 500 words | Fine |
| 2–3 per 500 words | Suspect |
| 4–5 per 500 words | AI tell |
| 6+ per 500 words | Pure slop |

Count them. If you're over 3 per 500, rewrite.

## The "most specific" rule

For every word choice, ask: **is this the most specific option, or the
safest option?**

| Safest (AI) | More specific (human) |
|---|---|
| leverage | use |
| utilize | use |
| facilitate | help |
| foster | build / grow |
| harness | use |
| catalyze | spark / trigger |
| unlock | enable / allow |
| elevate | improve / raise |
| revolutionize | change |
| seamless | unconfigured / works-out-of-the-box |
| robust | reliable / tested |
| comprehensive | full / complete |
| paradigm | model / approach |
| delve into | dig into / read |
| navigate the complexities of | deal with |
| in today's fast-paced world | (delete — adds nothing) |
| at the end of the day | (delete — adds nothing) |

The safe word is the modal word — the one that fits every context.
The specific word is the one that fits **this** context. Always pick specific.

## The "replace with concrete" rule

When you catch a signature word, don't just replace it with a synonym.
**Replace it with concrete content.**

```
Bad:  "We foster seamless collaboration across teams."
Synonym-replaced: "We build smooth teamwork across teams."    ← still generic
Concrete-replaced: "We replaced three Slack channels with one
                   Linear workspace; PR review latency dropped
                   from 2 days to 4 hours."                   ← specific
```

The signature word was hiding the absence of content. Replacing it with
another word keeps the absence. Replacing it with content fills the absence.

## Heuristic questions

1. **Count signature words per 500 words.** If over 3, rewrite.
2. **For each adjective, what specific information does it give?**
   "Seamless" gives none. "0-config, 3-second startup" gives two facts.
3. **For each verb, is there a more specific alternative?**
   "Leverage" → "use" → "fine-tune on internal data."
4. **Are there proper nouns? Numbers? Dates?** If none, the text is hiding.
5. **Could this paragraph appear in 1000 other documents?**
   If yes, it has no fingerprint. Add specificity until it couldn't.
6. **Is the register flat?** Mid-formal everywhere = AI. Real text varies:
   technical when describing the work, casual when describing the team,
   blunt when describing the problem.

## Anti-pattern: synonym swap

Replacing "leverage" with "utilize" is not de-AI'ing the text. Both are
signature words. The cure is not a different safe word — it's a specific one.

```
Bad:    "Don't use 'leverage,' use 'utilize' instead."    ← still AI
Worse:  "Don't use 'leverage,' use 'synergize' instead."  ← more AI
Good:   "Don't write 'leverage.' Write what you actually do:
        'we fine-tune Llama-3 on our commit history.'"    ← specific
```

## Instruction template

```
Choose vocabulary. Before producing, answer:

1. List every signature word in your draft (English or Chinese).
   Count per 500 words. If over 3, rewrite.

2. For each adjective, what specific fact does it convey?
   "Seamless" → ___ (if blank, delete or replace with a fact)

3. For each abstract verb (leverage/foster/harness/etc.),
   what is the concrete action?
   "We leverage AI" → "We fine-tune Llama-3 on ___"

4. List the proper nouns, numbers, and dates in the draft.
   If fewer than 3, the text is hiding. Add specifics.

5. Could this paragraph appear in 1000 other documents?
   If yes, add specificity until it couldn't.

6. Register: where does the text shift between technical / casual / blunt?
   If it doesn't shift at all, it's flat. Vary it.

Then produce the text. Read it aloud. Mark any word that sounds
"smart but empty" — those are signature words. Replace them.
```
