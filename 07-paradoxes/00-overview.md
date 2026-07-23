# 07-paradoxes / 00 · Overview

> Read this after sections 01–06. The earlier sections are necessary but
> not sufficient. This section addresses the meta-problems that arise
> when the guide itself is applied at scale.

---

## The diagnosis

Sections 01–06 teach the agent to **derive every choice from a source**
instead of reaching for statistical defaults. That's the right principle.
But the principle has five failure modes that emerge only when you try
to apply it in practice:

1. **Second-order convergence** — "anti-AI taste" becomes a new AI taste.
2. **Hallucinated sources** — the agent fabricates justifications to satisfy the "name a source" rule.
3. **Thin-input dependency** — the framework assumes high-quality inputs that most users don't provide.
4. **Moving target** — model iteration makes surface-level tells obsolete; the guide conflates structural and surface tells.
5. **Philosophy-to-checklist gap** — the self-check collapses into formality ("did you use these words") instead of substance ("is the source real").

This section adds the defense-in-depth layer that addresses each.

---

## Why this layer exists

The earlier sections are the **preventive** layer: they shape how the
agent produces output. This section is the **meta** layer: it shapes
how the agent applies the preventive layer, and catches the failures
the preventive layer causes.

Without this layer, the guide is a sharp tool that cuts its user. An
agent following sections 01–06 literally will:

- Produce output that smells like "anti-AI" (a new, recognizable smell).
- Fabricate sources to satisfy the "name a source" rule.
- Either hallucinate user context when input is thin, or refuse to produce anything.
- Treat current-model surface tells as if they were eternal.
- Pass its own self-check by saying "yes I have a source" without verifying the source is real.

This layer exists to catch each of these.

---

## The five sub-layers

Read all five before applying the guide at scale:

1. **01-second-order-convergence.md** — the meta-paradox and its only real cure
2. **02-source-verification.md** — the three-tier source classification and the "cite or admit" protocol
3. **03-thin-input-protocol.md** — what to do when the user provides no sources
4. **04-structural-vs-surface.md** — which tells are architectural (stable) vs current-model (ephemeral)
5. (The fifth problem — philosophy-to-checklist gap — is addressed by rewriting the self-check in `05-workflow/02-self-check.md` to ask verifiable questions instead of yes/no questions.)

---

## How to read this layer

Each file has the same structure as the previous layers, plus one
addition: a **"how this fails if applied naively"** section that
describes the failure mode the file is addressing.

Read all five before delivering output that uses sources the user
didn't explicitly provide.
