# 07-paradoxes / 06 · Cross-domain coherence

## The failure mode

The guide treats visual, language, and rhetoric as independent layers.
Each has its own directory (`02-visual/`, `03-language/`, `04-rhetoric/`)
and its own checklist.

But real output is **one artifact**. A landing page has a palette AND
copy AND a quotation strategy. An article has typography AND sentence
rhythm AND concept-coining. If the layers are decided independently,
they fight each other:

- Warm hand-crafted palette + corporate-signature-word copy = mismatch
- Industrial-control-panel typography + whimsical fragments = mismatch
- Data-first dashboard layout + forced-elevation marketing ending = mismatch

The smell isn't always in any single layer. Often it's in the **seam**
between layers — each layer individually fine, but together incoherent.

---

## The coherence rule

> **All Tier 1 decisions (see `05-decision-tiers.md`) must share a single source.**

If the palette comes from "hand-made ceramics in Portugal," the typography,
layout, copy register, and interaction model must also derive from that
same source. If the typography comes from "industrial control panel
heritage," the palette and copy can't be "warm and artisanal."

The source is **one story**. Every Tier 1 decision is a facet of that story.

---

## The shared-source test

After deciding all Tier 1 layers, run this test:

> **Can you tell the story of this product in one sentence that explains
> all the Tier 1 decisions?**

### Bad (incoherent)

```
Palette:   warm cream + burnt sienna (source: hand-made ceramics)
Typography: Inter + JetBrains Mono (source: "clean and techy")
Layout:    centered hero + 3-col features (source: default)
Copy:      "Build the future of work" (source: marketing default)
Rhetoric:  Einstein quote at the end (source: decorative)

Story: "This product is hand-made ceramics that is also clean and techy
       and uses the default landing page and quotes Einstein."
→ Incoherent. The layers fight.
```

### Good (coherent)

```
Palette:   warm cream + #c2592e (source: hand-made ceramics, unglazed clay)
Typography: Fraunces + IBM Plex Sans (source: editorial heritage of
            craft publications; Fraunces' opsz axis matches the
            "made by hand" variability)
Layout:    asymmetric, single long column (source: editorial essay,
            not marketing — ceramics is a story, not a product)
Copy:      first-person, specific (source: the maker's voice, not
            marketing copy)
Rhetoric:  no quotes, no summary, end on a specific moment (source:
            the maker describing a specific firing)

Story: "This is a hand-made ceramics studio; every layer reflects
       the maker's voice and the material's character."
→ Coherent. One story, many facets.
```

---

## Common coherence failures

### 1. Visual warm + copy cold

```
Palette: warm cream + sienna (hand-crafted)
Copy:    "Leverage our comprehensive solution to supercharge workflows"
```

The palette says "hand-made." The copy says "enterprise SaaS." Readers
feel the dissonance without being able to name it.

**Fix:** Copy register must match palette source. If palette is
hand-crafted, copy is first-person, specific, and uses plain words.

### 2. Layout data-first + ending marketing

```
Layout:  dashboard, data-first, no hero
Ending:  "Start your journey today. Join thousands of teams."
```

The layout says "tool." The ending says "marketing site." The user is
either a customer (no marketing needed) or a prospect (no dashboard).

**Fix:** If layout is data-first (tool), ending is functional (status
line, version, support email). If layout is marketing, ending can be
CTA — but see `04-rhetoric/02-summarization.md` for forced-elevation
rules.

### 3. Typography industrial + rhetoric decorative

```
Typography: IBM Plex Sans + Mono (industrial control panel)
Rhetoric:   "Augmented Genesis Model" + "Five Intelligences" coinages
```

The typography says "field tool." The rhetoric says "thought leadership."
Field tools don't coin terms; they describe procedures.

**Fix:** If typography is industrial, rhetoric uses plain procedural
language ("three things change when you add tools"), no coinages.

### 4. Voice fragment-heavy + content technical

```
Voice:   fragments, "I went back to bed," asides
Content: API reference documentation
```

The voice says "personal essay." The content says "reference." Users
reading API docs don't want fragments; they want completeness and
predictability.

**Fix:** Voice must match genre. API docs use complete sentences, no
fragments, no asides. Personal essays can fragment. See `08-genres/`
for genre-specific voice rules.

---

## The coherence check (added to self-check)

After Q10 (second-order convergence), run Q11:

### Q11. Cross-domain coherence

**Can you tell the story of this product in one sentence that explains
all the Tier 1 decisions?**

- If yes, and the sentence is coherent → ✓
- If the sentence is a Frankenstein ("hand-made ceramics that is also
  clean and techy and quotes Einstein") → ✗, redo the layers that
  don't fit

**For each pair of layers, do they share a source?**

| Pair | Check |
|---|---|
| Palette ↔ Typography | Do they come from the same story? |
| Palette ↔ Copy register | Does the copy sound like the palette? |
| Layout ↔ Ending | Does the ending match the layout's intent? |
| Typography ↔ Rhetoric | Does the rhetoric fit the type's personality? |
| Voice ↔ Genre | Does the sentence rhythm match the content type? |

If any pair conflicts, **whichever layer has the weaker source loses**.
Redo it to match the stronger-sourced layer.

---

## How this fails if applied naively

If the agent treats "coherence" as "everything the same," it produces
**monotone output** — every layer identical, no variation. That's a
different smell (over-uniform, sterile).

Coherence is not sameness. It's **shared source, differentiated role**.
The palette and typography come from the same story (hand-made ceramics)
but do different jobs (palette = material, typography = voice). They
cohere without being identical.

The test is the **one-sentence story**, not layer-by-layer similarity.

---

## Heuristic questions

1. **What is the one-sentence story of this product?**
   If you can't write it, the layers don't cohere.
2. **For each Tier 1 layer, does it derive from that story?**
   If any layer derives from a different story, you have a coherence failure.
3. **Does the copy register match the palette?**
   Warm palette + corporate copy = mismatch.
4. **Does the ending match the layout's intent?**
   Dashboard + marketing CTA = mismatch.
5. **Does the rhetoric match the typography's personality?**
   Industrial type + coined terms = mismatch.
6. **Does the voice match the genre?**
   Fragments in API docs = mismatch. (See `08-genres/`.)
7. **Is the output monotone (everything identical)?**
   Coherence is shared source, not sameness. Differentiate roles.

---

## Instruction template

```
After all Tier 1 decisions are made, run coherence check:

ONE-SENTENCE STORY:
  "This product is [source story]; every layer reflects [facet]."
  Can you write this sentence? If no, layers don't cohere. Redo.

PAIRWISE COHERENCE:
  palette ↔ typography: same story? [yes/no]
  palette ↔ copy register: copy sounds like palette? [yes/no]
  layout ↔ ending: ending matches layout intent? [yes/no]
  typography ↔ rhetoric: rhetoric fits type personality? [yes/no]
  voice ↔ genre: rhythm matches content type? [yes/no]

For any "no": identify which layer has the weaker source.
Redo that layer to derive from the stronger layer's source.

MONOTONE CHECK:
  Are all layers identical (no differentiation)?
  If yes: differentiate roles. Palette = material, typography = voice,
  layout = structure, copy = personality. Same story, different facets.
```
