# 04-rhetoric / 02 · Summarization

## Default reflex

- End every paragraph with a one-sentence summary of that paragraph
- End every section with a "key takeaway" or "in short" recap
- End every article with a "in conclusion" / "to sum up" / "综上所述" paragraph
- End with forced elevation: "this reminds us that..." / "in this era of..."
  / "the future belongs to..." / "在这个……的时代"
- Add a "Key Takeaways" bullet list at the end of every long-form piece
- Use the sandwich structure: intro → body → conclusion, all three similar length

## Why the reflex exists

RLHF training rewarded "complete" output. Raters gave high scores to
pieces that "wrapped up neatly." The model learned: summary = quality
correlation. So it summarizes everywhere — at paragraph end, section
end, article end — and elevates the summary to "deep" closure.

The problem: human writers summarize **once, at the natural end**, and
often don't summarize at all (they just stop). The model summarizes
constantly because the correlation says summary = good.

The forced elevation is a specific sub-reflex: raters preferred
"meaningful" endings, so the model adds a philosophical flourish to
every piece, regardless of whether the content earned one.

## Bad example (the default, annotated)

> The new platform provides a comprehensive set of features for modern
> teams. It includes task management, time tracking, and reporting
> capabilities. Users can create projects, assign tasks, and monitor
> progress in real time. **In short, the platform offers everything
> teams need to succeed.**
>
> <!-- ↑ paragraph-level summary. The paragraph summarized itself. -->
>
> Integration with third-party tools is fully supported. The platform
> connects with Slack, GitHub, and Google Workspace. This allows teams
> to maintain their existing workflows. **As a result, teams can work
> more efficiently.**
>
> <!-- ↑ another paragraph-level summary. Same pattern. -->
>
> Security is a top priority. All data is encrypted. The platform
> complies with SOC 2 and GDPR. **Therefore, users can trust the
> platform with their data.**
>
> <!-- ↑ another. Three paragraphs, three mini-summaries. -->
>
> **In conclusion**, the new platform **represents a paradigm shift** in
> how teams collaborate. **In today's fast-paced world**, organizations
> that **embrace this transformative technology** will thrive. **The
> future belongs to those who** dare to innovate. **As we look ahead**,
> one thing is clear: **this is just the beginning**.
>
> <!-- ↑ forced elevation. The piece ends on a "deep" note it didn't earn. -->

**Why this smells:**
- Every paragraph has a one-sentence summary at the end.
- The article has a meta-summary at the end ("In conclusion...").
- The ending elevates: "paradigm shift," "transformative technology," "the future belongs to."
- The sandwich structure is rigid: intro / body / conclusion, all roughly equal weight.
- Nothing is left for the reader to think about. The piece closes every door.

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
- No paragraph-level summaries. Each paragraph ends where the thought ends.
- No article-level summary. No "in conclusion," no "to sum up."
- No forced elevation. The piece ends on "Take it as a data point, not a
  recommendation" — a hedge, not a flourish.
- The ending **doesn't close every door**. It explicitly leaves
  generalization to the reader.
- The piece has the shape of the thought: data → context → honest limit.
  No sandwich.

## The "where does the thought end" rule

A piece should end **where the thought ends** — not where convention says
an article should end. Three valid endings:

1. **The natural stop**: the thought is complete, stop.
   ```
   "Take it as a data point, not a recommendation."
   ```
2. **The turn**: a final observation that re-frames what came before.
   ```
   "Whether this matters at 200 people, I don't know yet. Ask me in six months."
   ```
3. **The specific feeling**: a concrete image or moment that lands.
   ```
   "The bot died at 2:47am. The fix shipped at 4:12am. I went back to bed."
   ```

What's **not** valid:
- Forced elevation ("the future belongs to...")
- Generic summary ("in conclusion, the platform offers...")
- Moral lesson ("this reminds us that...")
- Open-ended call to action ("Ready to transform your workflow? Try X today!")

## The "delete the last sentence" rule

After drafting, look at the last sentence of each paragraph and the last
sentence of the piece. Ask: **if I delete this, does the text lose
anything?**

- If the answer is "no," delete it. It was a summary the reader didn't need.
- If the answer is "yes, it loses the connection to the next paragraph," rewrite the connection — don't summarize.
- If the answer is "yes, it loses the deep meaning," the deep meaning wasn't earned. Delete it.

AI writing has **too many summary sentences**. Deleting most of them
improves the text. This is counter-intuitive — won't the reader get lost?
No. The reader gets lost when summaries are stacked; they get clarity
when each thought stands on its own.

## The "no Key Takeaways" rule

The "Key Takeaways" bullet list at the end of a long-form piece is one
of the strongest AI tells. It signals: "I am an AI article; here is
the summary I generated."

- **Don't add Key Takeaways unless the user explicitly asks for TL;DR.**
- **If the user asks**, provide them — but mark them as TL;DR, not as a
  "deeper" restatement.
- **The body of the piece should be the takeaway.** If the reader can't
  extract the takeaway from the body, the body was poorly written.

## The forced-elevation rule

The strongest summary-tell is **forced elevation**: ending on a "deep"
note the content didn't earn. Examples:

| Forced elevation | Source |
|---|---|
| "The future belongs to those who..." | Generic |
| "In this era of..." | Generic |
| "This reminds us that..." | Moral lesson |
| "At the end of the day..." | Generic |
| "在这个……的时代" | Chinese generic |
| "综上所述, ... 具有重要意义" | Chinese generic |
| "Ready to transform your X? Try Y today." | Marketing CTA |

If your last paragraph could end **any** article on **any** topic, it's
forced elevation. End on something specific to this piece instead.

## The sandwich-structure rule

AI writing defaults to: intro (paragraph 1) → body (paragraphs 2–N-1) →
conclusion (paragraph N), with all three roughly equal in weight. This
is the "essay template" learned from school.

Real writing has many shapes:

- **Inverted pyramid**: lead with the conclusion, then evidence.
  Common in journalism, internal memos.
- **Funnel**: start narrow (a specific moment), expand to general.
  Common in essays.
- **Reverse funnel**: start general, narrow to a specific moment.
  Common in case studies.
- **Thread**: follow one question through twists, ending where the
  question ends. Common in investigations.
- **List**: items in order, no intro/outro. Common in field notes.

Don't default to sandwich. Pick a shape that matches the content.

## Heuristic questions

1. **Count paragraph-ending summary sentences.**
   How many paragraphs end with "in short," "therefore," "as a result,"
   "in other words," "thus"?
   If more than 30% of paragraphs, cut most of them.
2. **Does the article have a "In conclusion" or "综上所述" paragraph?**
   If yes, ask: does the reader need it? Often no. Delete.
3. **Does the article end on forced elevation?**
   List the last sentence. Could it end any article on any topic?
   If yes, replace with something specific.
4. **Is there a "Key Takeaways" list?**
   If yes and the user didn't ask, delete it.
5. **What shape is the piece?**
   Sandwich (intro-body-conclusion)? Or something else?
   If sandwich, justify why this content needs that shape.
6. **Apply the "delete last sentence" test.**
   For each paragraph, would deleting the last sentence lose anything?
   Often no. Delete.
7. **Does the ending close every door, or leave some open?**
   Real writing often leaves doors open. AI writing closes them all.

## Anti-pattern: ending swap

Replacing "in conclusion" with "ultimately" is not escaping the tell.
Both are AI summary signals. The cure is **no summary signal** — end
where the thought ends.

```
Bad:    "Don't write 'in conclusion,' write 'ultimately' instead."  ← same reflex
Good:   "Don't write a summary paragraph at all. End where the
        thought ends. 'Take it as a data point, not a
        recommendation.' Done."                                    ← natural stop
```

## Instruction template

```
Choose summarization strategy. Before producing, answer:

1. Paragraph-level summaries:
   How many paragraphs end with "in short," "therefore," "thus"?
   If > 30% of paragraphs, delete most.

2. Article-level summary:
   Is there a "In conclusion" / "综上所述" paragraph?
   If yes, justify. Often delete.

3. Forced elevation check:
   Last sentence of the piece: ___
   Could it end any article on any topic? If yes, replace with
   something specific to this piece.

4. Key Takeaways list:
   Is there one? If yes and user didn't ask, delete.

5. Sandwich structure check:
   Is the piece intro → body → conclusion with equal weight?
   If yes, justify. Or reshape:
   [ inverted pyramid | funnel | reverse funnel | thread | list ]

6. Delete-the-last-sentence test:
   For each paragraph, would deleting the last sentence lose anything?
   Often no. Delete.

7. Door-closing check:
   Does the ending close every door, or leave some open?
   Real writing often leaves doors open.

Then produce the text. Summarize only at the natural end. End where
the thought ends, not where convention says an article should end.
```
