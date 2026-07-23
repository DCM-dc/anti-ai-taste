# 08-genres / 00 · Overview

> Sections 02–04 give universal rules. This section gives **genre-specific
> overrides**. Different content types have different defaults, different
> acceptable moves, different smells. One-size-fits-all is wrong.

---

## The diagnosis

The universal rules in `02-visual/`, `03-language/`, `04-rhetoric/` were
calibrated against **marketing pages and blog posts** — the dominant
genres in AI training data. Applied unchanged to other genres, they
produce wrong output:

- **Technical documentation** needs completeness, predictability, no fragments.
  The rhythm rules ("use fragments, vary length") would make API docs unreadable.
- **Long-form essays** need sustained paragraphs, developed arguments.
  The "no summary at end" rule is right; the "no transition words" rule is wrong.
- **Marketing copy** is where the universal rules apply most directly —
  but even here, genre conventions differ (B2B vs B2C, enterprise vs consumer).
- **Fiction** needs voice, dialogue, sensory detail. The "no coined terms"
  rule is wrong for fiction (genres like sci-fi and fantasy require coinage).

The universal rules are a **default**. Each genre has **overrides** that
relax, tighten, or invert specific rules.

---

## The five genres covered

1. **Marketing** (`01-marketing.md`) — landing pages, ads, sales copy.
   The universal rules apply most directly. Overrides are minimal.
2. **Long-form** (`02-long-form.md`) — essays, journalism, blog posts
   > 1500 words. Overrides: relax rhythm rules, allow transitions.
3. **Technical documentation** (`03-technical-doc.md`) — API references,
   manuals, READMEs. Overrides: invert rhythm rules, require completeness.
4. **Fiction** (`04-fiction.md`) — short stories, novels, narrative.
   Overrides: relax coinage rules, require sensory detail, allow voice extremes.
5. **Forms & data entry** (`05-forms.md`) — sign-up, survey, registration,
   checkout, intake, settings. Overrides: invert rhythm rules (uniform
   terse labels), forbid summary, strip marketing chrome, require Tier 2
   usability sourcing (NN/g, WCAG).

---

## How to use this layer

1. **Identify the genre** before producing. If unclear, ask the user.
2. **Read the matching genre file** end-to-end.
3. **Apply the universal rules** (`02-04`) as defaults.
4. **Apply the genre overrides** — these take precedence.
5. **Run the self-check** with genre-aware questions.

If the output spans genres (e.g., a marketing page with a long-form blog
section), apply different rules to different sections. Document the
boundary.

---

## The genre detection rule

If the user doesn't specify genre, infer from the prompt:

| Prompt signal | Genre |
|---|---|
| "landing page," "SaaS," "convert," "pricing" | Marketing |
| "article," "essay," "blog post," "write about X" | Long-form |
| "API docs," "README," "manual," "how to use X" | Technical doc |
| "story," "novel," "narrative," "character" | Fiction |
| "form," "sign up," "survey," "register," "checkout," "intake" | Forms & data entry |
| "report," "analysis," "whitepaper" | Long-form (with technical-doc overrides for data sections) |

If ambiguous, ask: "Is this marketing, long-form, technical documentation,
fiction, or a form? The rules differ."

---

## What this layer does NOT cover

- **Academic papers** — partial coverage in long-form; citation conventions
  need their own treatment (future work).
- **Legal/contractual text** — out of scope; precision conventions are
  domain-specific.
- **Poetry** — out of scope; rules don't apply.
- **Children's content** — partial; needs developmental considerations
  not covered here.
- **Multimedia scripts** (video, podcast) — acknowledged as gap; see README.

Read the matching genre file before producing.
