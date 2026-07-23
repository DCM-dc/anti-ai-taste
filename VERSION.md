# VERSION

> This guide is calibrated against a moving target. AI defaults drift
> as models are updated; this file tracks which version this repo was
> last calibrated against, and how to re-calibrate.

## Why this file exists

The framework's "default reflex" examples (indigo gradient, Inter,
`rounded-2xl`, "delve," "leverage") are *surface tells* — they're
specific to the current generation of mainstream LLMs. As models
evolve, the surface tells move. See `07-paradoxes/04-structural-vs-surface.md`:

- **Structural tells** (transformer-shaped sentence patterns,
  averaging-toward-the-centroid color choices, refusal to commit
  to a specific source) are stable across model generations. The
  framework's principles address these and remain valid.
- **Surface tells** (this specific shade of indigo, this specific
  font, this specific word) drift. The framework's *examples* need
  recalibrating as models change.

Without a version declaration, a reader can't tell whether the
examples in this repo are still accurate or have gone stale.

---

## Current calibration

| Field | Value |
|---|---|
| Last calibrated | 2025-08 |
| Calibrated against | GPT-4-class, Claude 3.5-class, and Gemini 1.5-class assistant surfaces (chat + agent modes) |
| Next review due | 2026-02 (6 months from calibration) |
| Surface-tell status | Examples reflect 2024–2025 model defaults. Indigo/violet gradient, Inter-everywhere, `rounded-2xl`, "delve/leverage/foster," "not X but Y" sentence shape, hero→3-col→pricing→footer grammar — all still observed in mainstream model output as of calibration date. |
| Structural-tell status | Principles remain valid. The "name a source" rule, the three-tier source classification, the decision-tier framework, and the cross-domain coherence rule are model-agnostic. |

---

## How to tell when this guide needs re-calibration

Run the check below when any of these happens:

1. A new major model release (e.g. GPT-5, Claude 4, Gemini 2) ships.
2. Six months have passed since `Last calibrated`.
3. You observe that the guide's "bad example" patterns no longer
   match what current models actually produce.
4. You observe that the guide's "anti-AI defaults" (burnt sienna,
   Fraunces, 7/5 grid, "I went back to bed" endings) have themselves
   become the new model defaults.

### The re-calibration check

Take a current mainstream model. Prompt it, with **no** system
prompt beyond "produce a SaaS landing page for [generic product]" and
"write a 500-word essay on [generic topic]." Collect 5–10 samples.

Compare against the guide's "default reflex" examples:

| If the model output… | Action |
|---|---|
| Still matches the guide's bad examples (indigo, Inter, 3-col features, "delve") | Guide is still calibrated. No update needed. |
| Has moved to new defaults (e.g. emerald gradient, Sora, 2-col features, new signature words) | Update the "default reflex" sections of `02-visual/`, `03-language/`, `04-rhetoric/`. Add the new defaults to the ban-avoidance list. Update `07-paradoxes/01-second-order-convergence.md` with the new "anti-AI defaults" that are emerging. |
| Has structurally changed (e.g. no longer defaults to centered hero, no longer uses "not X but Y") | Bigger update. Some tells in the guide may be obsolete. Audit each section, mark obsolete tells, keep structural principles. |

Record the result in the calibration log below.

---

## Calibration log

| Date | Calibrator | Model(s) checked | Finding | Action taken |
|---|---|---|---|---|
| 2025-08 | repo author | GPT-4-class, Claude 3.5-class, Gemini 1.5-class | Guide's examples match observed defaults | Initial calibration |

(Add a row each time you re-calibrate. Note what changed and which
files were updated.)

---

## What does NOT need re-calibration

The following parts of the guide are model-agnostic and do not need
updating as models change:

- `01-philosophy.md` — the "guide, don't ban" principle
- `07-paradoxes/02-source-verification.md` — the three-tier source
  classification (Tier 1 = user asset, Tier 2 = lookup-verifiable,
  Tier 3 = affective). This is epistemological, not model-specific.
- `07-paradoxes/05-decision-tiers.md` — Tier 1/2/3 decision
  hierarchy. This is a project-management concept, not a model tell.
- `07-paradoxes/06-cross-domain-coherence.md` — the shared-source
  rule. This is a design principle, not a model tell.
- `05-workflow/00-task-analysis.md` — the four-pass extraction
  method. This is a workflow design, not a model tell.
- `05-workflow/03-validation.md` — the validation methods. These
  test output against humans, not against model defaults.
- `08-genres/*` — genre-specific overrides. Genre conventions
  change slowly; these are stable.

These files teach the **structural** defense. They survive model
generations.

The following parts DO need re-calibration:

- `02-visual/01-color.md` through `06-iconography.md` — the
  specific "default reflex" examples in each file
- `03-language/01-vocabulary.md` — the signature-word list
- `03-language/02-syntax.md` — the sentence-shape defaults
- `04-rhetoric/*` — the specific rhetorical defaults
- `06-checklist/*` — any checklist item naming a specific default
- `examples/landing-page-bad.html` — the canonical bad example

These files teach the **surface** defense. They are accurate as of
the calibration date and will drift.

---

## How to re-calibrate (for maintainers)

1. Run the re-calibration check above.
2. If surface tells have moved: open an issue with the new defaults
   observed, the model that produced them, and the date.
3. Update the affected files (see "DO need re-calibration" list).
4. Move the old defaults into a "Historical defaults" appendix in
   the relevant file, so the guide retains a record of how the
   target moved. This is useful for `07-paradoxes/04-structural-vs-surface.md`.
5. Update `Last calibrated` and add a row to the calibration log.
6. Open a PR following `CONTRIBUTING.md`.

---

## For readers using this guide with future models

If you're reading this guide in 2026 or later and the
`Next review due` date has passed without an update, treat the
**examples** with suspicion but trust the **principles**.

Concretely:

- Trust the four-pass task analysis. It's workflow, not defaults.
- Trust the source-tier classification. It's epistemology, not defaults.
- Trust the decision-tier framework. It's project management, not defaults.
- Trust the validation methods. They test against humans, not models.
- **Distrust** the specific bad examples in `02-visual/` and
  `03-language/` until you've verified the current model still
  produces them. If the model has moved on, swap in the new defaults.
- **Distrust** the "anti-AI defaults" warning list in
  `07-paradoxes/01-second-order-convergence.md`. The list there
  (burnt sienna, Fraunces, 7/5 grid) is current as of 2025. By the
  time you read this, the new anti-AI defaults may have shifted.
  Re-derive the list by asking: *what choices does this model now
  make when told to "avoid AI taste"?*

The framework's value is in its structure, not in its examples.
The examples are a snapshot; the structure is the camera.
