# 02-visual / 02 · Typography

## Default reflex

- Body font: **Inter**, alone, no fallback tuning, no variant settings
- Heading: **Inter**, just `font-bold` and a larger size
- Occasionally: **Roboto** or **system-ui**
- For "techy" feel: **JetBrains Mono** as a body or accent face (overused)
- Line-height: 1.5 (Tailwind `leading-normal`)
- Letter-spacing: default
- One font, one weight axis, used everywhere

## Why the reflex exists

Inter ships as the default in Tailwind documentation, Vercel templates,
shadcn/ui examples, and every starter v0/Lovable/Bolt produces. It's the
single most-represented font in modern web training data. Inter is a
well-engineered typeface — the problem is not Inter itself, it's Inter
**without a system**: no pairing, no optical sizing, no tracking, no
weight hierarchy.

The IOV Labs paper found that **Inter alone is a tell, but Inter with a real
type system is not** — Linear ships Inter and scores 0 on the Tell Score
because they pair it with optical sizing, tracking, and a weight hierarchy.

## Bad example (the default, annotated)

```html
<style>
  body {
    font-family: 'Inter', sans-serif;        /* ← the centroid */
    font-size: 16px;
    line-height: 1.5;                        /* ← the centroid */
    color: #0f172a;
  }
  h1 {
    font-size: 48px;
    font-weight: 700;                         /* ← the centroid */
    /* no letter-spacing */
    /* no optical sizing */
  }
  h2 { font-size: 32px; font-weight: 600; }  /* ← the centroid */
  p  { font-size: 16px; font-weight: 400; }  /* ← the centroid */
</style>
```

**Why this smells:**
- One family does everything → no personality differentiation.
- No display face → headings are just "bigger Inter," not a different voice.
- No tracking adjustment → headlines look loose, body looks tight (the opposite of what they should be).
- No optical sizing → large headlines use the same glyph shapes as small body text.
- Every value is the modal value. There is no system, only defaults.

## Good example (source-driven, annotated)

```css
/*
  Source chain for this pairing:
  Product  : a long-form essay platform for working scientists
  Content  : 2000–6000 word essays, read at length on desktop
  Reference: the visual feel of academic journals (Tiempos / Sentinel)
             but warmer, less institutional (Fraunces opsz axis)

  Derivation:
  - Display face ← Fraunces. Variable opsz lets headlines use the
    "display" optical size (more contrast, more elegant) while body
    uses "text" optical size (sturdier, more legible).
  - Body face ← IBM Plex Sans. Wider than Inter, which gives long
    essays more breath. IBM Plex has humanist roots that match
    academic tone without being stuffy.
  - Mono ← IBM Plex Mono. Used ONLY for code, data, and labels —
    never as decoration.
  - Tracking: headlines -0.02em (tightened, editorial feel);
              body default (Plex Sans is already well-spaced).
  - Line-height: body 1.65 for long-form; headings 1.1 for impact.
*/

:root {
  --font-display: 'Fraunces', 'Songti SC', Georgia, serif;
  --font-body:    'IBM Plex Sans', -apple-system, 'PingFang SC', sans-serif;
  --font-mono:    'IBM Plex Mono', 'JetBrains Mono', monospace;
}

body {
  font-family: var(--font-body);
  font-size: 17px;                /* larger than default — long-form */
  line-height: 1.65;              /* looser than 1.5 — long-form */
  color: #1a1814;
}

h1, h2, h3 {
  font-family: var(--font-display);
  font-variation-settings: 'opsz' 96;  /* display optical size */
  letter-spacing: -0.02em;
  line-height: 1.1;
  font-weight: 600;
}

h1 { font-size: clamp(36px, 5vw, 56px); }
h2 { font-size: clamp(28px, 3.5vw, 36px); }

code, kbd, .label {
  font-family: var(--font-mono);
  font-size: 0.9em;
}
```

**Why this doesn't smell:**
- The display face was chosen for a **specific content type** (long-form essays for scientists).
- The body face was chosen for a **specific reading pattern** (wider letterforms for breath).
- Optical sizing is actually used (not just declared).
- Tracking is differentiated by role (tight on display, default on body).
- Line-height is differentiated by role (loose on body for reading, tight on display for impact).
- Mono is restricted to its proper domain.

Every choice has a content-driven source.

## The Inter exception

Inter is not banned. Linear uses Inter and scores 0 on Tell Score. The
difference is that Linear pairs Inter with:

- A separate display treatment (size + weight + tracking)
- An optical-sizing strategy
- A real weight hierarchy (not just 400/600/700)
- A character set that includes all needed glyphs
- Tightening on large sizes, loosening on small sizes

**If you must use Inter, you must build the system around it.** Inter alone
with `font-bold` headings is the tell. Inter with a defensible type system
is a choice.

## Heuristic questions

1. **How many type families are you using?** One is the default. Two is the
   minimum for non-default work. Three is fine if each has a job.
2. **What is the display face doing that the body face can't?** If you can't
   answer, you don't need a display face. If you can, the answer is your
   source.
3. **Where did each family come from?** "It's clean" is not a source.
   "It has humanist roots matching the academic tone" is a source.
4. **Is optical sizing actually used?** If you loaded a variable font and
   didn't set `font-variation-settings: 'opsz' ...`, you wasted the choice.
5. **Is tracking differentiated by role?** Headlines should be tighter than
   body. If both are default, you've made no choice.
6. **Is line-height differentiated by role?** Body should be looser than
   headings. If both are 1.5, you've made no choice.
7. **Is mono restricted to code/data/labels?** If mono appears in body or
   headings as decoration, that's the JetBrains-Mono-as-vibes tell.

## Anti-pattern: font as costume

Swapping Inter for Fraunces without changing anything else does not de-AI
the page. The page now smells like AI in a Fraunces costume.

```
Bad:    "Use Fraunces instead of Inter."                  ← costume change
Good:   "This is a long-form essay platform; I need a
        display face with optical sizing for headlines and
        a humanist body face for reading. Fraunces + Plex
        Sans does that; Inter alone doesn't."              ← system change
```

## Instruction template

```
Choose a typography system. Before producing, answer:

1. Content type:
   [ short marketing copy | long-form essay | data dashboard |
     code documentation | editorial news | children's content ]
   This determines x-height needs, weight range, line-length tolerance.

2. Reading context:
   [ mobile glancing | desktop reading at length | outdoor |
     dark room | mixed ]
   This determines size, line-height, contrast.

3. Display face — name it, and name what it does that the body can't:
   Example: "Fraunces — gives headlines editorial character via
            optical sizing; Inter would just look bigger, not different."

4. Body face — name it, and name why not Inter:
   Example: "IBM Plex Sans — wider letterforms give long essays breath;
            Inter is too compressed for 2000-word reading."

5. Mono face (if any) — name its restricted domain:
   Example: "IBM Plex Mono — only for code blocks and data labels."

6. State the tracking and line-height for each role:
   h1: tracking ___, line-height ___
   body: tracking ___, line-height ___
   Justify each non-default value.

Then produce the CSS. Annotate each choice with its source in a comment.
```
