# 07-paradoxes / 02 · Source verification

## The failure mode

The guide's core rule is "every choice must have a source." But LLMs are
probability engines, not reasoning engines. When asked to "name the
source," the model will happily generate a plausible-sounding
justification that has no basis in reality:

> "I chose Fraunces because it evokes 19th-century industrial typography
> that matches the brand's heritage."

The brand has no such heritage. The model invented it because
"19th-century industrial typography" is a probable continuation of
"Fraunces because it evokes..." in the training distribution.

This is the guide's deepest trap. Without verification, the "source-driven"
framework becomes a **hallucination engine** — every default dressed up
as a sourced choice.

---

## Why LLMs hallucinate sources

LLMs predict the next token. When the prompt requires "name a source for
this choice," the most probable continuation is a plausible-sounding
justification, not a truthful one. The model has no internal mechanism
to distinguish:

- "I recall this from training data" (real)
- "This is a probable-sounding phrase" (fabricated)
- "I'm pattern-matching on the structure of design justifications" (fabricated)

RLHF makes this worse: raters rewarded "well-reasoned" output, which
taught the model to produce justifications whether or not they're true.
The model learned: source-like text = high-quality text.

---

## The three-tier source classification

Not all sources are equal. Classify every source claim into one of three
tiers. Only Tier 1 and Tier 2 count as real sources.

### Tier 1: Verifiable external (cannot be hallucinated)

The source is an external artifact the agent can point to:

| Source type | Example |
|---|---|
| User-provided asset | "Brand logo file: `logo.svg`, hex `#2d5a3d`" |
| URL the agent can cite | "linear.app (referenced by user)" |
| Cited paper / standard | "IEC 60617 battery symbol standard" |
| User's explicit statement | "User said: 'field techs read in sun'" |
| Real measurement | "PR review time dropped from 2.1 to 0.7 days (our internal data)" |

**Test:** can the agent point to where this came from? If yes, Tier 1.

### Tier 2: Conventional (verifiable by lookup, not hallucinated)

The source is an established convention the agent can reference:

| Source type | Example |
|---|---|
| Domain convention | "Amber is the hardware convention for battery warnings" |
| Established standard | "WCAG 2.2 AA requires 4.5:1 contrast" |
| Widely-known fact | "Inter ships as Tailwind's default" |
| Type design history | "IBM Plex was IBM's in-house face, designed by Mike Abbink" |

**Test:** could a human verify this by a 30-second web search? If yes,
Tier 2. If the "fact" turns out to be wrong on lookup, it was a
hallucination mislabeled as Tier 2.

### Tier 3: Asserted (hallucination risk — does NOT count as a source)

The source is a subjective claim about aesthetic or emotional resonance:

| Source type | Example |
|---|---|
| Affective claim | "Fraunces evokes 19th-century industrial typography" |
| Personality claim | "This font feels hand-made" |
| Vague historical | "Matches the brand's heritage" (when no heritage was provided) |
| Emotional mapping | "Burnt sienna conveys warmth and authenticity" |

**Test:** is this a claim about how something "feels" or "evokes"?
If yes, Tier 3. **Tier 3 sources do not satisfy the "name a source" rule.**
They are vibes in a source costume.

---

## The "cite or admit" protocol

For every source claim, the agent must do one of two things:

### Option A: Cite

State the source as Tier 1 or Tier 2:

```
✓ "Palette: #2d5a3d ← user-provided logo.svg, darkened 8% for AA."
   [Tier 1: user-provided asset]

✓ "Amber accent: IEC 60617 convention for battery warnings."
   [Tier 2: established standard]

✓ "IBM Plex Sans: designed by Mike Abbink for IBM, 2017."
   [Tier 2: verifiable by lookup]
```

### Option B: Admit

If the source is Tier 3 (or would be Tier 2 but you're not sure it's
real), explicitly mark it as a first guess:

```
✓ "Palette: warm cream. Source: first guess (no user brand asset
   provided). Marked as default."

✗ "Palette: warm cream. Source: evokes Mediterranean warmth matching
   the brand." [Tier 3 hallucination — forbidden]
```

The honesty is the point. A first guess marked as a first guess is
better than a hallucinated source dressed as a real one.

---

## The verification step (added to self-check)

Before delivering, the agent must verify every source claim:

```
For each source cited in the output:
  1. Is it Tier 1 (user-provided asset / URL / cited standard)?
     → If yes, cite the asset/URL/standard. ✓
  2. Is it Tier 2 (conventional, verifiable by lookup)?
     → If yes, state what a 30-second search would confirm. ✓
  3. Is it Tier 3 (affective claim, "evokes," "feels," "matches")?
     → If yes, REMOVE the source claim.
     → Replace with: "first guess (no source provided)" or
        "default value, marked for user review."
```

This step is non-negotiable. Without it, the guide produces
hallucinated-justification output that's worse than honest defaults.

---

## How this fails if applied naively

If the agent treats "verify sources" as another rule to satisfy, it will
**fabricate Tier 1 and Tier 2 citations**: "user provided logo.svg with
hex #2d5a3d" — when no such file was provided.

The defense against this: **the agent cannot invent user-provided
assets.** If the user didn't provide a logo file, the agent cannot
claim one. If the user didn't state a reading context, the agent cannot
claim "user said field techs read in sun."

When in doubt, the agent must **ask the user** rather than fabricate.
This connects to `03-thin-input-protocol.md`.

---

## Worked example

### Bad (hallucinated sources)

```css
/*
  Palette: #c2592e (burnt sienna)
  Source: evokes the warmth of hand-made ceramics and the
  founder's Portuguese heritage. ← Tier 3 hallucination;
  no founder or heritage was provided.
*/
```

### Good (verified or admitted)

```css
/*
  Palette: #c2592e (burnt sienna)
  Source: first guess. No brand asset was provided by the user.
  Marked as default for user review.

  Typography: Inter
  Source: first guess. No content-personality information provided.

  Layout: 7/5 asymmetric grid
  Source: structural default from anti-ai-taste guide. Not user-sourced.

  NOTE: This output uses 3 unsourced defaults. It will read as
  "anti-AI style" rather than as "this specific project."
  Provide brand assets and content context to escape defaults.
*/
```

The second version is **honest**. It tells the user exactly which
choices are sourced and which are defaults. The user can then decide
whether to provide sources or accept the defaults.

---

## Heuristic questions

1. **For each source you cited, which tier is it?**
   - Tier 1 (user asset / URL / cited standard): ✓
   - Tier 2 (conventional, lookup-verifiable): ✓
   - Tier 3 (affective, "evokes," "feels"): ✗ — remove or admit as first guess
2. **Did you invent any user-provided assets?**
   If you claimed "user-provided logo.svg" without the user providing it, that's a hallucination. Remove.
3. **For each Tier 2 claim, what would a 30-second search confirm?**
   If you can't state what the search would show, downgrade to first guess.
4. **Are you using "evokes," "feels," "matches," "conveys" anywhere?**
   These are Tier 3 markers. Remove the source claim; admit as first guess.

---

## Instruction template

```
After producing output, run source verification:

For each source cited:
  Tier 1 (user asset / URL / cited standard)?
    → cite the asset/URL/standard. ✓
  Tier 2 (conventional, lookup-verifiable)?
    → state what a 30-second search would confirm. ✓
  Tier 3 (affective, "evokes," "feels," "matches")?
    → REMOVE the source claim.
    → Replace with: "first guess (no source provided)" or
       "default value, marked for user review."

Forbidden:
  - Inventing user-provided assets the user did not provide.
  - Citing papers/standards you cannot name specifically.
  - Using "evokes" / "feels" / "matches" as if they were sources.

After verification, count:
  - Tier 1 sources: ___
  - Tier 2 sources: ___
  - First-guess admissions: ___
  - Tier 3 hallucinations removed: ___

If Tier 3 count > 0 before removal, you were hallucinating.
Run again until 0.
```
