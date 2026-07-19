# 02-visual / 06 · Iconography

## Default reflex

- Library: **Lucide** (or Heroicons)
- The same four icons on every feature card: `Zap`, `Shield`, `Rocket`, `Sparkles`
- Backup four: `Check`, `Star`, `ArrowRight`, `Bell`
- Style: thin 1.5px stroke, 24×24, monochrome
- Usage: one icon per feature card, top-left, in a `rounded-2xl` container
- Sometimes: emoji instead of icons (🚀⚡🎯🔒) — even worse

## Why the reflex exists

Lucide is the icon library that ships with shadcn/ui, which is the component
system most represented in AI-generated frontends. `Zap` is Lucide's
"speed/fast" icon. `Shield` is "security." `Rocket` is "launch/scale."
`Sparkles` is "AI/new." These four cover 90% of marketing-feature use cases,
so the model reaches for them constantly.

The problem is not Lucide itself. The problem is the **reflex**: every
feature needs an icon, every icon is from the same set, the same four
appear across every product. After you've seen `Zap / Shield / Rocket` on
ten AI pages, the eleventh is recognizable on sight.

## Bad example (the default, annotated)

```html
<section class="features grid grid-cols-3 gap-8">
  <div class="card">
    <div class="icon-wrapper rounded-2xl bg-indigo-50 p-3">
      <LucideIcon name="Zap" class="w-6 h-6 text-indigo-600" />
      <!-- ↑ Zap on a feature called "Fast." The icon is the word. -->
    </div>
    <h3>Fast</h3>
    <p>Lightning-fast performance.</p>
  </div>

  <div class="card">
    <div class="icon-wrapper rounded-2xl bg-indigo-50 p-3">
      <LucideIcon name="Shield" class="w-6 h-6 text-indigo-600" />
      <!-- ↑ Shield on "Secure." The icon is the word. -->
    </div>
    <h3>Secure</h3>
    <p>Enterprise-grade security.</p>
  </div>

  <div class="card">
    <div class="icon-wrapper rounded-2xl bg-indigo-50 p-3">
      <LucideIcon name="Rocket" class="w-6 h-6 text-indigo-600" />
      <!-- ↑ Rocket on "Scalable." The icon is the word. -->
    </div>
    <h3>Scalable</h3>
    <p>Grows with your team.</p>
  </div>
</section>
```

```html
<!-- Even worse: emoji instead of icons -->
<div class="card">
  <div class="text-4xl">🚀</div>     <!-- ← emoji is the most recognizable AI tell -->
  <h3>Fast</h3>
</div>
```

**Why this smells:**
- The icons are redundant with the labels. `Zap` next to "Fast" adds zero information.
- The same four icons appear on every other AI page.
- The icons are in `rounded-2xl` tinted containers — the centroid icon treatment.
- Emoji as feature icons is an immediate giveaway.

## Good example (source-driven, annotated)

```html
<!--
  Source chain for this icon system:
  Product  : a battery-monitoring tool for solar installers
  Visual ref: industrial control panel symbols (IEC 60617 standard)
              — these are the symbols field techs already read on hardware

  Icon strategy:
  1. Don't use icons where labels work. Most "feature cards" don't need
     icons; the title is enough.
  2. Where icons are needed (status, navigation, data), use SVGs that
     match the visual language of the domain.
  3. For battery status, use the IEC battery symbol (rectangle with
     internal bar), not a Lucide "battery" icon that looks like a phone.
  4. For alerts, use the IEC triangle with exclamation. Field techs
     recognize this from hardware.
  5. Stroke width: 1.5px to match the data-grid aesthetic. Same weight
     as the data tables.

  What we DON'T use:
  - Lucide Zap/Shield/Rocket/Sparkles — these are marketing icons; this
    is a tool, not a marketing site.
  - Emoji — never on a tool UI.
  - Tinted rounded-2xl containers — the icons sit in line with text,
    same as data labels.
-->

<!-- Status readout: IEC-style battery symbol, custom SVG -->
<svg viewBox="0 0 32 16" stroke="currentColor" stroke-width="1.5" fill="none">
  <rect x="1" y="3" width="26" height="10" />
  <rect x="27" y="6" width="3" height="4" fill="currentColor" />
  <rect x="3" y="5" width="18" height="6" fill="currentColor" stroke="none" />
</svg>

<!-- Alert: IEC triangle, custom SVG -->
<svg viewBox="0 0 24 24" stroke="currentColor" stroke-width="1.5" fill="none">
  <path d="M12 3 L22 20 L2 20 Z" />
  <line x1="12" y1="10" x2="12" y2="15" />
  <circle cx="12" cy="17.5" r="0.75" fill="currentColor" />
</svg>

<!-- Feature list: NO ICONS. Just titles and descriptions. -->
<section>
  <div class="feature">
    <h3>Live voltage per cell</h3>
    <p>Polled at 5s intervals from the BMS over CAN bus.</p>
  </div>
  <div class="feature">
    <h3>Drift detection</h3>
    <p>Flags any cell > 50mV from the pack mean.</p>
  </div>
  <div class="feature">
    <h3>Field notes per install</h3>
    <p>Photo and text attach to each install record.</p>
  </div>
</section>
```

**Why this doesn't smell:**
- Feature list has **no icons**. The titles and descriptions are clear on their own.
- Where icons are needed (status, alerts), they use **domain-specific SVGs**
  (IEC symbols), not generic Lucide.
- Custom SVGs match the visual weight of the data tables (1.5px stroke).
- No `rounded-2xl` tinted containers. Icons sit in line with content.
- The icon system is tied to the **domain's visual language**, not to the
  component library's defaults.

## The "does this need an icon" rule

Most feature cards don't need icons. The default reflex is to add one
because "cards have icons." But icons are information; if the title already
conveys the idea, the icon is decoration.

| Title | Needs icon? |
|---|---|
| "Fast" | No — title is the information; `Zap` adds nothing |
| "Live voltage per cell" | No — title is precise; icon would be redundant |
| "Settings" (in nav) | Maybe — convention favors gear icon |
| "Alert" (in nav) | Yes — triangle is faster to scan than the word |
| Battery status indicator | Yes — symbol is faster than number+unit at a glance |

The test: **if you remove the icon, is information lost?** If no, remove.

## The library rule

Lucide is not banned. But:

- **Don't use the marketing 4-pack** (`Zap`, `Shield`, `Rocket`, `Sparkles`) — these are the centroid.
- **Consider alternative libraries** for differentiation: Phosphor, Iconoir, Tabler, Heroicons.
- **Custom SVG is often better** for domain-specific concepts. Lucide doesn't have a "battery cell" icon; an IEC symbol does.
- **Match the stroke weight to the rest of the UI.** If your data tables use 1px borders, your icons should be 1.5px stroke. Don't use Lucide's default 2px stroke in a 1px UI.

## The "tinted container" rule

The default icon treatment is `rounded-2xl bg-indigo-50 p-3` containing a
`text-indigo-600` icon. This treatment is so common it's a tell on its own.

Alternatives:
- **Inline** — icon sits next to text, no container. Best for tool UIs.
- **Bordered** — `border border-current p-2` with the same border as everything else.
- **No treatment** — just the icon, sized appropriately.

Pick the treatment that matches the visual system. Don't default to
"indigo-tinted rounded square."

## The emoji rule

**Emoji as feature icons is one of the strongest AI tells** (cited in the
IOV Labs paper as a strong tell in the "AI self-reference" family).

Use emoji only when:
- The product is itself conversational/informal (chat apps, social)
- The emoji is content (a user typed it), not chrome
- The brand explicitly uses emoji as part of identity

For everything else, including any "serious" product, emoji as icons is forbidden.

## Heuristic questions

1. **Does each icon add information the title doesn't?**
   If not, delete the icon.
2. **Which library are you using, and why?**
   "It's the default" is not a reason. "It has the symbols my domain uses" is.
3. **Are you using `Zap / Shield / Rocket / Sparkles`?**
   If yes, you're in centroid territory. Find alternative icons or omit.
4. **Are you using emoji as feature icons?**
   If yes, this is one of the strongest AI tells. Replace or omit.
5. **What's the icon container treatment?**
   If `rounded-2xl bg-X-50`, that's the default. Find an alternative.
6. **Does the stroke weight match the rest of the UI?**
   Icons should feel like they belong to the same system as the data and borders.
7. **For domain concepts, would a custom SVG be more accurate?**
   Lucide's "battery" looks like a phone battery. IEC's battery symbol is
   what field techs recognize. Match the domain.

## Anti-pattern: library swap

Swapping Lucide for Phosphor without changing the strategy is costume change.

```
Bad:    "Don't use Lucide, use Phosphor."                ← same reflex, different set
Good:   "Feature list doesn't need icons — omit them.
        Status indicators use IEC symbols because field
        techs already read them on hardware."             ← strategy change
```

## Instruction template

```
Design the icon system. Before producing, answer:

1. For each proposed icon, answer:
   - What information does it add that the label doesn't?
   - If "nothing," delete the icon.

2. Library / source:
   [ Lucide | Phosphor | Iconoir | Tabler | custom SVG | none ]
   Why this source? "It's the default" is not a reason.

3. Are you using Zap / Shield / Rocket / Sparkles?
   yes / no. If yes, replace with non-centroid alternatives or omit.

4. Are you using emoji as feature icons?
   yes / no. If yes, what makes this product appropriate for emoji?

5. Icon container treatment:
   [ inline | bordered | tinted-square | none ]
   Why? "rounded-2xl bg-X-50" is the default — pick something else.

6. Stroke weight:
   __px. Does it match the rest of the UI's borders/data?

7. For domain-specific concepts, would a custom SVG be more accurate?
   List concepts and the matching domain symbol.

Then produce the icon set. For custom SVGs, document the source
(standard, reference, original). Apply consistently.
```
