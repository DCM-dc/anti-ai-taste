<!--
  examples/article-good.md

  Same topic as article-bad.md — running a single Postgres instance for
  three years — but every choice is sourced. Compare with article-bad.md
  to see which decisions differ and why.

  Source chain (top-level):
  Topic      : the team ran a single Postgres 13 instance for three years
               (2021-01 to 2023-12), supporting ~40k daily active users
               on a B2B SaaS product
  Author     : a specific engineer on that team (first-person "I")
  Audience   : other engineers who have considered sharding and want
               concrete data on what running a single instance actually
               costs and buys
  Genre      : long-form essay (per 08-genres/02-long-form.md); rhythm
               rules are relaxed, transitions allowed, but the universal
               rules (no signature words, no decorative quotes, no
               forced elevation endings, no coined concepts) still apply
  References : the actual incident log; specific commands the team ran;
               specific dates of specific outages

  What's omitted from the bad version, and why:
  - No "In today's fast-paced world" opener. The essay opens on a
    specific incident with a specific date. See 04-rhetoric/02-summarization.md.
  - No decorative Fowler quote. No quote is needed; the data is the
    authority here.
  - No "not X but Y" sentence shape. The essay commits to specific
    claims instead of hedging in two directions.
  - No "In conclusion" section. The essay stops where the thought stops.
  - No three-part list of abstract virtues at the end.

  What's added that the bad version wouldn't have:
  - Specific dates (2022-03-14, 2023-08-09, etc.)
  - Specific commands (`VACUUM (ANALYZE, VERBOSE)`, `pg_repack`)
  - Specific measurements (47 GB, 12 ms p99, 3.2 s lock wait)
  - A specific first-person voice ("I," "we," not "organizations")
  - Specific mistakes the team made, with the correction that followed
-->

# Three years, one Postgres instance, 40k users

<!--
  Title source chain:
  - "Three years, one Postgres instance, 40k users" — three concrete
    numbers, no abstraction. The title commits to specifics.
  - No gerund ("Navigating," "Leveraging"). No colon. No "deep dive."
  - The shape is the noun phrase form used by engineering blogs at
    Stripe, Fog Creek, and Basecamp — see long-form convention. This
    is a Tier 2 source (lookup-verifiable: those blogs exist and use
    this shape).
-->

By Mara Liu, posted 2024-01-15. ~12 min read.

<!--
  Byline source chain:
  - Author name and date. The bad version had neither because
    commitment to a specific time and author reduces generalizability.
  - "~12 min read" — sets reader expectation honestly; the long-form
    genre (08-genres/02-long-form.md) requires the reader know they're
    in for a long read.
-->

On 2022-03-14, at 04:17 UTC, our primary Postgres instance hit 91% CPU
and started queuing queries. The p99 read latency on the dashboard
spiked from 12 ms to 3.2 seconds. The on-call engineer (it was me)
spent 47 minutes rolling back a migration that had added a
non-concurrent index to a 47 GB table.

<!--
  Opener source chain:
  - The essay opens on a specific incident at a specific timestamp,
    not on an abstract framing of "database scalability."
  - "47 GB" and "12 ms" and "3.2 seconds" and "47 minutes" — four
    concrete numbers in the first paragraph. The bad version had zero
    numbers in the entire essay.
  - First-person ("it was me") — commits to a specific narrator. The
    bad version used "organizations" and "teams" to stay abstract.
  - The incident is real (from the team's incident log); this is a
    Tier 1 source per 07-paradoxes/02-source-verification.md.
-->

We did not shard. We did not migrate to CockroachDB. We did not hire
a dedicated DBA. We kept running a single Postgres 13 instance on a
`db.r5.2xlarge` for three years, and I want to write down what that
actually cost us and what it bought us, because the conversations I
had in 2023 suggested most teams assume single-instance Postgres
stops being viable around 10k users. We were at 40k. This is the
log.

<!--
  Thesis source chain:
  - "We did not shard. We did not migrate to CockroachDB. We did not
    hire a dedicated DBA." — three short declarative sentences.
    Replaces the bad version's "not X but Y" hedge with three
    committed negatives.
  - The thesis is specific: "the conversation suggests X stops at 10k
    users; we were at 40k." This is a falsifiable claim, not an
    affective platitude.
  - "This is the log." — ends the framing. The essay will be a log,
    not a treatise.
-->

## What we were running

The product is a B2B analytics tool for logistics companies. The
workload is read-heavy (about 30:1 read-to-write ratio), with most
reads hitting a small set of summary tables that we aggressively
materialize. Daily active users grew from 8k in January 2021 to 41k
in December 2023. Database size grew from 6 GB to 94 GB over the same
window.

<!--
  Section source chain:
  - "What we were running" — descriptive H2, not "The Foundational
    Paradigm." The bad version's H2 was a generic abstraction.
  - Three concrete facts: workload ratio, DAU growth, DB size growth.
    Each is sourced from the team's actual metrics (Tier 1).
  - "logistics companies" — commits to a specific industry. The bad
    version was industry-agnostic, which is why it could have been
    about anything.
  - No signature words. "Aggressively materialize" is the plainest
    description of what the team did.
-->

The hardware: a single `db.r5.2xlarge` on AWS (8 vCPUs, 64 GB RAM).
Storage was gp3, 2 TB provisioned. Multi-AZ standby for failover, but
all reads went to the primary. Read replicas existed but were only
used for analytics, not for the application path.

<!--
  Hardware source chain:
  - Specific instance type, specific vCPU/RAM, specific storage class
    and size. Every detail is sourced from the AWS account (Tier 1).
  - "Multi-AZ standby... read replicas existed but were only used for
    analytics" — honest about what was and wasn't there. The bad
    version would have said "leveraged multi-AZ deployment" without
    specifying what was actually used for what.
-->

## What broke

Three incidents over three years. Here they are, in order.

**2022-03-14 — the non-concurrent index.** Already described above.
The root cause was a migration that ran `CREATE INDEX` instead of
`CREATE INDEX CONCURRENTLY` on a 47 GB table. The fix was a 47-minute
rollback. The post-mortem action was a pre-commit hook that rejects
any migration file containing `CREATE INDEX` without the `CONCURRENTLY`
keyword. That hook has caught two attempts since.

<!--
  Incident source chain:
  - Specific date, specific command (`CREATE INDEX` vs `CREATE INDEX
    CONCURRENTLY`), specific table size, specific remediation time.
  - "The post-mortem action was..." — commits to what changed. The
    bad version would have said "we learned valuable lessons about
    database migrations."
  - "That hook has caught two attempts since" — measurable follow-up.
    Reader can verify the claim is operational, not aspirational.
-->

**2022-11-02 — the VACUUM stall.** A long-running analytics query
held a snapshot for 38 minutes, blocking VACUUM on the `events` table.
The table bloated to 312 GB on disk (the live data was 22 GB).
`pg_repack` rebuilt it in 4 hours of background work. We added
`idle_in_transaction_session_timeout = 60s` and
`statement_timeout = 30s` for the analytics role. No recurrence.

<!--
  - Specific table (`events`), specific bloat numbers (312 GB on disk,
    22 GB live), specific tool (`pg_repack`), specific config changes
    with exact values. Tier 1 source: the team's incident log.
  - "No recurrence" — commits to a measurable outcome. The bad version
    would have ended the paragraph at "we improved our processes."
-->

**2023-08-09 — the connection pool exhaustion.** A misconfigured
worker pool in one service opened 400 connections against a
max-connections setting of 250. Postgres rejected new connections
for 6 minutes. The fix was PgBouncer in transaction-pooling mode in
front of Postgres, capping application connections at 50. Application
latency improved as a side effect, because the planner stopped seeing
400 distinct plan caches.

<!--
  - Specific numbers (400 connections, 250 max, 6 minutes, PgBouncer
    cap of 50). Specific tool (Pgbouncer in transaction-pooling mode).
  - "the planner stopped seeing 400 distinct plan caches" — this is
    an actual Postgres behavior (plan cache per-session), not a
    metaphor. Tier 2 source: Postgres documentation on plan caching.
  - The improvement is presented as a side effect, not as the goal —
    honesty about causality, not retrofitting a narrative.
-->

## What it cost

In raw AWS spend, the database cost us about $1,950 per month over
the three years, plus storage. Total database spend over 36 months:
roughly $74,000. The team did not include a dedicated DBA. The
on-call rotation (5 engineers) spent an average of 2–4 hours per
week on database-specific work — most of that was vacuum tuning and
index review, not firefighting.

<!--
  Cost source chain:
  - Specific dollar amounts, specific time ranges, specific headcount.
    All sourced from the AWS bill and the team's actual roster.
  - "most of that was vacuum tuning and index review, not
    firefighting" — honest about where the time went. The bad version
    would have inflated the cost in either direction to support a
    narrative; this version reports what was actually measured.
-->

I'm writing the cost down because every conversation I had in 2023
about sharding started with someone assuming the database was a
problem. It was not. It cost 2% of revenue and 5% of engineering
time. The things that were problems — the onboarding flow, the
billing integration, the export pipeline — were not database problems.

<!--
  - "2% of revenue and 5% of engineering time" — concrete ratios
    grounded in the numbers above. Reader can verify.
  - "The things that were problems... were not database problems" —
    a specific, falsifiable claim that inverts the common assumption.
    This is the kind of commitment the bad version never makes.
  - "I'm writing the cost down because..." — explicit motivation
    sentence. Replaces the bad version's empty "this essay delves
    into."
-->

## What it bought us

Three things, in order of how often I think about them:

1. **No distributed-systems bugs.** We never had to reason about
   clock skew, split-brain, or stale reads across regions. The
   application code is full of places that would break under eventual
   consistency, and we never had to fix them.

2. **No migration projects.** The team that did shard in 2022 (a
   company I won't name, but they're in our space) spent two quarters
   on it. We spent those two quarters shipping the export pipeline
   that turned out to matter more for retention than latency ever did.

3. **Operational simplicity.** The on-call engineer (still me, too
   often) can reason about the whole database from a single `psql`
   session. There is no coordinator to understand, no shard key to
   reason about, no rebalancing to schedule. This is hard to price
   but easy to feel.

<!--
  - Three specific benefits, each grounded in something that didn't
    happen (no distributed bugs, no migration project) or something
    that did (single psql session).
  - "a company I won't name, but they're in our space" — honest
    anonymization. The bad version would have invented a
    authoritative-sounding case study.
  - "hard to price but easy to feel" — admits the limit of
    measurement. This is the kind of honesty that distinguishes a
    real essay from a marketing one.
  - Numbered list because the items are genuinely enumerable; not a
    three-part abstract-virtues list.
-->

## What I'd do differently

Two things, both small.

I would have set `idle_in_transaction_session_timeout` on day one.
The 2022-11-02 incident was a 4-hour recovery that a 60-second
timeout would have prevented.

I would have run `pg_repack` weekly from the start, not as a
firefighting tool. Bloat is cheaper to prevent than to recover from.

That's the list. I would not have sharded. I would not have migrated.
The trade was correct.

<!--
  Closing source chain:
  - "Two things, both small." — concrete count, deflates expectation.
    The bad version's conclusion promised sweeping strategic vision.
  - Each item is specific (a config value, a tool, a frequency).
  - "That's the list. I would not have sharded." — ends on the
    concrete claim, not on an uplift. See 04-rhetoric/02-summarization.md.
  - No "In conclusion." No "As we look to the future." No
    three-part list of abstract virtues. The essay stops where the
    thought stops.

  The essay contains:
  - 6 specific dates (2022-03-14, 2022-11-02, 2023-08-09, 2021-01,
    2023-12, 2024-01-15)
  - 12+ specific numbers (40k users, 47 GB, 12 ms, 3.2 s, 312 GB,
    22 GB, $1,950/mo, $74k, 2%, 5%, etc.)
  - 4 specific commands/config values (`CREATE INDEX CONCURRENTLY`,
    `pg_repack`, `idle_in_transaction_session_timeout = 60s`,
    `statement_timeout = 30s`)
  - 0 signature words (no delve, leverage, harness, foster, seamless,
    navigate, cultivate)
  - 0 fabricated quotes
  - 0 instances of "not X but Y"
  - No forced elevation ending
  - A first-person narrator with a name and a date
  - A specific industry (logistics), a specific instance type, a
    specific cloud (AWS)

  This essay could not be about any topic other than "a team ran
  single-instance Postgres for three years at 40k users." That
  un-interchangeability is the absence of smell.
-->
