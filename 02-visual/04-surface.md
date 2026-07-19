# 02-visual / 04 · Surface (radius, shadow, border)

## Default reflex

- Border radius: `rounded-2xl` (16px) on **everything** — buttons, cards, inputs, containers, avatars
- Shadow: `shadow-md` on cards, `shadow-sm` on inputs, `shadow-lg` on hover
- Border: `border border-slate-200` on every surface
- Backdrop: `backdrop-blur-xl bg-white/70` for any floating element
- Padding: `p-6` (24px) on every card

The whole page uses one radius, one shadow, one border, one padding.
Mechanically correct, emotionally flat.

## Why the reflex exists

`rounded-2xl` is the Tailwind utility that appears most often in component
library examples. `shadow-md` is the utility marked "cards" in the Tailwind
docs. The model learned "card = `rounded-2xl shadow-md p-6 border`" as a
single lexical unit, and reproduces it everywhere.

The result is **no surface hierarchy**. When everything has the same radius,
the same shadow, and the same border, nothing reads as more important than
anything else. The page becomes a flat field of identical containers.

## Bad example (the default, annotated)

```html
<style>
  .card        { border-radius: 16px; box-shadow: 0 4px 6px rgba(0,0,0,0.1);
                padding: 24px; border: 1px solid #e2e8f0; }
  .card:hover  { box-shadow: 0 10px 15px rgba(0,0,0,0.1); }
  .button      { border-radius: 16px; padding: 12px 24px; }  /* same radius as card */
  .input       { border-radius: 16px; padding: 12px; }       /* same radius as card */
  .avatar      { border-radius: 16px; }                       /* same radius as card — square corners on an avatar? */
  .modal       { border-radius: 16px; backdrop-filter: blur(12px);
                background: rgba(255,255,255,0.7); }         /* glassmorphism on everything */
  .container   { border-radius: 16px; }                       /* even the outer container */
</style>
```

**Why this smells:**
- One radius value across every element class — no semantic differentiation.
- One shadow recipe — no depth hierarchy.
- Backdrop blur + translucent white on a modal — the glassmorphism tell.
- Even avatars are 16px rounded, which makes them look like square cards, not avatars.
- The page has no surface hierarchy. Nothing is "above" anything else.

## Good example (source-driven, annotated)

```css
/*
  Source chain for this surface system:
  Product  : a battery-monitoring tool for solar installers
  Visual ref: industrial control panels (SCADA, factory HMIs)
              — they use sharp corners on data, slightly rounded on
              controls, circular on indicators

  Surface hierarchy derived from control-panel conventions:
  - Data displays      → 2px radius   (almost square; data is precise)
  - Interactive controls → 4px radius  (slightly rounded; affords press)
  - Cards / panels     → 8px radius   (clearly rounded; grouped content)
  - Large containers   → 12px radius  (most rounded; outermost shell)
  - Status indicators  → 50% radius   (circles; conventional for indicators)
  - Avatars            → 50% radius   (conventional for avatars)

  Shadow hierarchy:
  - One shadow recipe only. Used to indicate "floating above page."
  - Cards in normal flow: no shadow, just border.
  - Hovered interactive: shadow appears.
  - Modals: stronger shadow.
  - No glassmorphism. Glassmorphism imitates macOS; this is a field tool.

  Border:
  - 1px solid in a warm rule color (#e6dbc2) — warm, not slate.
  - Used to separate, not to decorate.
*/

:root {
  --r-data:    2px;
  --r-control: 4px;
  --r-card:    8px;
  --r-shell:   12px;
  --r-circle:  50%;

  --shadow-rest:  none;
  --shadow-hover: 0 2px 4px rgba(26, 24, 20, 0.08);
  --shadow-float: 0 8px 24px rgba(26, 24, 20, 0.12);

  --border: 1px solid #e6dbc2;
}

.data-readout  { border-radius: var(--r-data); border: var(--border); }
.button        { border-radius: var(--r-control); }
.input         { border-radius: var(--r-control); border: var(--border); }
.card          { border-radius: var(--r-card); border: var(--border); box-shadow: var(--shadow-rest); }
.card:hover    { box-shadow: var(--shadow-hover); }
.shell         { border-radius: var(--r-shell); }
.indicator     { border-radius: var(--r-circle); }
.avatar        { border-radius: var(--r-circle); }

.modal         { border-radius: var(--r-shell); box-shadow: var(--shadow-float);
                background: #f4ede0; /* solid, not translucent */ }
```

**Why this doesn't smell:**
- Five distinct radii, each tied to an element class with a **reason**.
- Shadows differentiate state (rest / hover / float), not just decoration.
- No glassmorphism. The product is a field tool; macOS aesthetics would lie.
- Border is warm, not slate — matches the warm palette from `01-color.md`.
- Avatars are circular (conventional), not 16px square.

## The radius hierarchy rule

Pick 3–5 radii. Assign each to a **class of element**, not to elements
ad hoc. The classes are typically:

| Class | Typical radius | Reason |
|---|---|---|
| Data / labels | 0–2px | Precision, "this is a fact" |
| Controls (buttons, inputs) | 4–6px | Slight rounding affords press |
| Cards / grouped content | 8–12px | Clear grouping, "this is a unit" |
| Shells / outer containers | 12–16px | Outermost layer, softest |
| Avatars / status dots | 50% | Convention; circular = person or status |

State it in a comment. Apply it consistently. This is what "compensating
craft" means in the IOV Labs paper — even if your palette is conventional,
a real radius hierarchy pulls the Tell Score toward 0.

## The shadow hierarchy rule

Pick 2–3 shadow recipes. Assign each to a **state**:

| State | Shadow | Reason |
|---|---|---|
| Rest (in normal flow) | `none` or 1px border only | Doesn't float |
| Hover (interactive) | small Y-offset shadow | "I can be pressed" |
| Float (modal, popover) | large soft shadow | "I'm above the page" |

Avoid `shadow-lg` on every card. Cards in normal flow don't float. Hover
is where shadow earns its place.

## The glassmorphism rule

`backdrop-blur` + translucent background was a 2020–2022 trend that the
training data absorbed as a default. Use it only when:

- The product is genuinely macOS/iOS-adjacent (Apple-style tools), OR
- The floating element genuinely overlaps varied content (overlays on photography), OR
- The aesthetic source is explicitly "glass."

Otherwise use **solid surfaces**. Solid is more legible, more printable,
and reads as deliberate.

## Heuristic questions

1. **How many distinct radius values does the page use?**
   - 1 → you've made no choice. Add a hierarchy.
   - 2 → minimal. Probably enough for simple pages.
   - 3–5 → good. Each should map to an element class.
   - 6+ → too many. Consolidate.
2. **Is each radius tied to a class, or assigned ad hoc?**
   If ad hoc, you're decorating, not systematizing.
3. **How many shadow recipes?**
   - 1 → no state differentiation.
   - 2–3 → good (rest / hover / float).
   - 4+ → too many.
4. **Are cards in normal flow shadowed?**
   They probably shouldn't be. Save shadow for state.
5. **Is `backdrop-blur` used? Why?**
   "Because it looks nice" is not a reason. macOS-adjacent / overlay-on-photo
   / explicit glass aesthetic are reasons.
6. **What color is the border?**
   Default slate is cold. If your palette is warm, the border should be warm.

## Anti-pattern: radius as decoration

Switching everything from `rounded-2xl` to `rounded-lg` is not a hierarchy.
It's the same hierarchy (none) with a different value.

```
Bad:    "Don't use rounded-2xl, use rounded-lg."        ← same flatness
Good:   "Data is 2px, controls 4px, cards 8px, shells 12px,
        indicators 50%. Each tied to an element class
        with a reason."                                  ← real hierarchy
```

## Instruction template

```
Design the surface system. Before producing, answer:

1. Radius hierarchy:
   List 3–5 element classes and the radius for each.
   - data/labels: __px  ← reason
   - controls:    __px  ← reason
   - cards:       __px  ← reason
   - shells:      __px  ← reason
   - indicators:  __%   ← reason

2. Shadow hierarchy:
   List 2–3 states and the shadow for each.
   - rest:   ___        ← reason
   - hover:  ___        ← reason
   - float:  ___        ← reason

3. Backdrop blur:
   yes / no. If yes, what's the source?
   [ macOS-adjacent | overlay on photo | explicit glass aesthetic ]

4. Border color:
   ___ (hex). Is it warm or cold? Why does it match the palette?

Then produce the CSS. Define the values as CSS variables. Annotate each
with its source in a comment. Apply consistently across all components.
```
