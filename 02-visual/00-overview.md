# 02-visual / 00 · Overview

The visual layer is where AI smell is most obvious and most fixable.
The default AI page is a recognizable object: indigo gradient, Inter on white,
three feature cards, `rounded-2xl` everything, soft shadow on every surface.

This layer covers six decision domains:

1. **Color** — where the palette comes from
2. **Typography** — how type pairings are chosen
3. **Layout** — how content blocks are arranged
4. **Surface** — radius, shadow, border treatment
5. **Motion** — easing, duration, when to animate
6. **Iconography** — which icon set, when to use icons at all

---

## The shared rule

For every visual decision, name a source. Sources are:

- **Brand** — logo, named colors, existing assets
- **Locale** — geography, climate, vernacular architecture
- **Content semantics** — what the product *is* (finance, agriculture, clinic)
- **Material reality** — what the product is *made of* (paper, glass, ceramic)
- **User context** — where/when/how it's read (bright sun, dark room, mobile)
- **Reference** — a specific existing design the user named
- **Structural logic** — content weight, hierarchy, flow

"Modern / clean / professional / sleek" are **not sources**. They are the
training distribution talking. If you find yourself reaching for these words,
stop and find an actual source.

---

## The trap to avoid

A page that's "not indigo" can still smell like AI. Replacing indigo with
burnt sienna, Inter with Fraunces, `rounded-2xl` with `rounded-4xl` —
without changing the underlying logic — produces the same smell in a
different costume.

The way out is not "different values for the same properties."
The way out is **a different decision process**.

- Default process: pick the most probable value.
- Guided process: ask what the content needs, derive the value from that.

---

## How to read this layer

Each file below has the same structure:

- **Default reflex** — what the model reaches for unconsciously
- **Why the reflex exists** — the training-data mechanism
- **Bad example** — the default, annotated
- **Good example** — a source-driven alternative, annotated
- **Heuristic questions** — to ask during the decision
- **Instruction template** — to give to the agent

Read all six before producing visual output. The decisions interact:
color affects typography weight choice affects layout density affects
surface treatment. They cannot be made independently.
