# 02-visual / 05 · Motion

## Default reflex

- Universal transition: `transition-all duration-300 ease-in-out`
- Hover scale: `hover:scale-105`
- Every animated element: Framer Motion `whileHover={{ scale: 1.05 }}`
- Page transitions: `AnimatePresence` with fade
- Card hover: lift + scale + shadow growth, all at once
- Loading: spinner, skeleton, or `motion.div` with `initial={{ opacity: 0 }}`
- Bounce easing on everything "playful": `cubic-bezier(0.68, -0.55, 0.265, 1.55)`

One easing, one duration, applied to everything.

## Why the reflex exists

`transition-all duration-300 ease-in-out` is the most-used transition
snippet in Tailwind's docs and component examples. `whileHover={{ scale: 1.05 }}`
is the most-used Framer Motion snippet. The model learned these as
lexical units and reproduces them on every interactive element.

The problem is not that they're bad values. It's that **one easing for
everything flattens interaction semantics**. A button press, a modal open,
a card hover, and a page transition all "feel the same" — and that
sameness is the smell.

## Bad example (the default, annotated)

```css
* {
  transition: all 0.3s ease-in-out;
  /* ↑ everything transitions every property. The universal default. */
}

.card:hover {
  transform: scale(1.05);
  box-shadow: 0 20px 25px rgba(0,0,0,0.1);
  /* ↑ hover = scale up + bigger shadow. The centroid hover. */
}

.button:hover {
  transform: scale(1.05);
  /* ↑ same scale as card. No semantic difference. */
}

.modal {
  animation: fadeIn 0.3s ease-in-out;
  /* ↑ same duration and easing as everything else. */
}

@keyframes fadeIn {
  from { opacity: 0; transform: scale(0.95); }
  to   { opacity: 1; transform: scale(1); }
}
```

```jsx
// Framer Motion version of the same defaults
<motion.div
  whileHover={{ scale: 1.05 }}        // ← the centroid
  whileTap={{ scale: 0.95 }}           // ← the centroid
  transition={{ duration: 0.3 }}       // ← the centroid
/>
```

**Why this smells:**
- `transition: all` transitions every property, including ones you don't want animated (color, layout).
- One duration for everything — a button press and a page transition take the same time.
- One easing for everything — `ease-in-out` is the model's default curve; it has no personality.
- `scale(1.05)` on every hover — buttons and cards lift the same way.
- The page has no motion vocabulary. Everything moves the same.

## Good example (source-driven, annotated)

```css
/*
  Source chain for this motion system:
  Product  : a battery-monitoring tool for solar installers
  User     : field tech, glances at phone, needs immediate feedback
  Visual ref: industrial control panels — small precise movements,
              no playful bouncing. The tool should feel like hardware,
              not like a marketing site.

  Motion vocabulary — one easing per interaction class:

  1. Press feedback (buttons, toggles)
     100ms, ease-out
     Why: press feedback must feel instant. 100ms is at the edge of
     perception. ease-out snaps to the new state.
     Property: transform scale only (no color, no shadow).

  2. Hover feedback (cards, list items)
     150ms, ease-out
     Why: hover is exploration, slightly slower than press.
     Property: translateY only (no scale, no shadow growth).
     -2px lift is enough; the user already knows it's interactive.

  3. Open/close (modals, popovers, dropdowns)
     180ms, cubic-bezier(0.2, 0, 0, 1)
     Why: opening needs presence (180ms so the user registers it).
     The cubic-bezier is "decelerating" — starts fast, ends slow.
     Property: opacity + scale(0.98) only.

  4. Page transitions
     220ms, cubic-bezier(0.2, 0, 0, 1)
     Why: page transitions are the slowest motion in the system.
     They convey "we are going somewhere," not "we are appearing."

  5. Data updates (live numbers, status changes)
     80ms, linear, NO transition on the number itself
     Why: data should appear instantly. Animating the number would
     imply "we are computing this." It's already computed.

  Forbidden:
  - transition: all (transition only the property you mean)
  - scale(1.05) on hover (too much; reads as marketing)
  - bounce/elastic easing (this is a field tool, not a toy)
  - whileTap scale 0.95 (too much; reads as squishy)
*/

:root {
  --ease-out: cubic-bezier(0, 0, 0.2, 1);
  --ease-decel: cubic-bezier(0.2, 0, 0, 1);
}

.button  { transition: transform 100ms var(--ease-out); }
.button:hover  { transform: scale(1.02); }      /* 2%, not 5% */

.card    { transition: transform 150ms var(--ease-out),
                       border-color 150ms var(--ease-out); }
.card:hover    { transform: translateY(-2px); border-color: var(--moss); }

.modal   { transition: opacity 180ms var(--ease-decel),
                       transform 180ms var(--ease-decel); }
.modal.opening { opacity: 0; transform: scale(0.98); }
.modal.open    { opacity: 1; transform: scale(1); }

.page    { transition: opacity 220ms var(--ease-decel); }

/* Data updates: no transition. The number is the number. */
.data-readout { transition: none; }
```

**Why this doesn't smell:**
- Five distinct motion treatments, each tied to an interaction class with a reason.
- Each motion uses the **minimum property set** — no `transition: all`.
- Easings differentiate intent (press = fast out; open = decelerating; data = none).
- The motion vocabulary matches the product personality (industrial, not playful).
- No bounce, no elastic, no `scale(1.05)`. The product is a tool, not a toy.

## The interaction-class rule

Pick 4–6 interaction classes. Assign each a duration, an easing, and a
property list. Typical classes:

| Class | Duration | Easing | Property |
|---|---|---|---|
| Press | 80–120ms | ease-out | transform only |
| Hover | 120–180ms | ease-out | transform / border / color |
| Open/close | 180–240ms | decelerating | opacity + transform |
| Page transition | 200–300ms | decelerating | opacity |
| Data update | 0ms (none) | — | — |
| Loading | loop, 1.2–2s | linear or ease-in-out | opacity / transform |

State the vocabulary in a comment. Apply consistently.

## The "transition: all" rule

`transition: all` is almost always wrong. It transitions properties you
didn't mean to animate (color, layout, padding), causing jank and
unintended effects.

**Animate only the property you mean.**

```css
/* Bad */
.card { transition: all 0.3s ease-in-out; }

/* Good */
.card {
  transition: transform 150ms var(--ease-out),
              border-color 150ms var(--ease-out);
}
```

## The "scale 1.05" rule

`hover:scale-105` is the most-recognizable hover tell. 5% is too much —
it reads as marketing.

| Scale | Reads as |
|---|---|
| 1.00 | static |
| 1.01 | subtle (data-dense UI) |
| 1.02 | button press |
| 1.03 | card hover (marketing) |
| 1.05 | "look at me!" — the AI tell |
| 1.10 | parody |

For tools, 1.01–1.02. For marketing, 1.02–1.03. Above that, you're
performing, not interacting.

## The bounce rule

Bounce / elastic easing (`cubic-bezier(0.68, -0.55, 0.265, 1.55)` and
similar) should be used **never** unless the product is genuinely playful
(toys, games, children's apps). For everything else, bounce reads as
"trying too hard."

## Heuristic questions

1. **How many distinct motion treatments does the page use?**
   - 1 → no vocabulary. Add differentiation.
   - 4–6 → good.
   - 7+ → too many. Consolidate.
2. **Is each treatment tied to an interaction class?**
   If not, you're decorating, not systematizing.
3. **Are you using `transition: all` anywhere?**
   If yes, replace with explicit property lists.
4. **What's the hover scale?**
   If 1.05, you're in AI-tell territory. Reduce to 1.01–1.03.
5. **Is bounce/elastic easing used? Why?**
   "Because it's playful" is not enough. The product must actually be playful.
6. **Do data updates animate?**
   They probably shouldn't. Animating data implies "we're computing this."
7. **Does the motion vocabulary match the product personality?**
   Tools → small, fast, precise. Marketing → larger, slower, more dramatic.
   Children's → bouncy. Match the personality.

## Anti-pattern: ease-in-out as costume

Replacing `ease-in-out` with `cubic-bezier(0.4, 0, 0.2, 1)` everywhere
is not a vocabulary. It's one easing in a different costume.

```
Bad:    "Don't use ease-in-out, use cubic-bezier(0.4, 0, 0.2, 1)."  ← same flatness
Good:   "Press = 100ms ease-out (snap). Open = 180ms decelerating
        (presence). Page = 220ms decelerating (going somewhere).
        Data = no transition (it's a fact). Each tied to a class."  ← real vocabulary
```

## Instruction template

```
Design the motion system. Before producing, answer:

1. Product personality:
   [ tool | marketing | editorial | playful | data-dense ]
   This determines the overall motion register.

2. Motion vocabulary (list 4–6 interaction classes):
   - press:      __ms, easing ___, properties ___
   - hover:      __ms, easing ___, properties ___
   - open/close: __ms, easing ___, properties ___
   - page:       __ms, easing ___, properties ___
   - data:       __ms (often 0), easing ___, properties ___
   - loading:    __ms, easing ___, properties ___

3. Hover scale: __ (justify — should match personality)

4. Bounce/elastic:
   yes / no. If yes, what makes this product playful?

5. transition: all:
   Where is it used? (Should be nowhere.)

Then produce the CSS. Define easings as CSS variables. Annotate each
class with its source. Apply consistently.
```
