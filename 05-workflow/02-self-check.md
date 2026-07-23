# 05-workflow / 02 · Self-check

## Default reflex

- Produce output
- Read it once
- "Looks good"
- Deliver

No self-check. Or: a self-check that consists of "is it polished?" —
which is the same as no self-check, because the model's default output
already reads as polished to itself.

## Why the reflex exists

LLMs are trained to be confident. Self-doubt reads as low-quality to
RLHF raters, so the model learned to skip self-critique. The result is
**delivery without verification**, which is the modal failure mode for
AI output.

The fix is not "be less confident." It's **specific heuristic questions
that the model must answer out loud before delivering.** If the model
can't answer a question, it must redo the corresponding decision.

## Bad example (the default, annotated)

```
Model:   [produces landing page]
         [reads once]
         "This looks good. Delivering."
         [delivers]

User:    This looks like every other AI landing page.

Model:   "You're right. Let me tweak the color."
         [swaps indigo for violet]
         "Better?"

User:    Still generic.

Model:   "Okay, different font."
         [swaps Inter for Roboto]
```

**Why this smells:**
- No self-check ran.
- "Looks good" is the model's reflexive assessment of its own output. It will always say "looks good."
- Patching follows the same pattern as the bad workflow in `01-process.md`:
  value swaps, not structural rethinks.

## Good example (source-driven, annotated)

```
Model:   [produces landing page]
         [runs self-check]

         Q1. Where did the palette come from?
         A1. Brand logo (#2d5a3d), darkened 8% for AA on cream.
            ✓ Has source.

         Q2. Where did the typography come from?
         A2. IBM Plex Sans — chosen for industrial control panel heritage.
            ✓ Has source.

         Q3. Is this my first guess for layout?
         A3. ...actually, the 7/5 asymmetric grid was my first guess
            for this content, but I notice I also defaulted to a
            navbar with right-aligned CTA. Let me check — does a
            field tool need a marketing CTA in the nav?
            [realizes: no, the user is already a customer]
            [redoes nav: removes CTA, makes it compact, left-aligned]
            ✓ Caught a default, fixed it.

         Q4. Could this design appear in 1000 other AI outputs?
         A4. The dashboard-first approach with no marketing hero is
            unusual — most AI would default to hero. ✓ Passes.
            But the "features" section I included uses 3 equal cards.
            Are these 3 features actually equal weight?
            [checks: no — live voltage is primary, drift detection
             is secondary, field notes is tertiary]
            [redoes: 7/3/2 asymmetric grid instead of 3 equal cards]
            ✓ Caught a default, fixed it.

         Q5. Signature words in copy?
         A5. Let me scan... "comprehensive," "seamless," "robust."
            3 in 200 words. Over threshold.
            [rewrites copy: replaces with specific facts]
            ✓ Caught signature words, fixed.

         Q6. Forced elevation at the end?
         A6. The CTA section ends with "Start your journey today."
            That's forced elevation. Delete.
            [removes, ends on the dashboard preview]
            ✓ Caught forced elevation, fixed.

         Q7. Hallucinated quotes or statistics?
         A7. None. All claims are about the product itself.
            ✓ Passes.

         Q8. Coined terms?
         A8. None.
            ✓ Passes.

         Self-check complete. Delivering.
```

**Why this doesn't smell:**
- The self-check is **specific questions with required answers**.
- Each question either passes or triggers a redo.
- The model caught 3 defaults in self-check (nav CTA, equal feature cards, signature words, forced elevation).
- The delivered version is the **second internal draft**, not the first.

## The ten-question self-check

Run these ten questions before delivering. For each, you must answer
**out loud** with a specific response. If you can't answer, or the answer
is "this is my first guess," redo the corresponding decision.

> Questions 1–8 are the original self-check. Questions 9–10 were added
> after the paradox layer (`07-paradoxes/`) — they catch the failure
> modes that emerge when the guide is applied naively. If you skip 9–10,
> you will produce hallucinated-justification output that's worse than
> honest defaults.

### Q1. Source for each major decision

For color, typography, layout, surface, motion, icon strategy —
**where did this come from?**

- Acceptable: "brand logo hex," "industrial control panel heritage,"
  "user said 'warm and quiet'."
- Unacceptable: "looks modern," "clean and professional," "it's the default."

If any decision has no source, redo it. Find a source, or pick a different
decision that has one.

### Q2. First-guess detection

**Is this my first guess?** If yes, what would the second and third be?

- If you can't generate alternatives, you haven't escaped the default.
- Generate at least 2 alternatives for each major decision.
- Pick the one with the best source. If it's still the first guess,
  that's fine — but you've verified it's a choice, not a reflex.

### Q3. The "1000 other AI outputs" test

**Could this same [color / layout / sentence / structure] appear in 1000
other AI outputs?**

- If yes, it's the centroid. Source harder.
- If no, you've made a specific choice. ✓

### Q4. The "delete this" test

For each element (sentence, section, design decision), **if I delete it,
does the output lose anything?**

- If "no," delete it. It was decoration.
- If "yes, it loses the connection to the next thing," rewrite the
  connection — don't decorate.
- If "yes, it loses deep meaning," the deep meaning wasn't earned. Delete.

This applies to: summary sentences, transition words, decorative quotes,
"Key Takeaways" lists, gradients, icons on feature cards, glassmorphism
overlays, and any other ornament.

### Q5. Signature-word density

**Count signature words per 500 words.** (See `03-language/01-vocabulary.md`.)

- 0–1: ✓
- 2–3: borderline, rewrite some
- 4+: redo

### Q6. Forced elevation check

**Last sentence of the piece: could it end any article on any topic?**

- "The future belongs to those who..." → forced elevation. Replace.
- "Take it as a data point, not a recommendation." → specific. ✓
- "In this era of..." → forced elevation. Replace.
- "The bot died at 2:47am. The fix shipped at 4:12am. I went back to bed." → specific. ✓

### Q7. Hallucination check

**Is every quote, statistic, citation, and reference real?**

- If you're not sure, mark as [source needed] or remove.
- Never deliver a hallucinated source. This is the most damaging AI failure.

### Q8. Coinage check

**Did I coin any terms?**

- For each coined term: can I describe it in plain words instead?
  If yes, delete the coinage.
- For each "Law" / "Model" / "Framework" / "Index": can I state the
  formula or falsifiable prediction? If not, change to "observation."
- Did I redefine an existing word? If yes, coin a new one instead.

### Q9. Source tier verification (from `07-paradoxes/02-source-verification.md`)

**For each source I cited in Q1, which tier is it?**

Classify every source claim:

- **Tier 1 (verifiable external):** user-provided asset (logo file,
  brand doc), URL, cited paper/standard, user's explicit statement,
  real measurement.
  *Test: can I point to where this came from?*
- **Tier 2 (conventional, lookup-verifiable):** domain convention
  (amber = warning), established standard (WCAG), widely-known fact
  (Inter is Tailwind's default).
  *Test: could a human verify this by a 30-second web search?*
- **Tier 3 (asserted, hallucination risk):** affective claims
  ("evokes warmth," "feels hand-made," "matches heritage," "conveys
  authenticity").
  *Test: is this a claim about how something "feels" or "evokes"?*

**Rules:**
- Tier 1 and Tier 2 count as sources. ✓
- Tier 3 does NOT count. Remove the source claim. Replace with
  "first guess (no source provided)" or "default, marked for review." ✗
- **Did I invent any user-provided assets?** If I claimed "user-provided
  logo.svg" without the user providing it, that's a hallucination. Remove.
- **Am I using "evokes" / "feels" / "matches" / "conveys" anywhere?**
  These are Tier 3 markers. Remove.

**Count after verification:**
- Tier 1 sources: ___
- Tier 2 sources: ___
- First-guess admissions: ___
- Tier 3 hallucinations removed: ___ (must be 0 before delivery)

If Tier 3 count > 0 before removal, you were hallucinating sources.
Run again until 0.

### Q10. Second-order convergence check (from `07-paradoxes/01-second-order-convergence.md`)

**Could this output appear in 1000 other outputs made with this same guide?**

For each source cited in Q1 (and verified in Q9), apply the specificity floor:

> *Could this same source apply to 1000 other projects?*

- "The brand is warm" → yes, applies to 1000 → not specific enough
- "The brand is hand-made ceramics in Portugal" → no, applies to ~5 → specific enough
- "Inter is clean" → yes → not specific enough
- "The founder's previous publication used Tiempos" → no → specific enough

**New anti-AI defaults check.** Am I reaching for these without a
specific source?
- Burnt sienna / forest green / ochre on warm cream
- Fraunces + IBM Plex Sans (or Sora + Inter)
- Asymmetric 7/5 grid with no hero
- Fragments and "I went back to bed" endings
- Custom IEC-style SVGs
- "Field tech reading in sun" user persona

If yes without a source unique to this input, I've **relocated to a new
centroid, not escaped defaults**. Redo with sources that couldn't apply
to 1000 other projects.

**The test:** if 1000 agents followed this guide with 1000 different
users, would my output be distinguishable? If no, the sources weren't
specific enough.

## Domain-specific self-checks

In addition to the ten universal questions, run the matching
domain-specific checklist:

- **Visual output**: run `06-checklist/visual-checklist.md`
- **Text output**: run `06-checklist/language-checklist.md`
- **Argumentative / long-form output**: also run `06-checklist/rhetoric-checklist.md`

The universal self-check catches cross-cutting defaults. The domain
checklists catch domain-specific ones.

## The "out loud" rule

The self-check must be **explicit**. The model must answer each question
in plain text, in the response, before delivering. Silent self-check is
no self-check — the model will rubber-stamp its own output if not forced
to articulate.

If you're an agent reading this: when you deliver output, **show the
self-check**. The user can verify you actually ran it, not just claimed
to. If the self-check reveals a default you fixed, mention it — that's
evidence the process worked, not evidence of failure.

## Heuristic questions

The self-check IS the heuristic. Run all eight before delivering.

## Anti-pattern: rubber-stamp self-check

```
Bad:    [runs self-check]
        Q1. Source? "Yes, has source."           ← no specifics
        Q2. First guess? "No, considered."        ← no alternatives
        Q3. 1000 other outputs? "No, it's specific."  ← no evidence
        Q4. Delete test? "All necessary."         ← no deletions
        Q5. Signature words? "None."              ← no count
        Q6. Forced elevation? "No."               ← no last sentence quoted
        Q7. Hallucination? "None."                ← no scan
        Q8. Coinage? "None."                      ← no scan
        [delivers unchanged]
                                                              ← rubber stamp

Good:   [runs self-check]
        Q1. Source? "Palette: brand #2d5a3d. Type: Plex Sans for industrial heritage. ..."
        Q2. First guess? "Layout was first guess (7/5 grid). Alternatives: full-bleed photo, single column. Picked 7/5 because user is field tech."
        Q3. 1000 other outputs? "Dashboard-first with no marketing hero is unusual; AI defaults to hero. ✓"
        Q4. Delete test? "Deleted 'Start your journey today' CTA — forced elevation. Kept dashboard preview — load-bearing."
        Q5. Signature words? "3 per 500 words: 'comprehensive,' 'seamless,' 'robust.' Over threshold. Rewriting."
        Q6. Forced elevation? "Last sentence: 'Start your journey today.' Could end any marketing page. Replacing with [specific]."
        Q7. Hallucination? "Scanned. No quotes, no stats, no citations. All claims about product itself. ✓"
        Q8. Coinage? "Scanned. No coined terms. ✓"
        [redoes Q5 and Q6]
        [delivers revised version]
                                                              ← real self-check
```

The rubber-stamp version asks the questions and answers "yes/no" without
specifics. The real version answers each question with **evidence**:
hex codes, alternatives, specific sentences, actual counts.

## Instruction template

```
Before delivering output, run the 10-question self-check out loud.
Answer each with specifics, not yes/no.

Q1. Source for each major decision?
    - color: ___
    - typography: ___
    - layout: ___
    - surface: ___
    - motion: ___
    - iconography: ___
    If any has no source, redo.

Q2. First-guess detection.
    For each major decision, name 2 alternatives you considered.
    If you can't, generate them now. Pick the one with the best source.

Q3. 1000-other-AI-outputs test.
    Could this same [decision] appear in 1000 other AI outputs?
    For each major decision, answer with evidence (not just "no").

Q4. Delete-this test.
    For each sentence, section, design element:
    If deleted, does the output lose anything?
    List elements you deleted during self-check.

Q5. Signature-word density.
    Count per 500 words: __
    List the signature words found.
    If > 3, rewrite.

Q6. Forced-elevation check.
    Quote the last sentence of the piece.
    Could it end any article on any topic?
    If yes, replace with something specific.

Q7. Hallucination check.
    List every quote, statistic, citation in the piece.
    For each, confirm the source is real.
    If unsure, mark [source needed] or remove.

Q8. Coinage check.
    List every coined term in the piece.
    For each, can you describe it in plain words? If yes, delete.
    For each "Law/Model/Framework/Index," state the formula.
    If you can't, change to "observation."

Q9. Source tier verification (from 07-paradoxes/02).
    For each source cited in Q1, classify:
      - Tier 1 (user asset / URL / cited standard / user statement / measurement)?
      - Tier 2 (conventional, 30-second lookup-verifiable)?
      - Tier 3 (affective — "evokes," "feels," "matches," "conveys")?
    Tier 3 does NOT count. Remove source claim; admit as first guess.
    Did you invent any user-provided assets the user did not provide?
    (If yes, remove — that's hallucination.)
    Count: Tier 1 __, Tier 2 __, first-guess admissions __,
    Tier 3 removed __ (must be 0 before delivery).

Q10. Second-order convergence check (from 07-paradoxes/01).
    For each source, could it apply to 1000 other projects?
      - "brand is warm" → too generic
      - "hand-made ceramics in Portugal" → specific enough
    Are you reaching for new anti-AI defaults without a specific source?
      (burnt sienna, Fraunces+Plex, 7/5 grid, "I went back to bed",
       IEC SVGs, "field tech in sun" persona)
    If yes without source unique to this input, you've relocated
    to a new centroid, not escaped. Redo.

After self-check, redo any decision that failed. Deliver only the
revised version.
```
