# 04-rhetoric / 01 · Quotation

## Default reflex

- Quote a famous person at the start of the article (Einstein, Jobs, Gandhi, Mandela)
- Quote a famous person at the end of the article (same set, plus Oprah, Churchill)
- Stack three quotes in a row from different authorities on the same point
- Use template structures: "古有 X，今有 Y" / "正如 X 所言：『……』"
- Quote studies without citing them: "studies show that..."
- Quote statistics without sourcing them: "80% of users report..."
- Invent quotes, studies, or statistics when none comes to mind (the worst tell)

## Why the reflex exists

In the training corpus, "high-quality" writing — academic papers, essays,
journalism — quotes outside voices. The model learned the correlation:
"good writing has quotes." It reproduced the form without the underlying
reason.

The reason humans quote is **load-bearing**: a quote brings in a voice
the writer can't replicate themselves, or evidence the writer can't
produce themselves. The model has no such reason — it can paraphrase
anything — so it quotes decoratively.

Worse, when the model can't recall a real quote that fits, it generates
one that sounds like it could be real. This is hallucination, and it's
the single most damaging form of the quotation reflex.

## Bad example (the default, annotated)

> As Albert Einstein once said, "Imagination is more important than
> knowledge." **In today's rapidly evolving landscape**, this sentiment
> **rings truer than ever**. The future of work demands creativity,
> and organizations that **embrace this paradigm** will thrive.
>
> **Studies show that** 87% of executives believe AI will transform
> their industry. **Furthermore**, **research indicates** that teams
> using AI tools are 40% more productive. As Steve Jobs famously noted,
> "Innovation distinguishes between a leader and a follower."
>
> **In conclusion**, the words of Gandhi remind us: "Be the change you
> wish to see in the world." The future belongs to those who **dare to
> dream**.

**Why this smells:**
- Three decorative quotes (Einstein, Jobs, Gandhi) — the modal "famous people" trio.
- Two unsourced statistics ("87%," "40%") with no study named.
- The quotes do no argumentative work — they're ornament.
- "Studies show" and "research indicates" are the AI tell for fabricated evidence.
- The structure is: famous quote → claim → fake stat → famous quote → famous quote. Pure decoration.

## Good example (source-driven, annotated)

> We rolled out the PR bot to 12 engineers in March. By April, average
> PR review time dropped from 2.1 days to 0.7 days, measured from PR
> open to merge. We didn't run a controlled study — it's an internal
> before/after on the same team.
>
> The closest thing to a published reference is Google's Eng Productivity
> Research group, which reported (Winters et al., 2022) that PR review
> latency correlates with developer satisfaction at r ≈ -0.4 across
> their sample of 5,000 engineers. Our numbers are smaller and our
> methodology is weaker, but the direction matches.
>
> I'm not going to claim this generalizes. Twelve engineers, one team,
> one quarter. Take it as a data point, not a recommendation.

**Why this doesn't smell:**
- No famous quotes. None are needed — the writer is reporting their own data.
- One real citation (Winters et al., 2022) with specific scope (5,000 engineers).
- Numbers are sourced: "measured from PR open to merge" tells you what the metric is.
- Hedging is specific: "I'm not going to claim this generalizes" — one hedge, with a reason.
- The writer admits weakness ("our methodology is weaker") — something AI writing almost never does.
- No "studies show" without a study. No "research indicates" without research.

## The load-bearing rule

A quote is **load-bearing** if removing it would collapse or weaken the
argument. A quote is **decorative** if removing it changes nothing.

| Quote type | Verdict |
|---|---|
| Einstein: "Imagination is more important than knowledge" in an article about creativity | Decorative — the article makes the same point without it |
| A direct quote from a user interview: "We saved 40 seconds per PR; doesn't sound like much but it's 6 minutes a day, 30 minutes a week" | Load-bearing — the user's voice carries the meaning |
| "As Steve Jobs said, innovation distinguishes leaders from followers" in a startup pitch | Decorative — and embarrassing |
| A quote from the actual research paper's discussion section, explaining the surprising finding | Load-bearing — you can't paraphrase the authors' interpretation |

**Quote only when load-bearing.** If you can paraphrase, paraphrase.

## The source rule

Every quoted statistic, study, or claim must have a **named source**:

| Vague (AI) | Sourced (human) |
|---|---|
| "studies show that..." | "Winters et al., 2022, ICSE Proceedings" |
| "research indicates..." | "Google's Eng Productivity Research group, internal study of 5,000 engineers" |
| "many experts believe..." | (delete — if you can't name them, don't cite them) |
| "80% of users report..." | "in our survey of 47 paying users, 38 reported..." |
| "in recent years..." | "between 2020 and 2024..." |

If you cannot name the source, **do not write the claim**. Vague
sources are the AI tell; hallucinated sources are worse.

## The no-hallucination rule (hard ban)

**Never invent quotes, studies, statistics, or citations.** This is the
single most damaging thing AI writing does. A wrong number with
confidence is worse than no number at all.

If you cannot recall a real source:
- Don't write the claim.
- Or write the claim and mark it explicitly: "[source needed]" / "I don't have a citation for this."
- Or use the writer's own data: "in our internal test on 12 engineers..."

Hallucinated citations have ended careers. Don't do it.

## The famous-quotes rule

The modal famous-quotes set is: Einstein, Jobs, Gandhi, Mandela, Oprah,
Churchill, Twain, Edison. These appear in AI text with absurd frequency.

- **Avoid all of them by default.**
- **If you must quote a famous person, pick one less obvious** (a
  specialist in the field, a writer on the topic, a practitioner).
- **Never quote Einstein, Jobs, or Gandhi in a marketing piece.**
  The combination is instantly recognizable.

The test: would this quote appear in 1000 other AI-generated articles on
this topic? If yes, don't use it.

## The "quote then analyze" rule

A quote without analysis is ornament. After every quote, the writer must
**do something with it**: extend it, qualify it, argue with it, apply it.

```
Bad (no analysis):  "As Einstein said, imagination is more important
                    than knowledge." [moves to next paragraph]

Good (analyzed):    The engineering director put it bluntly: "We don't
                    need more dashboards. We need fewer, and we need
                    them to be right." She'd been saying this for six
                    months before we listened. The dashboards we cut
                    had been showing metrics no one acted on; the ones
                    we kept got maintained.
```

The first quote is decoration. The second carries information and is
followed by the writer doing the work of applying it.

## The Chinese-template rule

Chinese AI writing has its own quotation templates that are just as
recognizable as English ones:

| Template | Verdict |
|---|---|
| "古有 X，今有 Y" | Decorative — avoid |
| "忆往昔…看今朝…思未来…" | Decorative — avoid |
| "正如 X 所言：『……』" | Acceptable if load-bearing |
| 三连排比引用 (X 说过…Y 也指出…Z 进一步强调…) | Almost always decorative — avoid |

The same rule: quote only when load-bearing, and analyze after.

## Heuristic questions

1. **Count quotes per 1000 words.** If more than 2, suspect decoration.
2. **For each quote, what argumentative work does it do?**
   If none, delete.
3. **Could you paraphrase the quote without losing meaning?**
   If yes, paraphrase.
4. **Is the quote from Einstein, Jobs, Gandhi, Mandela, Oprah, or Churchill?**
   If yes, replace with a less-modal source or delete.
5. **For each statistic, name the source.**
   If you can't, delete the statistic.
6. **For each "studies show" or "research indicates" — which study?**
   If unnamed, delete.
7. **Are you inventing any quote, study, or statistic?**
   If you're not sure it's real, don't write it. Mark as [source needed].
8. **After each quote, do you analyze it?**
   If not, delete the quote.
9. **Are you using a Chinese template ("古有 X, 今有 Y")?**
   If yes, replace with content.

## Anti-pattern: source swap

Replacing "Einstein" with a less-famous physicist is still decoration
if the quote doesn't do work.

```
Bad:    "Don't quote Einstein, quote Feynman instead."    ← still decoration
Good:   "Don't quote physicists in this article. We have
        our own data — 12 engineers, 2.1 days to 0.7 days.
        That's the quote. Cite ourselves."                ← source-driven
```

## Instruction template

```
Choose quotation strategy. Before producing, answer:

1. Count of quotes in the piece:
   __. If > 2 per 1000 words, suspect decoration.

2. For each quote, answer:
   - What argumentative work does it do?
   - Could it be paraphrased without loss?
   - If "no work" or "could paraphrase," delete.

3. Famous quotes check:
   Are any from Einstein / Jobs / Gandhi / Mandela / Oprah / Churchill?
   If yes, replace or delete.

4. Statistics check:
   For each statistic, name the source.
   Unnamed source → delete.
   Hallucinated source → delete immediately.

5. "Studies show" / "research indicates" check:
   Which study? Which researchers? If unnamed, delete.

6. Quote-then-analyze check:
   After each quote, is there analysis? If not, delete the quote.

7. Chinese template check:
   Any "古有 X, 今有 Y" or 三连排比引用? If yes, replace with content.

8. Hallucination check:
   Are you confident every quote and statistic is real?
   If not, mark [source needed] or remove.

Then produce the text. Quote only when load-bearing. Cite only what's real.
```
