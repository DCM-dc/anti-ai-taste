# 02-visual / 03 · Layout

## Default reflex

The canonical AI landing page grammar:

```
[Navbar: logo left, links right, CTA button far right]
[Hero: centered, H1 + sub + filled CTA + ghost CTA, 100vh, gradient bg]
[Social proof: 3–5 grayscale logos, "Trusted by"]
[Features: grid-cols-3, icon + title + 1-line description per card]
[How it works: 3 steps with numbered circles]
[Pricing: 3 plans, middle one elevated, rounded-2xl, green checks]
[Testimonials: 3 cards, 5 stars, headshot + name + title]
[FAQ: accordion]
[CTA banner: full-width gradient, "Start building today"]
[Footer: 4 columns — Product / Company / Resources / Legal]
```

Every section is full-width, vertically stacked, content centered.

## Why the reflex exists

This grammar appears in every shadcn/ui example, every Tailwind UI
screenshot, every Vercel template, every Lovable/v0/Bolt export. The model
pattern-matches on structure: "landing page" → this sequence. It's not
reasoning about what the content needs; it's retrieving the modal sequence.

The grammar is internally consistent and not always wrong — but it's
**always the same**. That consistency is the smell.

## Bad example (the default, annotated)

```html
<body>
  <nav class="flex justify-between items-center px-8 py-4">
    <!-- logo left, links right, CTA far right. The centroid nav. -->
  </nav>

  <section class="hero text-center py-32">
    <!-- 100vh, gradient bg, centered text. The centroid hero. -->
    <h1>Build the Future of Work</h1>
    <p>Supercharge your team's productivity with AI-powered workflows.</p>
    <div class="flex gap-4 justify-center">
      <button class="bg-indigo-600">Get Started</button>
      <button class="border border-indigo-600">Learn More</button>
    </div>
  </section>

  <section class="features grid grid-cols-3 gap-8 py-24">
    <!-- The centroid features. Three equal cards. -->
    <div class="rounded-2xl p-8 shadow-lg">
      <Icon name="Zap" />          <!-- ← Lucide Zap. The centroid icon. -->
      <h3>Fast</h3>
      <p>Lightning-fast performance.</p>
    </div>
    <div class="rounded-2xl p-8 shadow-lg">
      <Icon name="Shield" />       <!-- ← Lucide Shield. The centroid icon. -->
      <h3>Secure</h3>
      <p>Enterprise-grade security.</p>
    </div>
    <div class="rounded-2xl p-8 shadow-lg">
      <Icon name="Rocket" />       <!-- ← Lucide Rocket. The centroid icon. -->
      <h3>Scalable</h3>
      <p>Grows with your team.</p>
    </div>
  </section>

  <section class="pricing grid grid-cols-3 gap-8 py-24">
    <!-- The centroid pricing. Middle elevated. -->
    <div class="rounded-2xl p-8">Starter</div>
    <div class="rounded-2xl p-8 ring-2 ring-indigo-600 scale-105">Pro</div>
    <div class="rounded-2xl p-8">Enterprise</div>
  </section>

  <footer class="grid grid-cols-4 gap-8 py-16">
    <!-- The centroid footer. Four columns of links. -->
    <div>Product</div>
    <div>Company</div>
    <div>Resources</div>
    <div>Legal</div>
  </footer>
</body>
```

**Why this smells:**
- Every section is full-width and centered → no rhythm.
- Three equal feature cards → no hierarchy of importance.
- Three equal pricing plans with middle elevated → the model's first guess for pricing.
- Four-column footer → the model's first guess for footers.
- No section has been *omitted* → the model included every standard block whether needed or not.

## Good example (source-driven, annotated)

```html
<!--
  Source chain for this layout:
  Product  : a battery-monitoring tool for solar installers
  User     : field technician, on phone, in sun, wants the number
  Content  : 4 things actually matter:
               (a) the current battery voltage (live data)
               (b) the field tech's install list (work list)
               (c) recent alerts (chronological)
               (d) account / billing (low priority)

  Derivation:
  - No marketing hero. The user is paying; they don't need to be sold to.
    Replace hero with live dashboard.
  - No 3-card features. The product IS the feature; the dashboard is the features.
  - No "Trusted by" logo strip. Field techs don't care; remove entirely.
  - No pricing on the landing page. Pricing lives on /pricing.
  - No FAQ. Support lives in /docs and in chat.
  - Layout: dashboard-first, single column, data heavy.
    Asymmetric: live readout takes 7/12 width (most important),
    install list takes 5/12 (secondary), alerts below as full-width
    chronological log.
-->

<body>
  <nav>
    <!-- compact, left-aligned, no marketing CTA. Just product nav. -->
    [logo] [Dashboard] [Installs] [Alerts] [Account]
  </nav>

  <main class="grid grid-cols-12 gap-6">
    <!-- Live readout: 7 cols, the user's primary task -->
    <section class="col-span-12 lg:col-span-7">
      <BatteryReadout :install-id="current" />
    </section>

    <!-- Install list: 5 cols, secondary -->
    <aside class="col-span-12 lg:col-span-5">
      <InstallList />
    </aside>

    <!-- Alert log: 12 cols, chronological, not "cards" -->
    <section class="col-span-12">
      <AlertLog />
    </section>
  </main>

  <!-- No CTA banner. The user is already a customer. -->
  <!-- No footer columns. Just a single line: version, status, support email. -->
  <footer>
    v2.4.1 · status: ok · support@batterysolar.example
  </footer>
</body>
```

**Why this doesn't smell:**
- The default grammar was **omitted where it didn't fit** (no hero, no features, no social proof, no FAQ, no CTA banner, no 4-col footer).
- The grid is **asymmetric** (7/5), reflecting actual content weight.
- The decision to use a single column for alerts (not three cards) reflects that alerts are **chronological, not comparable**.
- Every section has a job; nothing is decorative.

## The grammar of omission

The most powerful de-AI move in layout is **removing sections**. The
default grammar includes every standard block whether the product needs
it or not. A real designer asks: *does this product need social proof?
Does it need an FAQ? Does it need a CTA banner?*

For a SaaS marketing page, maybe yes to all. For a field-tool dashboard,
no to all. For a personal portfolio, almost no to all. **The decision to
omit is louder than any decision to include.**

## Heuristic questions

Before producing the layout, answer:

1. **List the content blocks. What is the actual weight of each?**
   If three blocks have unequal weight, they should not be equal-width.
2. **Which standard sections did you omit, and why?**
   If you included every standard section, you've made no choices.
3. **Where is the visual center of gravity?**
   Default: the hero. Guided: wherever the content actually matters.
4. **Is the grid asymmetric anywhere?**
   If every grid is `grid-cols-3` or `grid-cols-4`, you've made no choices.
5. **Is anything full-bleed? Anything constrained?**
   Default: everything is full-width sections with centered content.
   Guided: some content breaks the grid, some is intentionally narrow.
6. **Does the layout match the content type?**
   - Marketing page → can have hero, features, pricing.
   - Dashboard → no hero, data-first.
   - Long-form essay → single narrow column, no cards.
   - Personal site → bento, not landing page.
7. **Could this layout appear in 1000 other AI outputs?**
   If yes, you've used the grammar unchanged. Break it.

## Anti-pattern: the asymmetric default

Banning `grid-cols-3` and reaching for `grid-cols-2` is not escaping the
default. Banning centered hero and reaching for left-aligned hero is not
escaping it either.

```
Bad:    "Don't use grid-cols-3, use grid-cols-2 instead."  ← still default
Good:   "These 7 content blocks have weights 5/3/2/4/1/2/3.
        I'll use a 12-col grid with col-spans 5,3,2,4,1,2,3
        because no two weights are equal."                 ← source-driven
```

The test: does your layout respond to the **specific** content, or could
the same layout fit any content?

## Instruction template

```
Design the page layout. Before producing, answer:

1. Content inventory:
   List every block the page will contain, with a 1–5 weight for each.
   Block 1: ___, weight __
   Block 2: ___, weight __
   ...

2. Standard sections to OMIT:
   [ ] Navbar with marketing CTA
   [ ] Centered hero
   [ ] Social proof logo strip
   [ ] 3-col features
   [ ] 3-step "how it works"
   [ ] 3-tier pricing
   [ ] Testimonials
   [ ] FAQ accordion
   [ ] CTA banner
   [ ] 4-col footer
   For each one you KEEP, justify why this product needs it.
   For each one you OMIT, the omission is a choice — note it.

3. Grid logic:
   If multiple blocks share a row, are their weights equal?
   If yes, justify. If no, use col-spans proportional to weight.

4. Reading path:
   Where does the eye start? Where does it go next?
   This determines visual hierarchy.

5. Could this layout be described as "[standard template] with [small tweak]"?
   If yes, the tweak is not enough. Rethink the structure.

Then produce the layout. Annotate each structural choice with its source.
```
