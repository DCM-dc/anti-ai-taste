# 08-genres / 03 · Technical documentation

## Scope

API references, SDK manuals, README files, user guides, runbooks,
internal technical docs.

This genre **inverts several universal rules**. Technical docs need
completeness, predictability, and procedural clarity — not rhythm,
fragments, or personality.

---

## Universal rules that apply directly

- **Language:** signature-word density ≤ 3 per 500 words (technical docs
  should be near 0).
- **Language:** no "not X but Y" reflex.
- **Rhetoric:** no decorative quotes.
- **Rhetoric:** no coined terms without lexical gap.

---

## Universal rules that INVERT for technical docs

### Inversion 1: NO fragments

The universal rhythm rule says "use fragments per 500 words." For
technical docs: **zero fragments**.

Technical docs must be complete sentences. Readers are scanning for
information; fragments create ambiguity.

```
✗ "Optional. Defaults to 80."  ← fragment; what's optional?
✓ "This parameter is optional and defaults to 80."
```

### Inversion 2: UNIFORM sentence length is OK

The universal rule says "vary sentence length, ratio ≥ 3." For
technical docs: **uniformity is fine, even preferred**.

Technical docs prioritize clarity over rhythm. A parameter description
that's 12 words, then one that's 14 words, then one that's 11 words —
that's fine. Readers aren't reading for music; they're scanning for facts.

### Inversion 3: TRANSITION WORDS are unnecessary

Technical docs don't need "furthermore" or "moreover." They need
**structure**: headers, lists, code blocks, tables. If the structure
is clear, transitions are noise.

### Inversion 4: SUMMARY at the end is OK (sometimes required)

The universal rule says "no summary at end." For technical docs:

- **Reference docs** (API, SDK): no summary. Each entry is standalone.
- **Tutorial / guide**: summary at end is OK if it crystallizes
  what was learned. But it must be **procedural recap**, not elevation.

```
✗ "In this tutorial, we've embarked on a transformative journey..."  ← elevation
✓ "You now have: a running server, a configured database, and a
   deployed endpoint. Next: [link to auth tutorial]."  ← procedural recap
```

### Inversion 5: SECOND PERSON is standard

The universal rule encourages first person ("I found," "we built").
For technical docs: **second person** ("you configure," "you run")
is standard and appropriate.

```
✓ "You configure the database URL in config.yaml."
✓ "Run npm install to install dependencies."
```

First person is OK in tutorial-style docs ("I'll walk you through..."),
but should be consistent within a section.

---

## Genre-specific rules

### Rule 1: Every parameter, every option, every edge case

Technical docs must be **complete**. If a function has 6 parameters,
document all 6 — even the obvious ones. If an error has 4 possible
causes, list all 4.

The universal rule "delete anything that doesn't carry information"
**inverts** here: in technical docs, completeness IS information.
Omitting a parameter because "it's obvious" is a bug.

### Rule 2: Code blocks for every code-relevant claim

If you describe an API, show the call. If you describe a config,
show the YAML. If you describe an error, show the message.

```
✗ "The endpoint returns a JSON object with the user's data."
✓ """
   The endpoint returns a JSON object with the user's data:

   ```json
   {
     "id": "usr_123",
     "email": "jane@example.com"
   }
   ```
   """
```

### Rule 3: Versioning and stability markers

Technical docs should mark versioning and stability:

```
✓ "Available since v2.3.0"
✓ "Deprecated in v3.0; use `newFunction()` instead"
✓ "Experimental; may change without notice"
```

### Rule 4: Cross-references are structural, not decorative

```
✗ "As mentioned earlier..."  ← vague
✓ "See [Authentication](/docs/auth) for how to get the API key."  ← specific link
```

### Rule 5: Examples must be runnable

If you show code, it should work. No pseudocode disguised as real code.
No `// TODO: implement this`. No `your-api-key-here` without explaining
where to get it.

---

## Genre-specific smells

### Smell 1: The "comprehensive" overview that says nothing

```
✗ "This comprehensive guide provides a detailed overview of the
   powerful features offered by our robust platform, empowering
   developers to build innovative solutions."
```

Signature words + zero information. Technical docs should start with
the first concrete action, not marketing copy.

### Smell 2: Missing error cases

```
✗ "Call the endpoint and it returns the user."
✓ "Call the endpoint. On success, returns 200 with user object.
   On 404, the user doesn't exist. On 401, your token is invalid.
   On 429, you're rate-limited; retry with exponential backoff."
```

### Smell 3: "Easy" and "simple"

```
✗ "Easy to use" / "Simply call..." / "Just add this line..."
```

If it were easy, you wouldn't need docs. These words signal that the
writer is hand-waving over complexity.

### Smell 4: Outdated examples

If the example shows v1 syntax but the library is on v3, the doc is
wrong. Technical docs need maintenance more than any other genre.

---

## Instruction template (technical-doc-specific)

```
Apply universal rules, plus these INVERSIONS:

FRAGMENTS: zero. Complete sentences only.
SENTENCE LENGTH: uniformity is fine. Clarity > rhythm.
TRANSITIONS: structural (headers, lists, links), not verbal.
SUMMARY: only in tutorials, only as procedural recap, never elevation.
PERSON: second person ("you configure") is standard.

GENRE RULES:
- Completeness: every parameter, every option, every edge case
- Code blocks for every code-relevant claim
- Versioning and stability markers
- Cross-references are specific links, not "as mentioned earlier"
- Examples must be runnable

GENRE SMELLS:
- No "comprehensive" / "robust" / "powerful" marketing copy
- No missing error cases
- No "easy" / "simple" / "just"
- No outdated examples (version-check before delivery)
```
