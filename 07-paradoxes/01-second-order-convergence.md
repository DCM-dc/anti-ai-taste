# 07-paradoxes / 01 · Second-order convergence

## The failure mode

If every agent reads this guide and bans the same defaults, output
converges on a **new median**. The burnt-sienna-and-Fraunces look
becomes the new indigo-and-Inter. The "I went back to bed" ending
becomes the new "in conclusion." The smell returns, dressed differently.

This is the IOV Labs paper's closing warning, cited but not solved in
section 01. This file solves it.

---

## Why banning defaults produces new defaults

A ban list removes one mode from the distribution. The next-most-probable
mode immediately fills the gap. The agent is still inside the distribution.

```
ban: indigo        → agent picks violet
ban: violet        → agent picks burnt sienna (the new "anti-AI" default)
ban: burnt sienna  → agent picks forest green
ban: forest green  → agent picks ochre
...
```

The guide's "source-driven" framing was supposed to escape this. But if
the agent fabricates sources (see `02-source-verification.md`), or if
every user provides the same kind of source ("warm and quiet"), the
output still converges. The guide becomes a recipe for a different
centroid.

---

## The new centroid this guide creates

If you follow sections 01–06 literally, you will produce output with
these features:

- Palette: burnt sienna / forest green / ochre on warm cream
- Typography: Fraunces + IBM Plex Sans (or Sora + Inter)
- Layout: asymmetric 7/5 grid, no centered hero
- Surface: 2/4/8/12px radius hierarchy
- Motion: ease-out, scale 1.02, no bounce
- Copy: specific numbers, first-person, fragments, "I went back to bed" endings
- Rhetoric: no quotes, no summaries, no coined terms

This is already a recognizable style. After 1000 agents have followed
this guide, it will be **the new indigo gradient**. Readers will
recognize "ah, this was made with that anti-AI guide" the way they
currently recognize "ah, this was made by v0."

---

## The only real cure: output conditional on a unique source

The escape from second-order convergence is NOT "don't have a style"
(impossible — every output has a style). It is:

> **Make every output conditional on a source that is unique to this specific input.**

If every output is conditional on a different brand, different locale,
different user, different content — the outputs cannot converge.
Convergence requires shared inputs. Unique inputs produce unique outputs.

This means:

| Source type | Converges? |
|---|---|
| "I chose burnt sienna because warm palettes are nice" | Yes — every agent reaches the same conclusion |
| "I chose #c2592e because the user's brand is hand-made ceramics, and unglazed clay is #c2592e" | No — only this user has this brand |
| "I chose Fraunces because it's editorial" | Yes — every agent reaches for Fraunces |
| "I chose Fraunces because the founder's previous publication used Tiempos, and Fraunces is the closest free variable alternative with the same opsz axis" | No — only this founder has this history |
| "I ended with 'I went back to bed' because that's a fragment and fragments are anti-AI" | Yes — every agent ends with fragments |
| "I ended with 'the fix shipped at 4:12am' because that's when the fix actually shipped" | No — only this incident has this timestamp |

The pattern: **generic reasoning converges; specific reasoning diverges.**

---

## The "specificity floor" test

For every source the agent names, apply this test:

> **Could this same source apply to 1000 other projects?**

- "The brand is warm" → yes, applies to 1000 projects → not specific enough
- "The brand is hand-made ceramics in Portugal" → no, applies to maybe 5 projects → specific enough
- "Inter is clean" → yes, applies to 1000 projects → not specific enough
- "The founder's previous publication used Tiempos" → no, applies to 1 project → specific enough

If the source passes the specificity floor, the output is conditional
and won't converge. If it fails, the output will converge regardless
of whether the source is "real."

---

## How this fails if applied naively

If the agent treats "make sources specific" as a new rule to satisfy,
it will **fabricate specific sources**: "I chose this because the
founder's previous publication used Tiempos" — even if no such founder
or publication exists.

This is the second-order convergence's evil twin. The agent escapes the
default style by inventing a fake specificity. The output looks
non-convergent but is actually hallucinated.

The cure for this is in `02-source-verification.md`: every source must
be either user-provided, URL-cited, or explicitly marked as a first guess.

---

## Heuristic questions

1. **List every source you cited.** For each, could it apply to 1000 other projects?
   If yes, the source is too generic. Source harder, or admit it's a first guess.
2. **Are you reaching for the "anti-AI defaults"?**
   - Burnt sienna, forest green, ochre on cream
   - Fraunces + IBM Plex Sans
   - Asymmetric 7/5 grid
   - Fragments and "I went back to bed" endings
   If yes, you've relocated, not escaped. Find a source unique to this input.
3. **Could this output appear in 1000 other outputs guided by this same repo?**
   If yes, your sources weren't specific enough.
4. **Are your sources real or fabricated?**
   Run `02-source-verification.md` on every source claim.

---

## Instruction template

```
After producing output, run the second-order convergence check:

1. List every source you cited (palette, font, layout, ending, etc.).
   For each: could this same source apply to 1000 other projects?
   - "warm palette" → too generic, source harder or admit first guess
   - "founder's previous pub used Tiempos" → specific, OK
   - "field techs read in sun" → specific to this user, OK

2. Are you using any of these "new anti-AI defaults"?
   - burnt sienna / forest green / ochre on cream
   - Fraunces + IBM Plex Sans
   - asymmetric 7/5 grid with no hero
   - fragments and "I went back to bed" endings
   If yes without a specific source, you've relocated, not escaped.

3. Could this output appear in 1000 other outputs made with this guide?
   If yes, redo with more specific sources.

4. Run source verification (02-source-verification.md) on every source.
   Hallucinated sources don't count.
```
