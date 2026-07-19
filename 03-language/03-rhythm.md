# 03-language / 03 · Rhythm

## Default reflex

- All paragraphs 3–5 sentences, all sentences 15–25 words
- Every paragraph has a topic sentence, body, and conclusion
- Every section ends with a transition to the next
- No fragments. No one-word sentences. No tangents. No interruptions.
- Punctuation: comma, period, comma, period, in regular rhythm
- No em-dashes used as asides; no semicolons; no colons for emphasis
- No questions asked unless immediately answered

Prose that reads like a metronome.

## Why the reflex exists

LLM training data skews toward edited prose: documentation, marketing,
academic papers, news articles. These genres share conventions: paragraph
balance, sentence regularity, smooth transitions. The model learned these
conventions as the modal distribution and reproduces them everywhere —
even in genres where they don't belong (blogs, essays, casual writing).

The result is "low burstiness": low variance in sentence length, low
variance in paragraph shape, low variance in punctuation. Detector
benchmarks show AI text has burstiness roughly **half** of human text.

## Bad example (the default, annotated)

> The platform provides a comprehensive set of features for modern teams.
> It includes task management, time tracking, and reporting capabilities.
> Users can create projects, assign tasks, and monitor progress in real
> time. The system is designed to be intuitive and easy to use.
>
> Integration with third-party tools is fully supported. The platform
> connects with Slack, GitHub, and Google Workspace. This allows teams
> to maintain their existing workflows without disruption. Setup takes
> only a few minutes.
>
> Security is a top priority for the development team. All data is
> encrypted at rest and in transit. The platform complies with industry
> standards including SOC 2 and GDPR. Regular audits ensure ongoing
> compliance with these requirements.

**Why this smells:**
- Every paragraph is exactly 4 sentences.
- Every sentence is 12–20 words.
- Every paragraph has the same shape: claim → list → elaboration → reassurance.
- No fragments, no short sentences, no long sentences, no questions, no asides.
- Transitions are smooth to the point of invisibility — nothing interrupts.
- The prose is technically correct and entirely forgettable. It has no music.

## Good example (source-driven, annotated)

> The bot died at 2:47am last Tuesday.
>
> Not "stopped responding." Not "degraded performance." Died — the process
> was gone, the supervisor restarted it, and the in-flight PR descriptions
> were lost. Three of them. The fourth had been written to disk 0.3 seconds
> before the crash, which is the kind of luck you don't question.
>
> We spent Wednesday morning figuring out why. Turned out the OOM killer
> had been firing for a week — we just hadn't noticed because the
> supervisor restart was fast enough that the on-call didn't page. The
> bot had been slowly leaking memory since the batching change. Embarrassing.
>
> Fix: we cap the batch at 8 diffs (was unbounded) and added a memory
> gauge to the dashboard. Took 90 minutes including the test.
>
> Could we have caught it sooner? Probably. The metric was there; we
> just didn't alert on it. Now we do.

**Why this doesn't smell:**
- Sentence lengths vary wildly: 8, 4, 4, 18, 2, 19, 7, 6, 9, 17, 12, 1, 24, 12, 4, 3, 5, 6.
- Paragraph lengths vary: 1 sentence, 5 sentences, 4 sentences, 2 sentences, 2 sentences.
- Fragments appear: "Three of them." "Embarrassing." "Fix:" "Probably."
- Questions appear: "Could we have caught it sooner?"
- Asides appear: "(was unbounded)" "which is the kind of luck you don't question."
- The rhythm matches the content: short for impact ("Died."), long for
  explanation ("Turned out the OOM killer had been firing for a week..."),
  fragments for turns ("Embarrassing.").
- The prose has music. You can hear it.

## The burstiness rule

Aim for high variance in:

- **Sentence length**: include at least one sentence under 8 words and one
  over 30 words per 200 words of prose.
- **Paragraph length**: include at least one 1-sentence paragraph and one
  5+ sentence paragraph per 1000 words.
- **Punctuation**: use commas, periods, em-dashes, colons, semicolons,
  question marks, and exclamation points where each is appropriate.
  Default AI uses only commas and periods.

This isn't decoration. It's how thought actually moves: short for emphasis,
long for exploration, fragment for turn, question for doubt.

## The fragment rule

Fragments are forbidden in formal prose, used everywhere in real writing.
A fragment is a sentence without a subject-verb structure: "Three of them."
"Embarrassing." "Mostly." "Worth it?"

Use fragments for:
- **Punch**: "Died." lands harder than "The process died."
- **Turn**: "Embarrassing." signals a shift in the writer's stance.
- **Answer**: "Probably." answers a question without ceremony.

Don't use fragments for every sentence — that's a different affectation.
Use them where the rhythm calls for a hit.

## The one-sentence paragraph rule

Single-sentence paragraphs are forbidden in academic prose, used constantly
in real writing. They signal:

- **A turn in the argument**: "Then again, maybe not."
- **An emphasis the writer wants to land alone**: "The bot died at 2:47am last Tuesday."
- **A transition without a transition word**: "We spent Wednesday morning figuring out why."

Use them sparingly — once per 500 words is plenty. But use them.

## The question rule

AI writing rarely asks questions; when it does, it answers them
immediately in the next sentence. Real writing asks questions and lets
them hang, or answers them later, or doesn't answer at all.

```
Bad (immediate answer):  "Could we have caught it sooner? Yes, by
                          alerting on memory usage."

Good (delayed answer):   "Could we have caught it sooner? Probably.
                          The metric was there; we just didn't alert
                          on it. Now we do."

Good (no answer):        "Whether this matters at 200 people, I don't
                          know yet. Ask me in six months."
```

Questions in real writing carry weight because they admit uncertainty.
AI writing hates admitting uncertainty, so it answers instantly. Resist.

## The aside rule

Em-dashes and parentheticals insert asides — commentary that runs
alongside the main thread without breaking it. AI writing avoids them
because they break the smooth flow. Real writing uses them constantly
because that's how thought actually works.

```
Bad (no asides):   "We cap the batch at 8 diffs and added a memory gauge
                   to the dashboard."

Good (with aside): "We cap the batch at 8 diffs (was unbounded) and
                   added a memory gauge to the dashboard — the one we
                   should have added a week ago."
```

The aside carries information: the previous value, and the writer's
opinion about the delay. Smooth prose would lose both.

## The punctuation rule

| Mark | AI use | Human use |
|---|---|---|
| Comma | High | Moderate |
| Period | High | High |
| Em-dash | Low | High (for asides) |
| Semicolon | Low | Moderate (for related clauses) |
| Colon | Low | Moderate (for setup-payload) |
| Question mark | Low (and always answered) | Moderate (often unanswered) |
| Exclamation | Low | Low (don't overuse) |
| Parentheses | Low | Moderate (for asides) |

If your prose uses only commas and periods, it's flat. Add variety.

## The transition rule

AI writing uses explicit transition words at every paragraph boundary:
"furthermore," "moreover," "in addition," "however," "consequently."
These are padding. Real writing often transitions by:

- **Juxtaposition**: just put the next paragraph next to the previous one.
- **Time marker**: "Wednesday morning, we..."
- **Question**: "Could we have caught it sooner?"
- **Fragment**: "Fix:"
- **Repetition with variation**: "The bot died. We spent the next day asking why."

If you find yourself reaching for "furthermore" or "moreover," ask:
**would the paragraph work without it?** Usually yes. Delete.

## Heuristic questions

1. **List sentence lengths in a sample paragraph.**
   Min: __. Max: __. Ratio max/min?
   If ratio < 3, the paragraph is too uniform.
2. **List paragraph lengths in a sample section.**
   If all paragraphs are 3–5 sentences, vary them.
3. **Count fragments.**
   If 0 in 500 words, the prose is too formal. Add 1–2.
4. **Count one-sentence paragraphs.**
   If 0 in 1000 words, the prose is too uniform. Add 1.
5. **Count questions.**
   If 0, the prose admits no uncertainty. Add 1.
6. **Are any questions immediately answered?**
   If yes, delay or remove the answer.
7. **Count asides (em-dashes, parentheticals).**
   If 0 in 500 words, the prose has no commentary layer. Add 1–2.
8. **Count transition words (furthermore, moreover, additionally).**
   If more than 2 per 500 words, replace most with juxtaposition.
9. **Read aloud.** Does the prose have a beat?
   If it reads like a metronome, it's flat. Add rhythm.

## Anti-pattern: rhythm as performance

Adding fragments and asides **without content to anchor them** produces
a different kind of bad prose: choppy, affected,empty.

```
Bad (no content):  "We built it. Fast. Real fast. The platform —
                   if you can call it that — was a beast. Mostly."

Good (with content): "We built it in 6 weeks. Fast. The platform —
                    a single Go binary — was handling 4k req/s by
                    week 4. Mostly because we cut every feature
                    that wasn't on the critical path."
```

Rhythm supports content. It doesn't replace it.

## Instruction template

```
Shape the prose rhythm. Before producing, answer:

1. Sentence-length range in a sample paragraph:
   shortest __, longest __, ratio __
   If ratio < 3, rewrite to add variance.

2. Paragraph-length range in a sample section:
   shortest __ sentences, longest __ sentences
   If all 3–5, vary.

3. Count of fragments in 500 words:
   __. If 0, add 1–2 where the rhythm calls for a hit.

4. Count of one-sentence paragraphs in 1000 words:
   __. If 0, add 1 where a turn or emphasis lands alone.

5. Count of questions in 500 words:
   __. If 0, add 1 where the text genuinely admits uncertainty.

6. Are any questions immediately answered?
   If yes, delay or remove the answer.

7. Count of asides (em-dashes, parentheticals) in 500 words:
   __. If 0, add 1–2 where commentary belongs.

8. Count of transition words (furthermore, moreover, additionally):
   __ per 500 words. If > 2, replace most with juxtaposition.

9. Read aloud. Where does the prose go flat?
   Mark those spots. Vary the rhythm there.

Then produce the text. The rhythm should match the content: short
for impact, long for exploration, fragment for turn, question for doubt.
```
