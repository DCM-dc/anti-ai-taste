# CONTRIBUTING

> This guide improves by accumulating specific, verifiable observations
> of how AI actually behaves. Contributions that add specificity are
> welcome; contributions that add generality are not.

## Why contributions matter

The core risk to this framework is **second-order convergence** —
when "anti-AI taste" itself becomes a recognizable default because
everyone follows the same guide (see
`07-paradoxes/01-second-order-convergence.md`).

The defense against second-order convergence is **specificity**:
sources unique to each project, defaults observed in actual current
models, conventions verified against real references. No single
maintainer can observe every model's defaults across every domain.
That's where contributions come in.

If you've observed a default the guide doesn't mention, or sourced
a decision in a way the guide's examples don't cover, your
contribution directly reduces the framework's bias toward its own
centroid.

---

## What we accept

### 1. New observed defaults (the model reaches for these by reflex)

Examples of useful contributions:

- "I prompted [model] with [task]. It defaulted to [specific choice]
  in 7 of 10 samples."
- "As of [date], [model] no longer defaults to indigo — it now
  defaults to [specific color]. The guide's bad example is stale."
- "New signature word observed: [word]. Appears in [N] of [M]
  samples of [model] on [task type]."

These belong in `02-visual/`, `03-language/`, `04-rhetoric/`, or
`06-checklist/`, depending on the default's layer. Or, if the
default has emerged as an *anti-AI default* (everyone now reaches
for it because the guide told them to), it belongs in
`07-paradoxes/01-second-order-convergence.md`.

### 2. New Tier 2 source candidates (lookup-verifiable conventions)

Examples:

- A new domain palette family with a verifiable reference (ISO
  standard, named style guide, material tradition). Belongs in
  `resources/color-sources.md`.
- A new genre with specific overrides the guide doesn't cover (legal
  drafting, scientific papers, theatrical dialogue). Belongs as a
  new file in `08-genres/`.
- A new locale palette with a real visual tradition. Belongs in
  `resources/color-sources.md` under Regional.

The bar for these: a 30-second lookup must confirm the convention
(see `07-paradoxes/02-source-verification.md`). "I think consulting
firms use navy" is not enough. "FT, Economist, INK all use deep
navy; verifiable via their public style guides" is.

### 3. New examples (bad / good pairs with annotations)

The examples folder currently covers landing pages. Useful additions:

- `article-bad.md` / `article-good.md` — long-form essay
- `readme-bad.md` / `readme-good.md` — open-source project README
- `email-bad.md` / `email-good.md` — onboarding or transactional email
- `api-doc-bad.md` / `api-doc-good.md` — API reference page
- `fiction-bad.md` / `fiction-good.md` — short story opening

Each pair must include annotations explaining **which specific
decision caused each tell** in the bad version, and **which source
drove each replacement** in the good version. See
`examples/comparison.md` for the format.

### 4. Validation findings

If you've run a validation method from `05-workflow/03-validation.md`
and found tells the guide's self-check misses, contribute them:

- The tell (specific, observable)
- Which self-check question failed to catch it
- A proposed new self-check question that would catch it

These belong as edits to `05-workflow/02-self-check.md` or as
additions to `06-checklist/`.

### 5. Re-calibration reports

When a new model ships and you've run the re-calibration check from
`VERSION.md`, contribute the result:

- Model checked, date, sample size
- Defaults observed (matched guide / new defaults / structural change)
- Files updated (if you updated them)
- Add a row to the calibration log in `VERSION.md`

---

## What we do NOT accept

### Affective source claims dressed as conventional

> "I feel like clinics should use sage green because it's calming."

This is Tier 3 — see `07-paradoxes/02-source-verification.md`. The
guide rejects Tier 3 sources in its own output; it rejects them in
contributions too. Bring a citation (a hospital design study, a
published clinical UX guideline), not a feeling.

### Ban-list additions

> "We should add 'emerald gradient' to the ban list."

The guide doesn't ban — see `01-philosophy.md`. If you've observed
emerald gradient as a new default, contribute it as a *default
reflex observation* (with samples), not as a ban. The fix is to
teach the agent to source the choice, not to forbid the color.

### Generic anti-AI defaults

> "Replace indigo with burnt sienna."

Burnt sienna is itself an anti-AI default now (see
`07-paradoxes/01-second-order-convergence.md`). Contributions that
propose new "anti-AI defaults" without a per-project source will be
rejected. The fix is sourcing, not swapping one default for another.

### Refusals to engage with the structural layer

> "The 'name a source' rule is too hard. Let's just ban the top 20
> AI tells."

The structural layer is the framework. Contributions that propose
dismantling it in favor of a ban list will be rejected. If you want
a ban list, fork the repo — the MIT license permits it.

---

## How to contribute

### For small changes (typos, single-example updates, new entry in an existing table)

Open a PR directly. In the PR description, include:

1. What you changed
2. Why (what default / gap / staleness it addresses)
3. How you verified it (for Tier 2 claims: the 30-second lookup reference)

### For medium changes (new file in an existing section, new example pair)

Open an issue first describing what you want to add. This avoids
you writing a full file and then discovering the maintainers had a
different structure in mind. Once the issue gets a "go ahead," open
a PR.

The PR must include:

1. The new file(s)
2. An update to the section's `00-overview.md` referencing the new file
3. An update to `README.md`'s repo map
4. (If applicable) an update to `PROMPT.md`
5. For example pairs: annotations on every decision, per
   `examples/comparison.md` format

### For large changes (new section, structural reorganization, change to
the source-tier classification or decision-tier framework)

Open an issue with the prefix `[large]` and make the case. Large
changes need discussion before PR. The framework's structural
decisions are deliberately load-bearing; changing them affects every
downstream file.

### For re-calibration reports

Open a PR against `VERSION.md` with:

1. A new row in the calibration log
2. (If defaults have moved) updates to the affected files
3. (If you updated the anti-AI defaults list) a note in
   `07-paradoxes/01-second-order-convergence.md` that the list was
   re-derived as of [date]

---

## Style guide for contributions

Match the existing voice of the repo. Specifically:

- **Direct, second-person.** "You," not "one." "The agent," not
  "an AI system."
- **Annotated examples over abstract rules.** Show the bad example,
  show the good example, explain the specific decision that differs.
  Don't write paragraphs of principle without grounding in an
  example.
- **Modal verbs for candidates, indicative for facts.** "Would be a
  candidate" is honest. "Is the right choice" is overreach.
- **No filler.** No "in today's fast-paced world," no "as AI
  continues to evolve," no "it's important to note that." If a
  sentence doesn't carry information, cut it. (The guide violates
  its own principle if it sounds like AI.)
- **Code blocks for templates, prose for explanation.** The
  instruction templates at the end of each file are the operational
  distillation. The prose above them is the *why*.

If your contribution reads like AI output, it will be rejected on
those grounds alone — not because we're being precious, but because
a guide against AI smell that smells like AI is self-defeating.

---

## Review criteria

Maintainers will review PRs against:

1. **Specificity.** Does this add a specific observation, or generic
   advice? Generic → reject.
2. **Verifiability.** Is every Tier 2 claim backed by a 30-second
   lookup? Unverifiable → reject or ask for citation.
3. **Second-order safety.** Does this contribution add a new
   "anti-AI default" without per-project sourcing? → reject.
4. **Structural coherence.** Does this fit the existing framework
   (source tiers, decision tiers, genre overrides)? Or does it
   propose a parallel system? Parallel → ask to integrate first.
5. **Voice match.** Does it read like the rest of the repo? If it
   reads like AI → reject with that note.

---

## Licensing your contribution

By contributing, you agree your contributions are licensed under the
MIT license (see `LICENSE`). No CLA, no contributor license
agreement — just MIT.

---

## A note on the maintainer's own bias

The maintainer is also a model-trained entity (or a human deeply
shaped by model output, depending on who's editing this when). The
guide will reflect that bias. Contributions that point out the
bias — "your examples all come from US/Western European conventions;
here's a Korean editorial convention with a real reference" — are
specifically valuable.

The framework's defense against its own bias is the same as its
defense against AI smell: **name the source, mark the bias, don't
dress defaults as universals.**
