# examples / comparison

Side-by-side annotation of `landing-page-bad.html` and `landing-page-good.html`.
Both files implement a SaaS landing page for a battery-monitoring tool.
The bad one uses every default in the book. The good one derives every
decision from a source.

---

## Top-level structure

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Page grammar | nav → centered hero → social proof → 3-col features → 3-tier pricing → FAQ → CTA banner → 4-col footer | nav → dashboard (7/5 split) → alerts log → 1-line footer |
| Sections omitted | none (every standard section included) | hero, social proof, features grid, pricing, FAQ, CTA banner, 4-col footer (all omitted with reasons) |
| Sections added | none | live readout, install list, alerts log (added because the user is a customer, not a prospect) |
| Source of structure | "the standard landing page" | "field tech wants the number, not the pitch" |

**Why the bad one smells:** it includes every standard section whether the
product needs it or not. A field technician who has already paid doesn't
need a marketing hero or a "Trusted by" logo strip.

**Why the good one doesn't:** it omits 7 standard sections and adds 3
non-standard ones. The structure is conditional on the user, not on the
template.

---

## Color

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Primary | `#6366f1` (indigo-500) | `#245944` (brand logo, darkened 8% for AA on cream) |
| Background | `#ffffff` (pure white) | `#f4ede0` (warm cream; reduces glare in sun) |
| Text | `#0f172a` (slate-900) | `#1a1814` (warm near-black) |
| Accent | indigo gradient | `#d97706` (hardware battery-warning amber) |
| Gradient | indigo → violet → fuchsia, 135° diagonal | none (field tools don't have gradients) |

**Why the bad one smells:** every value is the modal value in the training
distribution. There is no source; if asked "why indigo?" the only honest
answer is "because that's what most tutorials use."

**Why the good one doesn't:** every value is conditional. The hue comes
from the brand. The lightness comes from the user context (sun-readable).
The accent comes from hardware convention (amber = battery warning).
The absence of gradient comes from the product type (field tool, not
marketing surface).

---

## Typography

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Body font | Inter, alone | IBM Plex Sans (wider letterforms for data displays; humanist roots match industrial heritage) |
| Display font | none (just bigger Inter) | none (field tools don't have decorative headlines; data is the headline) |
| Mono font | none | IBM Plex Mono (used only for data, labels, nav — never body) |
| Line-height | 1.5 everywhere | 1.55 body (slightly looser for data) |
| Tracking | default | -0.02em on data displays (mono tightened) |

**Why the bad one smells:** Inter alone with no system is the single most
recognizable typography tell. One family does everything; no personality
differentiation; no optical sizing; no tracking adjustment.

**Why the good one doesn't:** two families paired with reasons. IBM Plex
Sans chosen for industrial control-panel heritage (Plex was IBM's in-house
face). IBM Plex Mono restricted to data — never body. No display face
because a field tool with a serif headline would lie about its character.

---

## Layout

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Hero | centered, 100vh, gradient bg, H1 + sub + filled CTA + ghost CTA | none (replaced by live readout) |
| Feature grid | `grid-cols-3`, equal cards | none (the dashboard is the features) |
| Pricing | 3 tiers, middle elevated, `rounded-2xl` + green checks | none (lives on /pricing) |
| Main grid | n/a (everything centered) | `grid-template-columns: repeat(12, 1fr)` with 7/5 split |
| Footer | `grid-cols-4`, Product/Company/Resources/Legal | single line: version + status + support email |

**Why the bad one smells:** every section is full-width, centered,
vertically stacked. Three equal feature cards have no hierarchy of
importance. Three-tier pricing with middle elevated is the modal pricing
pattern. Four-column footer is the modal footer.

**Why the good one doesn't:** the 7/5 split reflects actual content
weight (readout is primary, install list is secondary). The 12-col alerts
log reflects chronological, non-comparable content (not three equal cards).
The footer is one line because a field tech doesn't need a link farm.

---

## Surface (radius, shadow, border)

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Radius | `rounded-2xl` (16px) on everything | 2px (data) / 4px (controls) / 8px (cards) / 50% (status dots) |
| Shadow | `shadow-md` on cards, `shadow-lg` on hover | border-only on cards; small shadow only on hover |
| Border | `border-slate-200` everywhere | `#d4c8a8` (warm rule matching palette) |
| Glassmorphism | `backdrop-blur` on floating elements | none (field tools aren't macOS apps) |

**Why the bad one smells:** one radius value across every element class.
No surface hierarchy. Cards in normal flow have shadow they don't need.
Glassmorphism on a tool UI is a costume.

**Why the good one doesn't:** five distinct radii, each tied to an
element class with a reason (data is sharp; controls are slight; cards
are clearly grouped; status dots are conventional circles). Shadow is
reserved for hover state. Border is warm to match the palette.

---

## Motion

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Universal transition | `transition: all 0.3s ease-in-out` everywhere | property-specific transitions per class |
| Hover scale | `scale(1.05)` | `scale(1.02)` (button press only) |
| Card hover | lift + scale + shadow growth | border-color darkens only |
| Data updates | animated | none (the number is the number) |
| Easing | `ease-in-out` everywhere | `ease-out` for press/hover, decelerating for open/close |
| Bounce | used "for playfulness" | none (field tool, not a toy) |

**Why the bad one smells:** `transition: all` animates properties you
didn't mean to animate. One duration for everything flattens interaction
semantics. `scale(1.05)` is the most recognizable hover tell. Bounce on
a tool UI reads as trying too hard.

**Why the good one doesn't:** five distinct motion treatments, each tied
to an interaction class with a reason. Press is fast and snappy. Hover
is slower and subtler. Data updates don't animate (animating data implies
"we're computing this"). No bounce because the product is a tool.

---

## Iconography

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Library | Lucide (the default) | custom SVG (IEC 60617 industrial symbols) |
| Feature icons | Zap / Shield / Rocket (the centroid 4-pack) | none (feature list has no icons; labels are precise enough) |
| Status icons | Lucide `Battery` (looks like a phone battery) | custom IEC battery symbol (what field techs recognize) |
| Container | `rounded-2xl bg-indigo-50 p-3` (the centroid treatment) | inline, no container |
| Stroke | Lucide default 2px | 1.5px (matches data table weight) |

**Why the bad one smells:** Lucide Zap/Shield/Rocket appear on every
other AI page. The icons are redundant with the labels (Zap next to
"Fast" adds no information). The tinted `rounded-2xl` container is the
centroid icon treatment.

**Why the good one doesn't:** feature list has no icons (the labels
are precise enough). Status uses custom IEC symbols because field techs
already read them on hardware. Stroke weight matches the rest of the UI.
No tinted containers — icons sit inline.

---

## Copy

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Headline | "Build the Future of Work" | (no headline — the readout is the headline) |
| Subhead | "Supercharge your team's productivity with AI-powered workflows that harness the power of artificial intelligence." | (no subhead) |
| Feature copy | "Lightning-fast performance that supercharges your workflow." | "Cell 5 drift exceeded 50mV from pack mean (currently 71mV)" |
| Signature word density | ~17 per 6 sentences (extreme) | 0 |
| Forced elevation | "Start building today. Join thousands of teams already using FlowAI." | none (page ends at the alerts log) |
| Specific numbers | none | 48.2V, 82% SoC, 71mV drift, 4s poll, v2.4.1 |

**Why the bad one smells:** the marketing 4-pack ("Build the Future,"
"Supercharge," "harness the power") all appear in one sentence. No
specific numbers. No proper nouns. No first-person experience. Could
describe any product in any industry.

**Why the good one doesn't:** zero signature words. Specific numbers
everywhere (voltage, SoC, drift, poll interval, version). Proper nouns
(install IDs like "bryant-storage-04"). The copy could not appear in
any other document — it has a fingerprint.

---

## Process

| Decision | Bad (default) | Good (sourced) |
|---|---|---|
| Workflow | one-shot produce → patch → patch | ask → 3 candidates → pick with reason → produce with annotations → self-check → deliver |
| Source gathering | none | 5 questions about user, brand, content, constraint, reference |
| Alternatives | none (single output, then patched) | 3 candidates in different directions (dashboard-first, photo-first, quote-first) |
| Self-check | "looks good" | 8-question self-check, caught and fixed defaults |

**Why the bad one smells:** one-shot production always defaults to the
centroid. Patching swaps one default for another. The process never
asks "what does this product actually need?"

**Why the good one doesn't:** the workflow forces escape from defaults
at every stage. Asking first means the output is conditional on the
user's answers. Generating 3 candidates means the model explores
alternatives. Self-check catches what slipped through.

---

## The single difference

The bad file is **the centroid of the training distribution.** Every
decision is the modal value for that decision.

The good file is **conditional on a source.** Every decision is derived
from the product, the user, the brand, the locale, or the reference.

Same product brief. Same agent. Same tools. The difference is entirely
in **whether the agent asked for sources before producing**, and
**whether it ran self-check before delivering.**

That's the whole repo.
