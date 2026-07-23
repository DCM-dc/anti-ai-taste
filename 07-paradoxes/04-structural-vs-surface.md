# 07-paradoxes / 04 · Structural vs surface tells

## The failure mode

The guide lists many tells: "delve," indigo gradients, `rounded-2xl`,
"not X but Y," forced elevation, "Build the future of work."

But these tells have **different lifespans**:

- Some are **structural** — caused by the transformer architecture
  itself, will persist across model generations.
- Some are **surface** — caused by the current training data and RLHF
  preferences, will fade as models iterate.

The guide conflates them. If a future model (GPT-6, Claude 5) naturally
stops using "delve," the guide's advice to avoid "delve" becomes
stale — and worse, agents following the guide will avoid a word that's
no longer a tell, while missing whatever new tells the model introduces.

This file separates the two, so the guide can age gracefully.

---

## Structural tells (architectural, stable)

These come from how transformers work. They will not fade with model
iteration. They might reduce in intensity, but the underlying mechanism
remains.

### 1. Regression to the mean

**Mechanism:** LLMs predict the most probable next token. The most
probable token is the modal one. Stacked, modal tokens produce modal
output — the centroid of the training distribution.

**Why it's structural:** This is the architecture. Next-token prediction
IS regression to the mean. No amount of RLHF removes it; RLHF shifts
the mean but doesn't eliminate the tendency.

**Tells it produces:**
- Colors cluster around `#3b82f6`–`#8b5cf6`
- Fonts cluster around Inter
- Layouts cluster around the standard landing page grammar
- Words cluster around the safest register

**Implication for the guide:** The "every choice must have a source"
rule is permanent. It addresses the structural tell directly.

### 2. Low burstiness

**Mechanism:** LLMs produce sentences whose lengths cluster around the
mean. Variance is low because high-variance sequences are less probable.

**Why it's structural:** Next-token prediction rewards the modal length.
Long sentences and short sentences are both less probable than
medium-length ones. The model converges on medium.

**Tells it produces:**
- All sentences 15–25 words
- All paragraphs 3–5 sentences
- All sections similar length
- No fragments, no one-sentence paragraphs

**Implication for the guide:** The rhythm rules (vary length, use
fragments, allow one-sentence paragraphs) are permanent.

### 3. Form faking content

**Mechanism:** RLHF rewarded "polished, complete, authoritative" output.
The model learned to produce the surface markers of authority
(quotes, summaries, coined terms) without the underlying substance
(real sources, real endings, real insight).

**Why it's structural:** As long as RLHF (or any human-preference
training) rewards "looks complete," the model will produce form without
content. The form-content gap is a training-objective artifact.

**Tells it produces:**
- Decorative quotes (Einstein, Jobs)
- Forced elevation endings
- Coined "X's Law" without mathematical content
- "Key Takeaways" lists restating the body

**Implication for the guide:** The rhetoric rules (quote only when
load-bearing, end where the thought ends, don't coin unless necessary)
are permanent.

### 4. Single-system flattening

**Mechanism:** The model applies the same value everywhere because
that's the modal treatment. One radius, one easing, one font, one
register — because differentiation requires extra reasoning the model
doesn't do by default.

**Why it's structural:** Differentiation is conditional reasoning
("this element class needs a different value because..."). Conditional
reasoning is harder than pattern matching. The model defaults to
pattern matching.

**Tells it produces:**
- `rounded-2xl` on everything
- `transition-all duration-300 ease-in-out` everywhere
- Inter alone
- One register throughout

**Implication for the guide:** The hierarchy rules (radius hierarchy,
motion vocabulary, font pairing, register variation) are permanent.

---

## Surface tells (current-model-specific, ephemeral)

These come from the current training data and RLHF preferences. They
will fade as models iterate and training data shifts.

### 1. Specific signature words

**Current:** delve, leverage, foster, harness, seamless, robust,
paradigm; 至关重要, 综上所述, 赋能.

**Why it's surface:** These words are overrepresented in current
training data (2020–2024 web, RLHF raters who preferred "polished"
prose). Future training data will dilute them. GPT-5 may already use
them less.

**Lifespan:** 1–3 years. The specific words will rotate; the
**density** of signature words will remain a structural tell.

**Implication:** The specific word list in `03-language/01-vocabulary.md`
needs periodic refresh. The **density rule** (≤3 per 500 words) is
permanent; the specific words on the list are not.

### 2. Specific color defaults

**Current:** indigo→violet→fuchsia gradient, `#3b82f6`, `#6366f1`.

**Why it's surface:** These are Tailwind defaults that dominated
2020–2024 web. As Tailwind's defaults shift and new design trends
enter training data, the centroid will move.

**Lifespan:** 2–4 years. The specific colors will rotate; the
**regression to a default palette** will remain structural.

**Implication:** The specific hex ban is ephemeral. The "palette must
have a source" rule is permanent.

### 3. Specific font defaults

**Current:** Inter alone.

**Why it's surface:** Inter dominates current web. As new fonts
become popular, the centroid will shift (already shifting toward
Geist, Sora).

**Lifespan:** 2–4 years.

**Implication:** The specific "don't use Inter alone" advice is
ephemeral. The "pair at least two families with reasons" rule is
permanent.

### 4. Specific layout defaults

**Current:** centered hero + 3-col features + 3-tier pricing + FAQ
accordion + 4-col footer.

**Why it's surface:** This grammar dominates current component
libraries (shadcn/ui, Tailwind UI). As new libraries emerge, the
grammar will shift.

**Lifespan:** 3–5 years. Layout grammars change slower than words
or colors.

**Implication:** The specific grammar ban is ephemeral. The "content
weight determines layout" rule is permanent.

---

## How to read the guide with this in mind

| Section | Structural (permanent) | Surface (ephemeral, needs refresh) |
|---|---|---|
| 02-visual/01-color | "Palette must have a source" | "Avoid indigo/violet" |
| 02-visual/02-typography | "Pair families with reasons" | "Avoid Inter alone" |
| 02-visual/03-layout | "Content weight determines grid" | "Avoid centered hero + 3-col" |
| 02-visual/04-surface | "Build a hierarchy" | "Avoid rounded-2xl" |
| 03-language/01-vocabulary | "Density rule" | "Specific word list" |
| 03-language/02-syntax | "Vary structure, avoid reflex" | "Avoid 'not X but Y'" |
| 04-rhetoric/01-quotation | "Quote only when load-bearing" | "Avoid Einstein/Jobs" |
| 04-rhetoric/03-concept-coining | "Don't coin unless lexical gap" | "Avoid 'X's Law'" |

The left column is the guide's permanent core. The right column is
current-model calibration that needs periodic refresh.

---

## The versioning protocol

The guide should be versioned by model era:

- **v1.x** — calibrated against GPT-4 / Claude 3 / current Llama.
  Surface tells: indigo, Inter, "delve," centered hero.
- **v2.x** — recalibrate when a new model generation dominates.
  Test: generate 100 outputs with the new model, count tells, update
  surface lists. Structural rules unchanged.

The test for "is this tell still active": generate 10 unconstrained
outputs with the target model. If the tell appears in >50% of outputs,
it's still active. If <20%, it's faded — remove from the surface list.

---

## How this fails if applied naively

If the guide treats all tells as eternal, it will:

- Tell agents to avoid "delve" in 2027, when "delve" is no longer a
  tell (the model naturally stopped using it).
- Miss the new tells the 2027 model introduces (whatever they are).
- Become a stale rulebook that fights the last war.

If the guide treats all tells as ephemeral, it will:

- Refuse to give specific advice, retreating to "avoid defaults"
  (useless in practice).
- Lose the operational specificity that makes it actionable.

The balance: **structural rules are eternal, surface lists are versioned.**

---

## Heuristic questions

1. **For each tell you're addressing, is it structural or surface?**
   - If structural: the rule is permanent.
   - If surface: the specific list needs versioning.
2. **When was the surface list last calibrated?**
   - If >12 months ago, retest against the current model.
3. **Are you banning a word/color/font that the current model no longer overuses?**
   - Generate 10 unconstrained outputs. Count the tell. If <20%, remove the ban.
4. **Are you missing new tells the current model introduces?**
   - Generate 10 unconstrained outputs. Look for patterns not in the guide. Add them.
5. **Are you treating a structural rule as if it were surface?**
   - "Vary sentence length" is structural. Don't drop it when models improve at burstiness.
6. **Are you treating a surface rule as if it were structural?**
   - "Avoid indigo" is surface. Don't treat it as eternal.

---

## Instruction template

```
When applying the guide, classify each rule:

STRUCTURAL (permanent, architecture-level):
  - "Every choice must have a source"
  - "Vary sentence length, include fragments"
  - "Quote only when load-bearing"
  - "Build radius/shadow/font hierarchies"
  - "Don't coin unless lexical gap"
  - "End where the thought ends"

SURFACE (versioned, current-model-specific):
  - Specific signature word list (refresh every 6–12 months)
  - Specific color hex list (refresh when Tailwind defaults shift)
  - Specific font list (refresh when web trends shift)
  - Specific layout grammar (refresh when component libraries shift)

For surface rules, before applying:
  - Was the list calibrated against the current model within 12 months?
  - If no, generate 10 unconstrained outputs and recount tells.
  - Remove bans for tells that have faded (<20% occurrence).
  - Add bans for new tells that have emerged.
```
