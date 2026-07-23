# 08-genres / 01 · Marketing

## Scope

Landing pages, ads, sales copy, SaaS homepages, product pages, email
campaigns with conversion intent.

This is the genre the universal rules (`02-04`) were calibrated against.
Overrides are minimal — most rules apply directly.

---

## Universal rules that apply directly

- **Visual:** palette must have a source (brand / locale / content / user).
- **Visual:** typography must pair families with reasons.
- **Visual:** layout must match content weight; omit unneeded sections.
- **Language:** signature-word density ≤ 3 per 500 words.
- **Language:** sentence-length variance (not all 15–25 words).
- **Rhetoric:** no decorative quotes; no forced elevation; no coined terms.

These all apply. Marketing is where AI smell is strongest, so the
universal rules are most needed here.

---

## Genre-specific overrides

### Override 1: Marketing CAN use a hero

The universal layout rule (`02-visual/03-layout.md`) warns against the
"centered hero + 3-col features" grammar. For marketing, the hero
itself is not forbidden — **the default hero is forbidden**.

A marketing page can have a hero if:
- It's not centered H1 + sub + filled CTA + ghost CTA (the centroid)
- The hero carries information specific to this product (not "Build the future of work")
- The hero's visual logic is sourced (data-first, photo-first, quote-first — see `examples/landing-page-good.html`)

### Override 2: Marketing CAN use pricing tiers

The universal rule warns against "3-tier pricing with middle elevated."
For marketing, pricing is often legitimate. The rule is:

- Don't default to 3 tiers. Use the number of actual price points.
- Don't default to "middle elevated with green checks." If you elevate,
  source the elevation ("Pro is the most common plan for our user base").
- Consider alternatives: single price, slider, "contact for pricing,"
  comparison table without "elevation."

### Override 3: Marketing CAN have a CTA — but not forced elevation

Marketing pages end with a CTA. That's genre-appropriate. But:

- The CTA is functional ("Start a 14-day trial"), not elevating
  ("Start your journey today")
- The CTA follows the content, doesn't replace an ending
- No "Join thousands of teams" unless you can name them

### Override 4: Marketing copy CAN be punchy — but must be specific

Marketing allows shorter sentences, more fragments, more rhythm than
technical docs. But each punchy line must carry information:

```
✗ "Fast. Secure. Scalable."  ← three signature-word adjectives, zero information
✓ "4-second PR descriptions. SOC 2 Type II. 12-person team to 200."  ← three specific facts
```

---

## Genre-specific smells (in addition to universal tells)

### Smell 1: The "Trusted by" logo strip with fake logos

```
✗ "Trusted by ACME, GLOBEX, INITECH"  ← fictional companies
✓ "Used at: [3 real customer logos with links to case studies]"
✓ "No customers yet. Here's the demo."  ← honest
```

If you don't have real customers, don't fake social proof.

### Smell 2: "Most Popular" on the middle pricing tier

The middle tier is "Most Popular" in 90% of AI-generated pricing. If
it's actually popular, source it ("62% of paying users are on Pro").
If you don't know, don't claim it.

### Smell 3: Star ratings with no reviews

```
✗ "★★★★★ Rated 4.9/5 by 1000+ users"  ← unsourced number
✓ "★★★★★ 47 reviews on G2" (with link)
✓ (no rating if you don't have one)
```

### Smell 4: Feature lists with no differentiators

```
✗ "Fast, Secure, Scalable, Easy to use, Reliable"  ← applies to any product
✓ "Drift detection at 50mV, CAN bus polling at 5s, field notes per install"
```

If your features could describe any competitor, they're not features.

---

## Instruction template (marketing-specific)

```
Apply universal rules, plus:

HERO:
  - Can have a hero, but not the centered centroid hero
  - Hero must carry product-specific information
  - Hero visual logic must be sourced (data / photo / quote / etc.)

PRICING:
  - Number of tiers = actual number of price points (not default 3)
  - If elevating a tier, source the elevation
  - Consider alternatives (single price, slider, comparison table)

CTA:
  - Functional ("Start 14-day trial"), not elevating ("Start your journey")
  - Follows content, doesn't replace ending
  - No "Join thousands" without naming them

SOCIAL PROOF:
  - Real customers with links, or honest "no customers yet"
  - No fake logos, no unsourced numbers

FEATURES:
  - Each feature must be specific to this product
  - If it could describe any competitor, it's not a feature
  - Replace adjectives with facts
```
