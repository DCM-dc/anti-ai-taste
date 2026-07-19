# 04-rhetoric / 03 · Concept-coining

## Default reflex

- Inventing new terms for things that already have names
  ("Semantic Discovery Engine" for "search")
- Inventing "X's Law" / "The X Model" / "The X Framework" / "The X Index"
  for observations that aren't laws, models, or frameworks
- Inventing acronyms (FILE, AGM, RAG, A2A, KWI) for concepts that could
  be named in plain words
- Inventing "Five X" / "Three Y" / "Seven Z" symmetric taxonomies
  (Five Intelligences, Three Pillars, Seven Principles)
- Inventing "X-driven" / "X-native" / "X-first" marketing coinages
- Verb-noun coinages: "The Empowerment," "The Alignment," "The Convergence"
- Re-defining existing words as proprietary terms
  ("Skill" = Prompt + Tool bundled together)

## Why the reflex exists

In the training corpus, "high-quality" writing — academic papers, McKinsey
reports, thought-leader Substacks — coins terms. The model learned the
correlation: "deep writing has named concepts." It reproduces the form
without the underlying insight.

The reason humans coin terms is **lexical gap**: a new phenomenon exists,
no existing word describes it, the writer needs a name to refer to it.
The model has no such reason — it can always describe in plain words —
so it coins decoratively.

The result is text full of "X's Law" and "The X Model" that sounds deep
but explains nothing. The IOV Labs paper ranks this among the strongest
rhetorical tells, especially in "thought leadership" content.

## Bad example (the default, annotated)

> I'm excited to introduce the **Augmented Genesis Model (AGM)** — a new
> framework for thinking about human-AI collaboration. AGM is built on
> the **Five Intelligences**: AI (Artificial Intelligence), EQ
> (Emotional Intelligence), CQ (Creative Intelligence), PQ (Physical
> Intelligence), and AQ (Adaptive Intelligence).
>
> These five intelligences flow through the **5E Cascade**: Evolution,
> Effectiveness, Excellence, Ecosystems, and Empowerment. Together,
> they form the **Seven Co-Creative Intelligences** — what I call the
> **FILE⁵ Framework** for augmented leadership.
>
> In the **Augmented Genesis Model**, every interaction follows the
> **Law of Convergence**: as AI capability increases, the Five
> Intelligences collapse into a single unified field of augmented
> cognition. This is what I call the **Mariani Index (MI)** — a
> quantitative measure of co-creative alignment.

**Why this smells:**
- Six new terms in three paragraphs: AGM, Five Intelligences, 5E Cascade, Seven Co-Creative Intelligences, FILE⁵, Law of Convergence, Mariani Index.
- Every term is named with a symmetry tic (Five / 5E / Seven / FILE⁵).
- None of the terms refers to a phenomenon that lacks an existing name.
- "EQ" is hijacked from its established meaning (Emotional Quotient) and redefined.
- The "Law of Convergence" is not a law (it's an assertion).
- The "Mariani Index" has no formula, no measurement, no data.
- The whole passage is **the simulation of theory**, not theory.

## Good example (source-driven, annotated)

> When we write prompts, we usually give the model some context first,
> then ask it to do something. When we wrap that context-and-instruction
> pair with a few tools the model can call, we get something that behaves
> differently from a plain prompt — it can take actions, not just produce
> text. People call this an "agent," though the word is overloaded.
>
> I'm going to call it a "tool-calling prompt" in this post, because
> that's the only part that's actually different from a regular prompt.
> The "agent" framing suggests autonomy the model doesn't have; the
> "tool-calling prompt" framing is precise.
>
> Three things change when you add tools to a prompt:
> 1. The model can produce structured output (function calls) instead of text.
> 2. The system can execute the call and return the result to the model.
> 3. The model can chain calls together across turns.
>
> That's it. No "Five Pillars of Agentic Cognition," no "Tool-Calling
> Convergence Law." Just three concrete differences you can test.

**Why this doesn't smell:**
- The writer uses existing words ("prompt," "tool," "agent," "context") until they fail.
- They coin **one** term ("tool-calling prompt") and explicitly justify it:
  the existing word ("agent") is overloaded and misleading.
- They describe the new term by what it **does**, not by what it's "named."
- The "three things change" list is concrete and testable, not a symmetric taxonomy.
- They explicitly refuse to coin ("No 'Five Pillars of Agentic Cognition'").

## The lexical-gap rule

Coin a term only when **existing vocabulary genuinely fails**:

| Situation | Verdict |
|---|---|
| Existing word works ("search" for search) | Use existing word. Don't coin "Semantic Discovery Engine." |
| Existing phrase works ("prompt + tools bundled") | Use phrase. Don't coin "Skill." |
| Existing word is overloaded ("agent" means many things) | Coin a more precise term, with justification. |
| New phenomenon, no existing word | Coin a term, with definition. |
| Existing word is misleading ("agent" suggests autonomy the model lacks) | Coin a corrective term, with explanation. |
| You want to sound deep | Don't coin. Just say the thing. |

The test: **can you describe the concept in plain words in one sentence?**
If yes, don't coin. If no (the sentence is unwieldy, or you find yourself
repeating the phrase), maybe coin.

## The "law / model / framework" rule

These four words are the most-abused in AI writing:

| Word | When it's earned | When it's decoration |
|---|---|---|
| Law | Mathematical or empirical regularity with predictive power (Moore's Law, Amdahl's Law) | Any observation that sounds deep |
| Model | Formal representation with defined inputs, outputs, and relationships | Any framework for thinking about something |
| Framework | Set of interconnected concepts that produce testable predictions | Any collection of three or more ideas |
| Index | Numerical measure with a defined formula and data source | Any qualitative ranking dressed as a number |

If you write "X's Law," you must be able to state the law as an equation
or as a precise empirical claim with falsifiable predictions. If you can't,
it's not a law — it's an observation. Call it an observation.

If you write "The X Index," you must be able to give the formula and the
data source. If you can't, it's not an index — it's a vibe.

## The acronym rule

Acronyms (FILE, AGM, RAG, A2A, KWI) are easy to coin and hard to remember.
They almost always indicate decoration rather than precision.

- **Don't coin acronyms** unless the concept appears so often in the text
  that the full name becomes unwieldy.
- **If you coin one**, introduce it once with the full name, then use the
  acronym. Never lead with the acronym.
- **Don't re-define existing acronyms.** RAG means "Retrieval-Augmented
  Generation" in ML; don't redefine it as "Recursive Action Graph" in
  your agent post.

## The symmetry-tic rule

AI writing loves symmetric naming: "Five Intelligences," "5E Cascade,"
"Seven Co-Creative Intelligences," "Three Pillars," "Four Quadrants."

The symmetry is decorative. Real taxonomies have **whatever number of
items the domain has** — three, four, six, or seven, but not chosen for
symmetry. Amdahl's Law has two terms (parallelizable, non-parallelizable).
The CAP theorem has three. Neither chose the number for aesthetic reasons.

- **Don't pick the number first and find items to fit.**
- **Don't name items to fit a letter pattern (5E: Evolution, Effectiveness, ...).**
- **If you have 4 items, call it 4. If you have 6, call it 6. Don't fudge to 5.**

## The redefinition rule

Don't redefine existing words as proprietary terms. This is a McKinsey-
tell: "We define 'Skill' as a Prompt-Tool bundle in the LLM context."

- **"Skill"** has a meaning. Use it for that meaning.
- **"Agent"** has a meaning (multiple, actually). If you need a more
  precise term, coin a new one; don't redefine "agent."
- **"Empowerment"** has a meaning. Don't make it a proprietary concept.

Redefining existing words confuses readers and signals that the writer
cares more about coining than communicating.

## The "describe, don't name" rule

When you catch yourself reaching for a coinage, try this: **describe the
concept in plain words instead of naming it.**

```
Coining (decorative):  "This is the Mariani Index — a measure of
                       co-creative alignment between human and AI."

Describing (precise):  "You can roughly estimate how well a human-AI
                        pair is working by counting how often the human
                        has to redo the AI's output. Fewer redos = better
                        alignment. We logged 0.7 redos per task in week 1
                        and 0.3 in week 6."
```

The second version has no coined term, but it has **more information**:
the operational definition, the metric, the actual numbers. Coined terms
usually **replace** information; description **adds** information.

## Heuristic questions

1. **Count coined terms per 1000 words.**
   If more than 2, suspect decoration.
2. **For each coined term, can you describe the concept in one plain sentence?**
   If yes, delete the term; use the description.
3. **For each "Law," state the equation or falsifiable prediction.**
   If you can't, change to "observation."
4. **For each "Index," state the formula and data source.**
   If you can't, delete the index.
5. **For each acronym, did the full name appear first?**
   If not, introduce it.
6. **Are you redefining an existing word?**
   If yes, coin a new word instead.
7. **Did you pick the number first and find items to fit?**
   If yes, you're decorating. Stop.
8. **Did you name items to fit a letter pattern (5E: Evolution, Effectiveness...)?**
   If yes, you're decorating. Stop.
9. **Would this term appear in 1000 other AI "thought leadership" posts?**
   If yes, don't coin it.

## Anti-pattern: synonym coin

Replacing "Semantic Discovery Engine" with "Smart Search Layer" is not
escaping the tell. Both are coinages for "search."

```
Bad:    "Don't call it 'Semantic Discovery Engine,' call it 'Smart Search Layer.'"
                                                                       ← still coining
Good:   "Don't coin a term. It's search. Call it search.
        If you need to specify what kind, say 'search over
        embeddings' — three plain words, no coinage."         ← plain language
```

## Instruction template

```
Choose concept-coining strategy. Before producing, answer:

1. Count of coined terms in the piece:
   __. If > 2 per 1000 words, suspect decoration.

2. For each coined term, can you describe the concept in one plain sentence?
   Term: ___  → Plain description: ___
   If yes, delete the term; use the description.

3. For each "Law":
   State the equation or falsifiable prediction. If you can't, change to "observation."

4. For each "Index":
   State the formula and data source. If you can't, delete.

5. For each acronym:
   - Did the full name appear first?
   - Is the concept used often enough to need abbreviation?
   - Are you redefining an existing acronym?

6. Symmetry check:
   - Did you pick the number first (Five / Seven / Three)?
   - Did you name items to fit a letter pattern?
   If yes to either, you're decorating. Stop.

7. Redefinition check:
   Are you redefining an existing word (Skill, Agent, Empowerment)?
   If yes, coin a new word instead.

8. Could this term appear in 1000 other AI "thought leadership" posts?
   If yes, don't coin it. Use plain language.

Then produce the text. Use existing words until they fail. Coin only
when there's a genuine lexical gap. Describe, don't name.
```
