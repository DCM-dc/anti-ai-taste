# 06-checklist / Visual

> Quick-reference leaf-node checklist. Run after producing visual output.
> This catches defaults; the principle layer (`02-visual/`) prevents them.

---

## Color

- [ ] Primary hue has a named source (brand / locale / content / user / reference).
- [ ] Lightness matches reading context (sun → high contrast, dark room → low).
- [ ] Temperature is a choice, not a default (warm vs cold vs neutral — defend it).
- [ ] Accent color has a reason (domain convention / brand secondary / contrast).
- [ ] Gradient: if used, what does it communicate? If you can't answer, delete it.
- [ ] No indigo → violet → fuchsia diagonal gradient unless explicitly sourced.
- [ ] Border color matches palette temperature (slate is cold; warm palette needs warm border).
- [ ] Could this palette appear in 1000 other AI outputs? If yes, source harder.

## Typography

- [ ] At least 2 type families paired (display + body).
- [ ] Display face chosen for content personality (not "clean").
- [ ] Body face chosen for reading context (not "Inter by default").
- [ ] Inter alone is refused unless accompanied by a real type system (optical sizing, tracking, weight hierarchy).
- [ ] Mono restricted to code / data / labels, never body.
- [ ] Optical sizing (`font-variation-settings: 'opsz'`) used if variable font loaded.
- [ ] Tracking differentiated by role (headlines tight, body default).
- [ ] Line-height differentiated by role (body loose, headings tight).
- [ ] CJK fallback specified for any Chinese-content page (PingFang SC, Songti SC, etc.).

## Layout

- [ ] Content blocks inventoried with weights before grid chosen.
- [ ] Equal-weight blocks may share grid; unequal-weight blocks must not.
- [ ] At least one standard section deliberately omitted (hero / social proof / 3-col features / pricing / FAQ / CTA banner / 4-col footer).
- [ ] No centered hero with H1 + sub + filled CTA + ghost CTA unless explicitly justified.
- [ ] No `grid-cols-3` feature cards with Lucide Zap/Shield/Rocket unless explicitly justified.
- [ ] No 3-tier pricing with middle elevated and `rounded-2xl` + green checks unless explicitly justified.
- [ ] No 4-column footer with Product/Company/Resources/Legal unless explicitly justified.
- [ ] At least one asymmetric grid (`col-span-7 + col-span-5` or similar).
- [ ] Could this layout be described as "[standard template] with [small tweak]"? If yes, rethink.

## Surface

- [ ] 3–5 distinct radius values, each tied to an element class.
- [ ] Radius classes: data (0–2px), controls (4–6px), cards (8–12px), shells (12–16px), indicators (50%).
- [ ] No `rounded-2xl` on everything.
- [ ] 2–3 shadow recipes, tied to state (rest / hover / float).
- [ ] Cards in normal flow don't have shadow (border is enough).
- [ ] Backdrop blur (`backdrop-blur`) used only with explicit reason (macOS-adjacent / overlay-on-photo / explicit glass).
- [ ] Border color matches palette temperature.

## Motion

- [ ] 4–6 motion treatments, each tied to an interaction class.
- [ ] Press: 80–120ms, ease-out, transform only.
- [ ] Hover: 120–180ms, ease-out, transform / border / color.
- [ ] Open/close: 180–240ms, decelerating, opacity + transform.
- [ ] Page: 200–300ms, decelerating, opacity.
- [ ] Data updates: no transition (it's a fact, not an animation).
- [ ] No `transition: all` anywhere — explicit property lists only.
- [ ] Hover scale ≤ 1.03 (1.05 is the AI tell).
- [ ] No bounce / elastic easing unless product is genuinely playful.
- [ ] `prefers-reduced-motion` respected.

## Iconography

- [ ] For each icon: what information does it add that the label doesn't?
- [ ] If "nothing," icon is deleted.
- [ ] No Lucide `Zap / Shield / Rocket / Sparkles` 4-pack.
- [ ] No emoji as feature icons.
- [ ] Icon library / source chosen with reason (not "it's the default").
- [ ] Custom SVG considered for domain-specific concepts.
- [ ] Stroke weight matches the rest of the UI's borders / data.
- [ ] Icon container treatment: not default `rounded-2xl bg-X-50`.

## Final

- [ ] Every major design decision annotated with a source comment.
- [ ] Could this entire page appear in 1000 other AI outputs? If yes, redo.
