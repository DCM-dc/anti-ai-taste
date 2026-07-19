# 02-visual / 01 · Color

## Default reflex

The model reaches for:

- Primary: `#3b82f6` (Tailwind `blue-500`) or `#6366f1` (`indigo-500`) or `#8b5cf6` (`purple-500`)
- Gradient: indigo → violet → fuchsia, diagonal 135°
- Background: `#ffffff` or `#f8fafc` (`slate-50`)
- Text: `slate-900` on `slate-50`, `slate-600` for secondary
- Accent: emerald for success, rose for error, amber for warning

## Why the reflex exists

Tailwind CSS is the dominant styling framework in the model's training corpus.
Tailwind's documentation, examples, and component libraries defaulted to
`bg-indigo-500` for years (Tailwind's author has publicly apologized for this).
The model learned "modern web = indigo/purple" as a correlation, and reproduces
the correlation as if it were a preference.

The feedback loop is self-reinforcing: developers use Tailwind → Tailwind
defaults enter training data → AI generates Tailwind defaults → developers
ship → re-enters training data.

## Bad example (the default, annotated)

```css
:root {
  --primary: #6366f1;        /* ← Tailwind indigo-500. The centroid. */
  --primary-hover: #4f46e5;  /* ← indigo-600. The centroid one step darker. */
  --bg: #ffffff;             /* ← pure white, the highest-frequency bg in training */
  --text: #0f172a;           /* ← slate-900 */
  --text-soft: #64748b;      /* ← slate-500 */
}

.hero {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 50%, #d946ef 100%);
  /* ↑ indigo → violet → fuchsia. The single most recognizable AI tell. */
}
```

**Why this smells:**
Every value here is the modal value in the training distribution. There is
no source. If asked "why indigo?", the only honest answer is "because that's
what most tutorials use." That is the definition of a default.

## Good example (source-driven, annotated)

```css
/*
  Source chain for this palette:
  Product  : battery-monitoring tool for solar installers
  Locale   : field use, often in direct sunlight on phone screens
  Brand    : logo uses #2d5a3d (deep cycle battery green)
  User     : reads data outdoors, needs high contrast

  Derivation:
  - Primary ← brand green (#2d5a3d), darkened 8% for AA contrast on cream
  - Surface ← warm off-white (#f4ede0), reduces glare vs pure white in sun
  - Text    ← near-black with warm undertone (#1a1814), not pure slate
  - Accent  ← caution amber (#d97706), the color field techs already
              associate with battery warnings on hardware
  - No gradient. Field tools don't have gradients. Field tools have
    high-contrast blocks.
*/

:root {
  --primary:        #245944;  /* brand green, contrast-adjusted */
  --primary-hover:  #1c4636;
  --surface:        #f4ede0;  /* warm cream, glare-reducing */
  --surface-deep:   #e6dbc2;
  --ink:            #1a1814;  /* warm near-black */
  --ink-soft:       #4a443a;
  --caution:        #d97706;  /* hardware battery-warning amber */
}
```

**Why this doesn't smell:**
- The hue comes from the brand logo (a real source).
- The lightness comes from the user context (a real constraint).
- The accent comes from hardware semantics (a real convention).
- The warmth comes from the locale (sun-readable surfaces skew warm).
- The decision to use **no gradient** comes from the product type (field tools
  are not marketing surfaces).

Nothing here is the centroid. Every value is conditional.

## Heuristic questions

Before committing a palette, answer all of these out loud:

1. **Where does the hue come from?** If the answer is "it looks modern," redo.
   Acceptable answers: brand logo, locale, content semantics, user emotion.
2. **Where does the lightness come from?** Should match the reading context
   (bright sun → high contrast; dark room → low contrast; long reading →
   off-white, not pure white).
3. **Where does the temperature come from?** Warm vs cold should be a choice,
   not a default. Pure neutral gray is also a choice — defend it.
4. **Why this accent color?** Acceptable: it's the convention in this domain
   (amber for warnings, green for confirm). Unacceptable: "it pops."
5. **Does this need a gradient at all?** Gradients are decorative. Most
   information doesn't need them. If you can't articulate what the gradient
   communicates, it's decoration — delete it.
6. **Could this palette appear in 1000 other AI outputs?** If yes, it's the
   centroid. Source harder.

## Anti-pattern: the new default

Banning indigo and reaching for burnt sienna is **not** escaping the default.
It's relocating it. If the only reason for burnt sienna is "indigo is banned,"
the choice is still not source-driven.

```
Bad:    "Don't use indigo. Use burnt sienna instead."   ← still default logic
Good:   "The product is hand-made ceramics. The palette comes from
        unglazed clay, which is #c2592e."                ← source-driven
```

The test: could you write the same sentence for any other product? If yes,
your reasoning is generic, not source-driven.

## Instruction template

```
Choose a color palette. Before producing, answer in plain text:

1. Source for the hue:
   [ brand asset | locale | content semantics | user emotion | reference ]
   Name it specifically: "brand logo #XXXXXX" or "coastal Japan haze"
   — not "modern," not "professional."

2. Source for the lightness:
   [ reading context | user context | brand ]
   Name the reading context: "outdoor phone use" or "long-form reading"

3. Source for the accent:
   [ domain convention | brand secondary | contrast requirement ]
   Name the convention: "warning amber" or "confirm green"

4. Gradient: yes / no. If yes, what does it communicate?
   If you can't answer in one sentence, the answer is no.

Then produce the palette. Annotate each value with its source in a comment.
```
