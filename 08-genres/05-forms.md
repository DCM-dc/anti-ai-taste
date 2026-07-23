# 08-genres / 05 · Forms & data entry

## Scope

Sign-up forms, surveys, registration forms, checkouts, intake forms,
application forms, questionnaires, multi-step wizards, settings panels.

This genre **inverts several universal rules**. Forms are tools, not
prose. Their job is to collect specific information with minimal
friction and maximal accuracy — not to express voice, rhythm, or
rhetorical strategy.

The most common AI-smell failure mode for forms: **applying marketing-page
or essay logic to a data-collection task.** A sign-up form is not a
landing page. It does not need a hero, a value prop, social proof, or
a conclusion. It needs fields, labels, validation, and a submit button.

---

## Universal rules that apply directly

- **Visual:** palette must be sourced (brand / domain / locale), not "modern."
- **Visual:** radius hierarchy, not one radius everywhere.
- **Visual:** one easing family per interaction class.
- **Language:** signature-word density ≤ 3 per 500 words (forms should be near 0).
- **Rhetoric:** no decorative quotes (a form intro is not a place to cite
  someone famous).
- **Rhetoric:** no coined concepts (forms describe fields, not paradigms).
- **Workflow:** task analysis before producing. Source the palette, the
  field grouping, the validation strategy.

---

## Universal rules that INVERT for forms

### Inversion 1: NO rhythm variation

The universal rhythm rule says "vary sentence length, include fragments."
For forms: **labels and helper text must be uniformly terse.**

Form text is not prose. It's signage. Uniformity aids scanning;
variation creates cognitive load.

```
✗ Labels: "Your full legal name" / "Email address, please" / "Phone?"
   ← inconsistent length, inconsistent register, one has a question mark

✓ Labels: "Full name" / "Email" / "Phone"
   ← uniform: noun phrase, no question mark, no please
```

The rhythm rules in `03-language/03-rhythm.md` **do not apply** to form
labels, helper text, button copy, or validation messages. They apply
only if the form has an introductory paragraph — and most forms
shouldn't have one.

### Inversion 2: NO first person

The universal rule encourages first person ("I," "we"). For forms:
**second person or imperative** is standard.

```
✗ "We'd love to know your name."   ← marketing register, wrong for a form
✓ "Enter your full name."           ← imperative, instructional
✓ "Full name"                       ← label, no verb needed
```

### Inversion 3: SUMMARY is forbidden

The universal rule says "no forced summary at end." For forms this
inverts harder: **no summary at all, ever.**

A "Thank you for completing our form! Your responses have been
recorded and will help us serve you better." page is the modal AI-smell
failure for this genre. After submit, show:

- What was submitted (the data, for confirmation)
- What happens next (specific: "You'll receive a confirmation email
  within 5 minutes" — not vague: "We'll be in touch soon")
- A way to go back or edit, if applicable

No uplift. No "we're excited to have you on board." No "thank you for
joining our community."

```
✗ "🎉 Thank you for registering! We're thrilled to have you join
   our community of innovators. Our team will review your application
   and reach out soon."

✓ "Registration received. Confirmation email sent to {email}.
   Decisions sent within 5 business days. [Edit responses] [Done]"
```

### Inversion 4: COMPLETENESS over deletion

The universal rule says "if you delete this, does anything lose? If no,
delete." For forms: **fields are not deletable based on aesthetic judgment.**

If the form needs to collect 12 fields, collect 12 fields. Don't reduce
to 6 to "feel cleaner." The universal rule applies to *decoration*
(gradients, icons, marketing copy) — not to *required data collection*.

The form's job is to gather what the requester needs. Cutting fields to
look minimal is a smell — it signals the producer prioritized aesthetics
over function.

### Inversion 5: STRUCTURE is the content

For prose, structure serves content. For forms, **structure IS the
content.** Field grouping, section ordering, conditional logic, and
step breaks are the form's information architecture.

Apply `02-visual/03-layout.md`'s layout rules **more strictly** for
forms than for marketing pages:

- Group related fields with visual hierarchy (section headers, dividers,
  spacing — not cards-with-shadows, which is the default AI form smell).
- Order fields by logical dependency, not by "what looks good."
- Use a single column for primary input fields. Multi-column forms are
  a known usability failure mode (NN/g research, lookup-verifiable) —
  Tier 2 source, not opinion.

---

## Genre-specific rules

### Rule 1: Labels above inputs, not as placeholders

Placeholder-as-label is the single most common AI default for forms.
It fails because:

- Placeholder disappears on focus, breaking the field's identity.
- Screen readers may not announce it as a label.
- It conflates "what this field is" with "example of what to type."

```
✗ <input placeholder="Email address" />

✓ <label for="email">Email</label>
   <input id="email" name="email" type="email"
          placeholder="you@example.com" />
```

The placeholder, if used, shows an *example*, not the *label*.

### Rule 2: Required-field marking must be explicit and consistent

Pick one convention and apply it everywhere:

- Asterisk after label ("Email *"), with a legend "Required fields marked
  with *" at the top, OR
- "Required" text in helper position, OR
- Bold label for required, regular for optional (with legend)

**Never** mark optional fields only (e.g., "(optional)" suffix) without
also marking required ones. This is the AI default and it's backwards
from user expectation — users assume unmarked = required.

### Rule 3: Validation is inline, specific, and immediate

```
✗ "Please enter a valid email."           ← what's valid?
✗ "Invalid input."                        ← which field? what's wrong?
✓ "Enter an email like name@domain.com."  ← shows the expected format

✗ Shown only on submit                    ← user fills 12 fields, then learns field 2 was wrong
✓ Shown on blur, after the user leaves the field
```

Validation messages must:

- Name the specific problem (not "invalid")
- Show the expected format (example, regex-implicit, or rule)
- Appear after the user has had a chance to enter correctly (on blur,
  not on every keystroke — that's hostile)

### Rule 4: Error states are not apologies

```
✗ "Oops! Something went wrong. Please try again."
✓ "Submission failed: the server returned a timeout. Your draft is
   saved. [Retry] [Save and exit]"
```

Errors state what happened, what the user's options are, and whether
their work is preserved. No exclamation marks. No "oops." No apologies
beyond a single "Sorry" at most, and only if the error is the system's
fault (not the user's).

### Rule 5: Button copy is the action, not the feeling

```
✗ "Submit"                    ← vague; submit what?
✗ "Continue"                  ← continue to what?
✗ "Get Started"               ← marketing register
✗ "Complete Your Registration" ← title case, breathless

✓ "Register"                  ← matches the form's purpose
✓ "Send application"          ← verb + object
✓ "Next: Payment"             ← tells the user where they're going
```

The button says what clicking it does. No "Let's go!" No "Join the
journey." The user is filling out a form, not embarking on an adventure.

### Rule 6: Multi-step forms show progress honestly

If a form has multiple steps, show:

- Current step number and total ("Step 2 of 4")
- A way to go back without losing data
- What the next step is (so the user can decide whether to continue now
  or later)

Do **not** show a progress bar that fills with a gradient animation on
advance. That's decoration. A static "2 of 4" with the step names is
more informative and less performative.

### Rule 7: No marketing chrome on a form

The default AI form lives inside a marketing-page shell: hero at top,
value prop, social proof, then the form, then a CTA banner below. For
a form whose purpose is data collection (not conversion marketing):

- No hero. The form is the page.
- No value prop paragraph. If the user is here, they know why.
- No "Trusted by" logo strip. Forms are not sales surfaces.
- No FAQ accordion below the form. Help lives on a help page or in
  inline helper text.

Exception: a sign-up form whose explicit purpose is conversion (not
data collection) may have minimal marketing context. But even then,
the form itself should not be wrapped in marketing chrome — the
marketing lives on the page before the form, not around it.

---

## Sources specific to forms

When sourcing form decisions, these are the Tier 2 (lookup-verifiable)
references:

| Decision | Reference | What it says (verify before citing) |
|---|---|---|
| Single-column layout | NN/g "Web Form Design" (Jarrett, 2008, updated) | Multi-column forms increase completion errors; single-column is the default recommendation |
| Label position (above input) | NN/g; WCAG 2.1 SC 1.3.1 | Labels above inputs are more scannable and more accessible than left-aligned or placeholder labels |
| Required-field marking | WCAG 2.1 SC 3.3.2 (Labels or Instructions) | Required fields must be programmatically determinable; visual marking must be consistent |
| Inline validation timing | NN/g "Inline Validation in Web Forms" (2009, still cited) | Validate on blur, not on submit; not on every keystroke |
| Error message specificity | WCAG 2.1 SC 3.3.1 (Error Identification) | Errors must identify the specific field and the specific problem |
| Autocomplete attributes | HTML5 spec; WCAG 2.1 SC 1.3.5 (Identify Input Purpose) | Use `autocomplete` for fields that map to standard user data (name, email, address) |
| Field type semantics | HTML5 spec | Use `type="email"`, `type="tel"`, `type="date"` etc. — they trigger correct mobile keyboards and native validation |

Cite the reference when you make the choice. "Single-column because
NN/g" is not enough — say "Single-column because multi-column forms
increase completion errors per NN/g research (Jarrett, 'Web Form
Design')." That's a Tier 2 source; the verifier can look it up in 30
seconds.

---

## Heuristic questions (form-specific)

1. **Did you apply marketing-page logic to a data-collection form?**
   If there's a hero, value prop, social proof, or CTA banner around the
   form, you did. Strip it.
2. **Are your labels above inputs, not as placeholders?**
   Placeholder-as-label is the modal AI default. Fix it.
3. **Is required-field marking explicit, consistent, and not
   optional-only?**
   If you mark optional fields but not required, you've inverted user
   expectation. Fix it.
4. **Are validation messages specific (not "invalid")?**
   Generic validation is an AI smell. Each message must name the problem
   and show the expected format.
5. **Does validation fire on blur, not on submit and not on keystroke?**
   Submit-only is hostile; keystroke is hostile. Blur is correct.
6. **Does the success page avoid uplift?**
   "Thank you for joining our community" is the smell. Replace with
   "Received. Next step: X. [Action]."
7. **Is button copy the action, not the feeling?**
   "Get Started" / "Join the journey" → "Register" / "Send application."
8. **Is the form single-column?**
   Multi-column for primary inputs is a known failure mode. Justify with
   a source if you deviate.
9. **Did you cite Tier 2 form-usability sources for structural choices?**
   NN/g, WCAG, HTML5 spec — these are 30-second-verifiable. If you
   claimed "best practice" without citing, that's affective.
10. **Did you apply `03-language/03-rhythm.md` to your labels?**
    If yes, you applied a rule that inverts for this genre. Form text
    is signage, not prose. Make it uniform.

---

## Instruction template

```
For form/data-entry tasks, after running task analysis:

LAYOUT (apply 02-visual/03-layout.md strictly):
  [ ] Single column for primary inputs (NN/g source)
  [ ] Labels above inputs, not placeholders (WCAG 1.3.1)
  [ ] Field grouping via hierarchy (headers, dividers, spacing) — not cards
  [ ] Order by logical dependency, not aesthetic

LABELS & COPY (apply 03-language/01-vocabulary.md; INVERT 03-rhythm.md):
  [ ] Uniform terse labels: noun phrase, no question mark, no "please"
  [ ] Imperative or second person, never first person plural
  [ ] Required marking: explicit, consistent, marks required not optional
  [ ] Button copy = the action ("Register"), not the feeling ("Get Started")

VALIDATION (genre-specific, no universal equivalent):
  [ ] Inline, on blur, specific ("Enter an email like name@domain.com")
  [ ] Error states: what happened + what user can do + is work saved
  [ ] Success state: what was received + what happens next + edit option
  [ ] No "thank you for joining our community" uplift

WHAT TO STRIP (forms are not marketing pages):
  [ ] No hero above the form
  [ ] No value prop paragraph
  [ ] No social proof / "trusted by"
  [ ] No CTA banner below
  [ ] No FAQ accordion (help goes inline or on a help page)

SOURCES TO CITE (Tier 2, 30-second verifiable):
  [ ] Single-column → NN/g "Web Form Design"
  [ ] Label position → WCAG 2.1 SC 1.3.1
  [ ] Required marking → WCAG 2.1 SC 3.3.2
  [ ] Validation timing → NN/g inline validation research
  [ ] Error specificity → WCAG 2.1 SC 3.3.1
  [ ] Autocomplete → WCAG 2.1 SC 1.3.5

SKIP (per README Task router):
  [ ] 04-rhetoric/* — forms don't quote, summarize, or coin concepts
  [ ] 03-language/03-rhythm.md — form text is signage, not prose
  [ ] 08-genres/01-marketing.md, 04-fiction.md — wrong genre
```
