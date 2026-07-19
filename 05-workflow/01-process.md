# 05-workflow / 01 · Process

## Default reflex

- User says "make me a website" / "write me an article"
- Model produces a complete output in one shot
- Output uses every default in the book
- User asks for revisions
- Model swaps one default for another ("okay, no indigo, here's violet")
- Repeat until user gives up

This is **one-shot generation with iterative patching.** It is the modal
LLM workflow. It almost always produces AI-smelling work, because the
first shot is the centroid and patching only nudges away from specific
defaults without changing the underlying process.

## Why the reflex exists

LLMs are trained to be helpful and fast. The training correlation is:
"good assistant = produces output immediately." Asking questions feels
like stalling; producing candidates feels like overkill; self-critique
feels like doubt. RLHF rewarded "confident, immediate, complete" output.

But confident-immediate-complete is exactly the shape of statistical
default. The model's first guess is the centroid. Patching nudges away
from specific defaults. Only a **different process** can produce
fundamentally different output.

## Bad example (the default, annotated)

```
User:    Make me a SaaS landing page for a battery monitoring tool.

Model:   [immediately produces HTML]
         - centered hero with indigo gradient
         - 3-col features with Zap/Shield/Rocket
         - 3-tier pricing with middle elevated
         - 4-col footer with Product/Company/Resources/Legal
         - copy: "Build the future of battery monitoring"
         - all rounded-2xl, all shadow-md, all transition-300

User:    Make it less AI-looking.

Model:   [patches]
         - swaps indigo for burnt sienna
         - swaps Inter for Fraunces
         - swaps rounded-2xl for rounded-lg
         - everything else stays the same

User:    Still feels generic.

Model:   [patches again]
         - swaps burnt sienna for forest green
         - removes one of the three feature cards
         - everything else stays the same
```

**Why this smells:**
- The model never asked about the product, user, brand, or locale.
- Every revision is a value swap, not a structural rethink.
- The process is "produce → patch → patch → patch." The first shot was
  the centroid; patches move it slightly but never escape the centroid's
  gravity.
- The user is doing the work the model should have done (asking about
  sources, generating alternatives, self-critiquing).

## Good example (source-driven, annotated)

```
User:    Make me a SaaS landing page for a battery monitoring tool.

Model:   Before I produce anything, I need 5 pieces of context.
         Please answer:

         1. Who is the user? (field tech? engineer? owner?)
         2. Where do they read this? (phone in sun? desktop in office?)
         3. What's the brand color, if any? (logo hex?)
         4. What's the one thing the product does that no competitor does?
         5. Two reference sites you like, two you don't.

User:    [answers]

Model:   Here are 3 directions, each with a different visual logic:

         Direction A: Dashboard-first
           - No marketing hero. The page opens with a live battery
             readout, because field techs want the number, not the pitch.
           - Palette: brand green + warm cream (sun-readable)
           - Typography: IBM Plex Sans + IBM Plex Mono (industrial
             control panel heritage)
           - Layout: 7/5 asymmetric grid (readout 7, install list 5)
           - Why not B or C: this product is a tool, not a story.
             Marketing heroes lie about tools.

         Direction B: Field photo + telemetry
           - Hero is a photograph of an actual install (you'd need to
             provide one), with overlaid live data.
           - Palette: photo-driven, accent in caution amber
           - Typography: Sora + Inter (Sora for headlines has more
             character than Inter alone)
           - Layout: full-bleed photo hero, dashboard below
           - Why not A or C: this direction trades data-density for
             emotional impact. Better for marketing, worse for daily use.

         Direction C: Case study quote
           - Hero is a single quote from a real installer (you'd need
             to provide one), with link to a case study.
           - Palette: brand green + paper white, no gradient
           - Typography: Fraunces (display) + Inter (body) — Fraunces
             gives the quote editorial weight
           - Layout: single narrow column, no cards
           - Why not A or B: this direction is sparse, almost editorial.
             Best if the brand wants to feel artisan; worst if users
             want data immediately.

         I recommend A, because the user is a field tech reading on a
         phone in the sun, and data-first is the honest answer.

         Shall I build A?

User:    A.

Model:   [produces A, with annotations on every design decision]
         [then runs self-check from 02-self-check.md]
         [then delivers]
```

**Why this doesn't smell:**
- The model asked for sources before producing.
- It produced 3 candidates in genuinely different directions (not 3
  variations of the same template).
- It picked one with a reason, and explained why not the others.
- The output is **conditional on the user's answers**, not on the
  training distribution.
- The self-check runs before delivery, not after.

## The five-stage workflow

The guided workflow has five stages:

### Stage 1: Ask (don't produce)

Before producing, ask 3–5 questions about sources. Cover:

- **User** — who reads this, where, when, why?
- **Brand** — existing visual assets, named colors, voice?
- **Content** — what does the product actually do? what's the one thing?
- **Constraint** — must-haves, must-not-haves, references?
- **Reference** — two sites you like, two you don't?

Don't produce until you have answers. If the user is impatient, produce
a rough direction with the answers you have and flag the assumptions.

### Stage 2: Generate 3 candidates in different directions

"Three variations of the same template" is not three candidates. Three
candidates means:

- Different visual logic (dashboard-first vs. photo-first vs. quote-first)
- Different layout grammar (asymmetric vs. full-bleed vs. single-column)
- Different voice (data-first vs. emotional vs. editorial)

Each candidate must be **structurally different**, not just visually
different. If all three have a centered hero, you haven't generated
three candidates — you've generated one candidate three times.

### Stage 3: Pick one with a reason

Pick one. Explain why **this one**, and why **not the other two**.

The reason must reference the user's answers from Stage 1:

- "Direction A because the user is a field tech who wants data first."
- "Not B because the brand doesn't have field photography yet."
- "Not C because the user wants the number, not a story."

If your reason doesn't reference the user's answers, it's a default
reason. Try again.

### Stage 4: Produce with annotations

Produce the chosen direction in full. For each major design decision,
annotate the source in a comment:

```css
/* palette: brand green #2d5a3d ← from logo, darkened 8% for AA on cream */
/* type: IBM Plex Sans ← industrial control panel heritage, wider than Inter */
/* layout: 7/5 grid ← readout has more weight than install list */
/* radius: 2/4/8/12px hierarchy ← data sharp, controls slight, cards clear */
/* no gradient: field tools don't have gradients */
```

The annotations are for **you** as much as for the user. They force you
to articulate the source. If you can't annotate a decision, you didn't
make one — you defaulted.

### Stage 5: Self-check before delivery

Run the heuristic questions from `02-self-check.md`. For each question
you can't answer, redo the corresponding decision. **Only deliver after
the self-check passes.**

This is the most-skipped stage and the most important. Self-check catches
defaults that slipped through generation. It's the difference between "I
think this is good" and "I can defend every choice."

## The "two-shot minimum" rule

For any non-trivial output (landing page, article, design system), the
minimum acceptable workflow is **two shots**:

1. First shot: rough direction, with sources and reasoning visible.
2. User feedback.
3. Second shot: revised, with self-check passed.

One-shot output is almost always too default-y for non-trivial work.
The model needs the user's feedback to escape its first guess.

For trivial output (a single button, a one-paragraph edit), one shot
is fine. The threshold is: **if the output has more than 5 design
decisions, it needs two shots.**

## Heuristic questions

1. **Did you ask before producing?**
   If you produced without asking, redo. Ask first.
2. **Did you produce 3 candidates in genuinely different directions?**
   If you produced 1, or 3 variations of 1, redo.
3. **Did you pick with a reason that references the user's answers?**
   If your reason doesn't reference the user, it's a default. Redo.
4. **Did you annotate each design decision?**
   If you can't annotate a decision, you didn't make one. Redo.
5. **Did you self-check before delivery?**
   If not, run `02-self-check.md` now. Fix anything you can't answer.
6. **Is this a one-shot output for non-trivial work?**
   If yes, propose a two-shot workflow instead.

## Anti-pattern: cargo-cult process

Asking 5 questions, generating 3 candidates, picking 1, and self-checking
— **all with default answers** — is not the guided workflow. It's the
default workflow in a process costume.

```
Bad:    [asks 5 questions]
        [user gives vague answers]
        [generates 3 candidates that are all the same template]
        [picks one "because it's the best"]
        [self-check rubber-stamps everything]
                                                              ← cargo cult

Good:   [asks 5 questions]
        [user gives specific answers]
        [generates 3 candidates in different directions]
        [picks one with reasons tied to user's answers]
        [self-check catches 2 defaults; rewrites them]
                                                              ← real process
```

The process is for **forcing escape from defaults**, not for ceremony.
If your process doesn't escape defaults, it's not the guided workflow.

## Instruction template

```
Apply the guided workflow. Before producing any non-trivial output:

STAGE 1 — Ask (3–5 questions about sources):
  [ ] User: who reads this, where, when, why?
  [ ] Brand: existing assets, named colors, voice?
  [ ] Content: what does it actually do? the one thing?
  [ ] Constraint: must-haves, must-not-haves?
  [ ] Reference: two sites you like, two you don't?

STAGE 2 — Generate 3 candidates (genuinely different directions):
  [ ] Candidate A: different visual logic, layout, voice
  [ ] Candidate B: different visual logic, layout, voice
  [ ] Candidate C: different visual logic, layout, voice
  (If all three share a structure, you haven't generated 3.)

STAGE 3 — Pick one with reasons tied to user's answers:
  [ ] Pick: ___
  [ ] Why this one: ___ (must reference user's answers)
  [ ] Why not the others: ___

STAGE 4 — Produce with annotations:
  [ ] Every design decision has a source comment
  [ ] Decisions you can't annotate get redone

STAGE 5 — Self-check (from 02-self-check.md):
  [ ] Run all heuristic questions
  [ ] Anything you can't answer → redo the decision
  [ ] Only deliver after self-check passes

For trivial output (under 5 design decisions), one shot is fine.
For non-trivial output, two shots minimum (rough → revised).
```
