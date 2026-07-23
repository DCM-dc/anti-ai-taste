# 05-workflow / 00 · Task analysis

> Read this **before** `01-process.md`. It is the missing stage 0:
> what to do before you even ask the user for sources.

## The gap this file fills

`01-process.md` says: *ask 3–5 questions about sources, then produce.*
`07-paradoxes/03-thin-input-protocol.md` says: *when input is thin,
ask / diverge / label.*

Both assume the only sources available are the ones the user hands
you. That's wrong. **Most tasks carry implicit sources in the task
itself** — in the noun, the verb, the domain, the audience the user
implied but didn't state. A good agent extracts those before asking
anything, so the questions it does ask are sharp rather than generic.

The failure mode this prevents:

```
User:    "Write me a landing page for a battery monitoring tool."
Agent:   "Who's the user? What's the brand color? Two sites you like?"
         [5 generic questions, none derived from the task itself]
User:    [vague answers]
Agent:   [produces default output, labels it "unsourced"]
```

The agent never noticed that "battery monitoring tool" already implies
a domain (industrial / electrical), a probable user (field tech or
facility manager, not consumer), a probable reading context (phone in
sun, not desktop in office), and a semantic palette family
(caution amber, electrical copper, deep industrial green). Those are
not sources — they're **source candidates**, derivable in 10 seconds
from the task noun. The agent's job is to surface them, mark them
as candidates (not facts), and ask the user only the questions that
genuinely remain open.

---

## The four extraction passes

Before asking the user anything, run the task through four passes.
Each pass pulls a different kind of implicit source.

### Pass 1 — Domain pass (what field is this?)

Read the nouns in the task. Map them to a domain. Each domain carries
conventional palette families, typography traditions, and content
shapes that are **Tier 2 sources** (lookup-verifiable, see
`07-paradoxes/02-source-verification.md`) — not hallucinations.

| Task noun(s) | Implied domain | Tier 2 source candidates |
|---|---|---|
| battery / monitoring / telemetry | industrial electrical | caution amber (#FFB800), IEC copper, deep industrial green; mono numerals; control-panel typography (IBM Plex, Roboto Mono) |
| clinic / patient / intake | healthcare | clinical white, sage, muted teal; humanist sans (Source Sans, Open Sans); generous line height for low-vision readers |
| coffee / roaster / single-origin | specialty food & beverage | warm earth tones (ochre, espresso, kraft); editorial serif (Fraunces, Tiempos) for craft narrative |
| finance / portfolio / rebalance | financial services | deep navy, oxblood, off-white; serif for trust (Source Serif, Lora); tabular numerals mandatory |
| farm / harvest / CSA | agriculture | moss, ochre, sky; humanist sans; field-photography-driven palette |
| dev tool / CLI / runtime | developer infrastructure | terminal palette (one accent on near-black); mono-first typography; high information density |

This is **not** "the palette is forest green because agriculture."
That would be Tier 3 affectation. This is: "agriculture is one of the
domains where moss-green is conventional and lookup-verifiable; I'll
treat it as a Tier 2 candidate and let the user override."

The difference: candidates are labeled as candidates. Hallucinations
are dressed as facts.

### Pass 2 — Audience pass (who reads this, where?)

Read the verbs and the implied reading situation. The task rarely
states the audience, but it implies one.

| Signal in task | Implied audience | Implied context | Design consequence |
|---|---|---|---|
| "monitoring tool," "dashboard" | operator / technician | desktop, all day, glanceable | data-first layout, no marketing hero, high contrast |
| "landing page," "convert," "sign up" | prospect, comparing alternatives | phone, 5-second attention | one clear value prop above the fold |
| "essay," "long-form," "deep dive" | engaged reader | desktop or tablet, 10+ minutes | narrow column, comfortable measure (60–75 chars), serif body |
| "API reference," "docs" | developer, looking up specifics | desktop, multiple tabs, scanning | search-first, dense, code blocks, no decoration |
| "story," "novel," "fiction" | reader, immersive | e-reader or print emulation | minimal chrome, generous leading, no UI chrome competing with prose |
| "onboarding email" | new user, mobile, distracted | 3-second open → archive or read | short, single CTA, plain text over HTML |

Again: candidates, not facts. The agent surfaces the implied audience
and asks the user to confirm or correct — *one* question, not five.

### Pass 3 — Constraint pass (what's fixed by the task itself?)

Some constraints aren't choices — they're imposed by the task. The
agent often ignores them because they aren't phrased as constraints.

| Task says | Implicit constraint | Don't violate |
|---|---|---|
| "API reference" | Must be scannable, complete, linkable | Don't impose marketing rhythm (hero, story, CTA). The genre inverts the rhythm rules — see `08-genres/03-technical-doc.md`. |
| "press release" | Must be quotable, dateline-shaped, AP style | Don't impose essay structure. Don't coin concepts. Don't use the "not X but Y" sentence shape. |
| "README" | Must answer: what is this, how do I install it, how do I use it | Don't write a manifesto. Don't put a hero gradient. Don't summarize at the end. |
| "short story" | Must have scene, subtext, sensory detail | Don't impose essay logic. Allow fragments, run-ons, voice extremes — see `08-genres/04-fiction.md`. |
| "newsletter" | Must arrive in an inbox, render in 3 email clients, survive images-off | Don't use a 7/5 asymmetric grid. Don't rely on custom fonts. Plain-text-first. |

Listing these constraints out loud, before producing, prevents the
most common cross-genre failure: **applying marketing-page logic to
non-marketing content.**

### Pass 4 — Anti-default pass (what is the model about to do by reflex?)

Before producing, predict your own first guess. Write it down. This
is the single most useful 30 seconds in the whole workflow.

```
Task:     "Landing page for a battery monitoring tool."

My first guess (predicted):
  - centered hero with a gradient
  - 3-col features (Monitor / Alert / Analyze) with Lucide icons
  - 3-tier pricing, middle elevated
  - "Build the future of battery monitoring" headline
  - indigo / violet accent
  - Inter throughout
```

Once you've written your first guess, **you can see it**. You can't
escape a default you can't name. Naming it is half the work.

Then ask: for each line in the first guess, what's the alternative?
The alternative doesn't have to be brilliant — it has to be
*different and defensible*.

```
Alternative directions (from Passes 1–3):
  - Direction A: dashboard-first (Pass 2 says audience is a field tech)
  - Direction B: photograph of an actual install (Pass 1 says industrial)
  - Direction C: a single quote from an installer (Pass 3 says it's a tool, not a story)
```

Now your 3 candidates in `01-process.md` Stage 2 have actual seeds,
instead of being three redraws of the same template.

---

## The extraction output

Run all four passes, then produce a single short brief **before**
asking the user anything:

```
TASK ANALYSIS (internal, then shared with user)

Domain (Pass 1):
  industrial electrical
  → Tier 2 palette candidates: caution amber, IEC copper, deep
    industrial green
  → Tier 2 typography candidates: IBM Plex Sans + IBM Plex Mono
    (control-panel heritage)

Audience (Pass 2):
  implied: field technician or facility manager
  implied context: phone in sun, glanceable, daily use
  → design consequence: data-first, high contrast, no marketing hero

Constraints (Pass 3):
  - it's a tool, not a story → no narrative arc
  - glanceable → no animation that delays the number
  - sun-readable → contrast floor AA-large minimum

My predicted first guess (Pass 4):
  centered hero, 3-col features, indigo, Inter, "Build the future of..."
  → rejecting: this is the centroid for "SaaS landing page," and the
    task noun says "tool," not "SaaS"

Three directions I'll propose:
  A: dashboard-first
  B: install photograph + telemetry
  C: installer quote + case study

OPEN QUESTIONS for the user (only what Passes 1–3 couldn't resolve):
  1. Brand color (if any)? — affects whether A/B/C uses an accent or
     a brand hue
  2. Do you have a real install photograph? — decides B vs A/C
  3. Is there a real installer quote available? — decides C
```

Note what's happened: the agent asked **3 questions, not 5**, and each
one is sharp and conditional. The user can answer all three in 30
seconds because they're concrete.

This is what "ask before producing" was always supposed to mean. Not
*ask 5 generic questions*, but *ask 3 specific questions that
surfaces the remaining gaps after you've done your own extraction*.

---

## The anti-pattern: extraction as fabrication

The easy failure mode is to treat Pass 1 (domain) as a license to
invent sources. It is not.

```
✗  "Palette: warm cream, evoking the user's hand-made ceramics brand."
   [Task said nothing about ceramics. This is hallucination, not
   extraction. Caught by 07-paradoxes/02.]

✓  "Domain is industrial electrical. Caution amber is a Tier 2
   conventional palette candidate for this domain (IEC 60417,
   lookup-verifiable). Treating as a candidate, not a fact.
   Brand color, if any, would override."
```

The difference is the **modal verb**: *would*, *could*, *candidate* —
not *is*, *evokes*, *matches*. Candidates are honest. Affective
claims dressed as facts are hallucinations.

If you cannot defend a Pass 1 mapping with a 30-second lookup (IEC
standard, AP style guide, financial tabular-numeral convention), it's
Tier 3. Drop it. Admit the gap and ask the user.

---

## How this changes the rest of the workflow

`01-process.md` Stage 1 (Ask) becomes:

```
Old:  Ask 3–5 questions about sources.
New:  Run task analysis (4 passes).
      Surface candidates and predicted default.
      Ask only the questions the analysis couldn't resolve.
      Cap at 3 (was 5).
```

`07-paradoxes/03-thin-input-protocol.md` Path A becomes stronger: even
when input is thin, the task itself supplies candidates, so the agent
isn't reduced to "produce 3 random divergent directions." It can
produce 3 directions **seeded by the task**, while still labeling them
as unsourced candidates pending user confirmation.

`07-paradoxes/05-decision-tiers.md` Tier 1 decisions get a head start:
the task analysis surfaces 2–3 Tier 2 source candidates per Tier 1
decision, so the agent isn't starting from a blank page when it
begins the sourcing conversation.

---

## Heuristic questions

1. **Did you run all four passes before asking the user anything?**
   If you jumped straight to asking, you skipped extraction. Redo.
2. **Did you write down your predicted first guess (Pass 4)?**
   If you didn't name the default, you can't escape it. Redo.
3. **Are your domain→palette mappings Tier 2 (lookup-verifiable)?**
   If any mapping is "evokes," "feels," or "matches," it's Tier 3.
   Drop it or admit it as a candidate, not a source.
4. **Are you asking the user 3 sharp questions or 5 generic ones?**
   If 5 generic, you didn't extract. Redo.
5. **Did you surface candidates as candidates (modal verbs), not
   facts (affective claims)?**
   "Would be" is honest. "Evokes" is hallucination.
6. **Did you list the task-imposed constraints (Pass 3) before
   producing?**
   If you started producing without listing constraints, you'll
   apply wrong-genre logic. Redo.
7. **Do your 3 proposed directions come from the analysis, or are
   they 3 redraws of the same template?**
   If they share palette logic / layout grammar / voice, they're
   not 3 directions. Redo.

---

## Instruction template

```
Before Stage 1 (Ask) of 05-workflow/01-process.md, run task analysis:

PASS 1 — DOMAIN (from task nouns):
  [ ] Identify the implied domain
  [ ] List 2–3 Tier 2 palette / typography candidates
      (each must be 30-second lookup-verifiable; not affective)
  [ ] Mark each as "candidate," not "fact"

PASS 2 — AUDIENCE (from task verbs):
  [ ] Identify implied audience and reading context
  [ ] List design consequences (layout, density, contrast floor)

PASS 3 — CONSTRAINTS (imposed by task, not chosen):
  [ ] List 2–4 constraints the task fixes (genre, deliverable shape,
      must-include sections)
  [ ] For each, note what it forbids (e.g. "API reference → no
      marketing rhythm")

PASS 4 — PREDICTED FIRST GUESS:
  [ ] Write down the centroid output you'd produce by reflex
  [ ] For each line, mark "rejecting because [reason from Pass 1–3]"

OUTPUT (shared with user before asking):
  [ ] Brief: domain, audience, constraints, predicted default,
      3 seeded directions
  [ ] Open questions: max 3, all conditional on what Passes 1–3
      couldn't resolve

FORBIDDEN:
  - Skipping extraction and jumping to "ask 5 questions"
  - Dressing domain mappings as affective facts ("evokes ceramics")
  - Using Pass 1 as license to fabricate brand/user/locale
  - Asking 5 generic questions when 3 sharp ones would do
```
