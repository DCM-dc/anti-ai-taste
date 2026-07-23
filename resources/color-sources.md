# resources / color-sources

> A lookup table of **Tier 2 sources** (conventional, 30-second
> verifiable — see `07-paradoxes/02-source-verification.md`) for
> palette decisions. The point of this file: when you can't source
> a palette from the user's brand, you can still source it from the
> *domain's actual conventions* instead of from "looks modern."

## How to use this

This is **not** a "pick a palette from the list" menu. That would
just relocate the centroid (see `07-paradoxes/01-second-order-convergence.md`).
If every agent reads this file and picks "industrial green" for
electrical, "industrial green" becomes the new default.

The correct use:

1. **Confirm the domain** with the user (one question, see
   `05-workflow/00-task-analysis.md` Pass 1).
2. **Look up the domain's conventional palette family** here.
3. **Pick a specific hue within the family** based on a Tier 1 source
   the user provided (brand color, locale light, content semantics),
   not on what "looks nice."
4. **Annotate** which family you picked and why (e.g. "IEC 60417
   caution amber family, hue shifted toward brand orange +8°").

If you skip step 3 and pick "the standard amber for industrial,"
you're using a Tier 2 source as if it were Tier 1. That's better
than "modern indigo," but it's still relocating the centroid. The
escape is: use the family as a *constraint*, not as a *choice*.

---

## Industrial / electrical / monitoring

Conventional palette families, each lookup-verifiable:

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| IEC 60417 caution amber | IEC 60417-5510, ISO 7010 W012 | #FFB800 ± 10° | safety-critical warnings, alert states |
| Industrial copper | electrical conductor material | #B87333 ± 5° | "electrical" semantic without using a literal warning color |
| Deep industrial green | control panel / SCADA convention | #1B4332, #2D5A3D | "operational / normal" status, field-readable |
| Off-white panel cream | legacy industrial equipment | #F4F0E6 | sun-readable backgrounds in field contexts |
| Caution red | ISO 7010 W001 | #C8102E | fault / critical alert only — never decorative |

Tabular-numeral typography convention: any mono with `tnum` feature
(Roboto Mono, IBM Plex Mono, JetBrains Mono). Numerals must not
shift width when refreshed.

---

## Healthcare / clinical

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| Clinical white | hospital lighting convention | #FAFAF7 (slight warm to reduce glare under fluorescents) | default background |
| Sage / muted teal | calming-color studies in waiting rooms | #8FA68E, #5E8B8B | accent, non-alert |
| Vital-sign red | pulse oximeter / ECG convention | #C73E1D | alert only — never decorative |
| Chart background blue | EHR / Epic / Cerner convention | #E6EEF5 | data chart backgrounds (low-contrast for figure-ground) |

WCAG consideration: clinical contexts often have low-vision elderly
readers. Contrast floor is AA-large minimum, often AAA. Humanist
sans (Source Sans, Open Sans) for body — never geometric (Futura,
Avenir) for clinical body text.

---

## Financial services

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| Deep navy | banking heritage (INK-style) | #0A2540, #1A237E | primary brand / trust color |
| Oxblood / burgundy | private banking, ledger convention | #6B1F2E | accent for "legacy / established" register |
| Off-white / parchment | ledger paper, annual report convention | #FBF9F3 | background, body text contrast |
| Tabular-numeral requirement | FT/Economist style guides | (typographic, not chromatic) | any number in a table or chart |

Financial typography convention: serif for trust body (Source Serif,
Lora, Tiempos), tabular numerals mandatory in any column of figures.
Sans-serif is acceptable only for navigation / metadata.

---

## Agriculture / food / craft

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| Moss / field green | actual crop reference (not "green = agriculture") | #4A5D23, #6B7F3F | only if the specific crop or locale implies it |
| Ochre / wheat | harvest grain color | #C68E17, #D4A574 | food / grain content |
| Sky / weather | field-sky reference | #B8D4E3 | sparingly; never as primary |
| Kraft / unbleached | packaging material reference | #C9A876 | craft / artisan register |

Critical: do not use "green = agriculture" as a rule. Use "this
farm's actual main crop is wheat → ochre family" as a source.
Generic "agriculture = green" is Tier 3 affectation.

---

## Developer tooling / infrastructure

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| Terminal palette | VT100 / xterm 16-color convention | #1E1E1E background, #00FF66 or #FF6B35 accent | CLI tools, terminal-first products |
| Code editor dark | VS Code / Sublime default dark themes | #1E1E1E, #2D2D30 | code surfaces only — not marketing |
| Syntax highlight palette | TextMate / Linguist conventions | varies by token type | code blocks; never decorative |

Convention: one accent on near-black. Multiple bright accents = the
"cyberpunk default," which is itself a centroid.

---

## Editorial / long-form

| Family | Reference | Hex range | Use when |
|---|---|---|---|
| Newsprint cream | newsprint paper stock | #F5F1E8 | long-form essay background, print emulation |
| Ink black | printing press ink | #1A1A1A (not pure #000) | body text — pure black is a screen default, not print convention |
| Editorial red | NYT / Economist section markers | #B01E2E | sparingly — section markers, pull quotes |

Typography convention: serif body (Tiempos, Source Serif, Lora) for
long-form; comfortable measure (60–75 characters per line);
generous leading (1.5–1.7 for body).

---

## Regional / locale palette candidates

For use only when the locale is **stated by the user** (not inferred
from vibes). Each entry references an actual visual tradition, not a
stereotype.

| Locale | Source tradition | Palette | Use when |
|---|---|---|---|
| Portugal (Azulejo tradition) | glazed ceramic tile convention | #2E5A88 (azul), #F2E8DC (cream), #8B3A2F (terracotta) | user states Portugal context, esp. craft / heritage products |
| Japan (Traditional Woodblock, Ukiyo-e) | Edo-period woodblock print palette | #1A3A5C (ai indigo), #C8553D (beni red), #E8DCC4 (washi) | user states Japan context, esp. craft / editorial |
| Mexico (Papel Picado / Folk) | cut-paper folk art tradition | #E63946, #F4A261, #2A9D8F | user states Mexico context, esp. celebration / folk products |
| Nordic (Kvadrat / Marimekko tradition) | Scandinavian textile design heritage | #4A6572, #D4A5A5, #E8E4DC | user states Nordic context, esp. minimal / craft |
| Morocco (Zellige tradition) | geometric mosaic tile convention | #1B5E20, #D4A574, #B71C1C | user states Morocco context, esp. craft / hospitality |

**Hard rule:** do not use any of these if the user did not state
the locale. "Evokes Morocco" with no Morocco in the input is Tier 3
hallucination — see `07-paradoxes/02-source-verification.md`.

---

## What this file is NOT

- **Not a menu.** Picking from this list without a Tier 1 source
  (brand, user statement, locale) just relocates the centroid.
- **Not exhaustive.** Domains and locales not listed here are not
  "default to indigo." They're "look it up yourself and add it here
  via `CONTRIBUTING.md`."
- **Not authoritative.** The references are starting points for
  30-second verification, not gospel. If you find a better source
  (e.g. a domain style guide the user actually follows), use that.
- **Not a substitute for brand.** If the user has a brand color,
  it wins. Domain convention is a fallback when brand is absent.

---

## Adding to this file

See `CONTRIBUTING.md`. The bar for additions is:

1. **Tier 2 verifiable.** A 30-second lookup must confirm the
   convention. "I think consulting firms use navy" is not enough.
   "INK, Financial Times, Economist all use deep navy; verifiable
   via their style guides" is.
2. **Domain-specific.** Not "blue = trust." That's affective, not
   conventional.
3. **Annotated with the reference.** IEC standard, ISO standard,
   style guide, material reference, named tradition.
4. **Tested for second-order convergence.** If your addition would
   become a new default (e.g. "every agent picks copper for
   electrical"), it's not adding variety — it's relocating the
   centroid. Don't add it, or add multiple alternatives within the
   family so the choice is still sourced per-project.
