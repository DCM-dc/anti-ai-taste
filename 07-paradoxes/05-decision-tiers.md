# 07-paradoxes / 05 · Decision tiers

## The failure mode

The guide says "every choice must have a source." Taken literally, this
means the agent must source the palette, the font, the layout, the
radius, the shadow, the easing, the icon stroke weight, the line-height,
the letter-spacing, the border color, the padding, the gap, the focus
ring width...

The result is **decision paralysis**: the agent either stalls, or
hallucinates sources for trivia to satisfy the rule. The framework
becomes unusable for real work.

The cure is not "drop the source rule." It's **tier the decisions**.
Not every decision is equally load-bearing. Some must be sourced; some
can inherit from a sourced decision; some can be honest defaults.

---

## The three tiers

### Tier 1: Load-bearing (must be sourced)

Decisions that define the project's identity. If changed, the output
looks like a different project.

| Decision | Why load-bearing |
|---|---|
| Primary palette (1–3 colors) | Defines visual identity |
| Type system (display + body pairing) | Defines voice |
| Page grammar (which sections, in what order) | Defines structure |
| Information hierarchy (what's primary, secondary, tertiary) | Defines meaning |
| Voice / register of copy | Defines personality |
| Interaction model (data-first vs narrative vs marketing) | Defines user relationship |

**Rule:** Every Tier 1 decision must have a Tier 1 or Tier 2 source
(see `02-source-verification.md`). No exceptions. If unsourced, admit
as default and flag for user input.

### Tier 2: Derived (inherits from Tier 1, must be consistent)

Decisions that follow from Tier 1 choices. They don't need their own
source — they need to be **consistent** with the Tier 1 source.

| Decision | Derives from |
|---|---|
| Secondary palette (accents, borders, dividers) | Primary palette |
| Heading sizes, weights, tracking | Type system |
| Card radius, button radius, input radius | Surface hierarchy (itself Tier 1) |
| Border color, shadow recipe | Palette + surface hierarchy |
| Section spacing, grid gap | Layout grammar |
| Sentence length variance | Voice / register |
| Hover/press motion | Interaction model |

**Rule:** Tier 2 decisions don't need an independent source. They must
be **consistent with the Tier 1 decision they derive from**. The
self-check question is "does this follow from [Tier 1 source]?" not
"what is the source for this?"

### Tier 3: Trivia (defaults are fine, just be honest)

Decisions so fine-grained that sourcing each one is paralysis.

| Decision | Why trivial |
|---|---|
| Exact padding value (24px vs 26px) | Doesn't change identity |
| Exact focus ring width (2px vs 3px) | Doesn't change identity |
| Exact transition duration (150ms vs 180ms) | Within perceptual threshold |
| Exact letter-spacing on body (-0.01em vs 0) | Within perceptual threshold |
| Exact border opacity (15% vs 18%) | Within perceptual threshold |

**Rule:** Tier 3 decisions can use defaults. No source required. But
**don't dress them as sourced** — if asked, say "default, within
perceptual threshold."

---

## The decision count budget

For a typical project (landing page, article, dashboard), expect:

- **5–8 Tier 1 decisions** (palette, type system, layout grammar,
  hierarchy, voice, interaction model)
- **15–25 Tier 2 decisions** (derived from Tier 1)
- **50+ Tier 3 decisions** (trivia, defaults fine)

**Source only the Tier 1 decisions.** This brings the source-count from
"everything" (~80) down to "load-bearing" (~7). The framework becomes
usable.

The self-check (Q9, Q10) runs on Tier 1 only. Running it on Tier 3
is waste — the answers will all be "default, within threshold," which
is correct and uninteresting.

---

## Source conflict resolution

When two Tier 1 sources conflict, the agent must resolve explicitly.
Common conflicts:

### Brand color vs reading context

```
Brand:    logo is #2d5a3d (deep green)
Context:  user reads in direct sunlight on phone

Conflict: brand green at full saturation has poor contrast in sun
Resolution: darken the brand hue 8–12% for AA contrast on warm cream
            surface. Document the adjustment.
Source:   brand (hue) + WCAG 2.2 AA (lightness adjustment)
```

### Brand color vs domain convention

```
Brand:    logo is purple
Domain:   fintech for kids

Conflict: purple is fine for kids, but "banking purple" reads as
          enterprise (Stripe, Wise). Kids' fintech usually uses
          candy colors.
Resolution: ask the user. If brand is non-negotiable, use purple
            as accent only; use candy palette as primary. If brand
            is flexible, propose candy palette and explain.
Source:   user decision (escalate)
```

### Locale vs brand

```
Brand:    logo is cool blue
Locale:   coastal Japan (warm haze palette)

Conflict: cool blue fights the warm-haze locale
Resolution: locale wins for surfaces (warm cream bg), brand wins
            for accent (cool blue used sparingly on key CTAs).
Source:   locale (surfaces) + brand (accent)
```

### Reference vs content semantics

```
Reference: user likes linear.app (dark, sharp, dense)
Content:   long-form essays for scientists (needs breath, warmth)

Conflict: linear's density fights long-form reading
Resolution: take linear's structure (asymmetric grid, no marketing
            fluff) but invert its surface (light warm paper, not dark).
Source:   reference (structure) + content (surface)
```

---

## The conflict resolution protocol

When two Tier 1 sources conflict:

1. **Name the conflict explicitly.** "Brand color and reading context
   conflict on contrast."
2. **Identify which source wins for which property.** Usually one wins
   for hue, the other for lightness, or one wins for structure, the
   other for surface.
3. **Document the resolution.** "Hue from brand, lightness adjusted for
   WCAG AA on warm surface."
4. **If unresolvable, escalate to user.** Don't silently pick one.
   Present the conflict and ask.

---

## How this fails if applied naively

If the agent treats every decision as Tier 1, it will:
- Stall on trivia ("what's the source for 24px padding?")
- Hallucinate sources for Tier 3 decisions to satisfy the rule
- Produce output that's over-justified and under-delivered

If the agent treats every decision as Tier 3, it will:
- Default everything
- Produce the centroid

The balance: **Tier 1 is sourced, Tier 2 is derived, Tier 3 is honest
default.** This is the operational shape of the framework.

---

## Heuristic questions

1. **For each decision you're sourcing, which tier is it?**
   - Tier 1: source it.
   - Tier 2: derive from Tier 1, check consistency.
   - Tier 3: default is fine, don't dress as sourced.
2. **How many Tier 1 decisions did you actually source?**
   - If 0: you're defaulting everything.
   - If 5–8: healthy.
   - If 20+: you're over-sourcing; reclassify most as Tier 2 or 3.
3. **Are any Tier 2 decisions inconsistent with their Tier 1 source?**
   - E.g., palette is warm but border is slate (cold). Inconsistent.
4. **Did any Tier 1 sources conflict?**
   - If yes, did you resolve explicitly, or silently pick one?
5. **Are you dressing Tier 3 defaults as Tier 1 sources?**
   - "The 24px padding evokes industrial breathing room" — Tier 3
     hallucination. Admit as default.

---

## Instruction template

```
Classify every decision before sourcing:

TIER 1 (load-bearing, must be sourced):
  - primary palette (1–3 colors)
  - type system (display + body pairing)
  - page grammar (sections + order)
  - information hierarchy
  - voice / register
  - interaction model
  Count: __ (target 5–8)

TIER 2 (derived, must be consistent with Tier 1):
  - secondary palette, heading sizes, radius values, border color,
    spacing, motion easing, sentence length variance
  For each: "derives from [Tier 1 decision], consistent? yes/no"
  Count: __

TIER 3 (trivia, defaults fine):
  - exact padding, focus ring width, transition duration,
    letter-spacing micro-values, border opacity
  Mark: "default, within perceptual threshold"
  Count: __

CONFLICT CHECK:
  Did any Tier 1 sources conflict? (brand vs locale, brand vs domain,
  locale vs content, reference vs content)
  If yes: resolve explicitly (which source wins for which property),
  or escalate to user.

Self-check (Q9, Q10) runs on TIER 1 ONLY.
```
