# Research And Plan Review

Company: Bolt Threads
Project: `silkloop`

## Refined Thesis

Bio-material commercialization fails at scale-up unless batch variability, yield, and material properties are tied together.

The implementation is intentionally local and synthetic, but the test harness is shaped around the real operating question: can the proposed artifact create evidence a founder, CTO, or product leader would immediately recognize as useful?

## Fresh Sources Checked

- https://boltthreads.com/technology/mylo
- https://cfda.com/resources/materials-hub/materials-index/bolt-threads/
- https://www.gearpatrol.com/tech/a446046/bolt-threads-mylo-leather/

## Plan Excerpt Used

## The Gap

Bolt Projects' entire 2026 thesis rests on one number: **cost per gram of B-SILK at commercial titer**. Every public investor letter says "reduce the green premium." Yet a strain-optimization program with Ginkgo is fundamentally a **closed-loop search problem** — propose mutation set, ferment, measure titer, repeat — and Bolt has no public software backbone for it. The ingredient roadmap calls for a *third* Vegan Silk platform ingredient launching in 2026; that's a new protein design, a new strain, a new fermentation recipe, and a new application-performance fingerprint (film-forming on hair, sun-care emulsion stability, etc.) — all of which need to be tracked, queried, and *learned from* across batches. Today that knowledge lives in Slack threads and Benchling notebooks. The gap is a **strain-and-batch decision system** purpose-built for fermentation-derived cosmetic peptides — one that closes the loop between **sequence design → strain construct → fermentation run telemetry → downstream peptide QC → cosmetic application performance**. Without it, the "reduce the green premium" promise stays a slide.

## The Project — `silkloop`

> A closed-loop strain-and-batch decision system for fermentation-derived silk peptides: ingest fermentation telemetry + LC-MS QC + customer application data, recommend the next strain construct, and prove the recommendation with a back-tested learning curve.

**What it is.** A small, opinionated platform composed of (1) a typed data model for **construct → strain → fermentation run → harvest → peptide QC → application panel**, (2) a Bayesian-optimization recommender that proposes the next strain-construct + fermentation set-point pair, and (3) a "green-premium dashboard" that exposes one number — **dollars-per-functional-gram of B-SILK** — broken down into titer, yield, downstream losses, and application-equivalent silicone benchmark.

**Why it solves the gap.** Three concrete moves: (a) replaces ad-hoc Benchling tracking with a queryable graph of every B-SILK / XL-SILK construct lineage; (b) closes the loop with Ginkgo's strain-optimization output by ingesting their build-and-test results into the same data model; (c) turns the FY26 ingredient launch into a *learning curve you can show investors*, not a press release.

**The wow moment.** Open the dashboard. A single tile labelled **$/functional-gram** is sitting at, say, $42 today. Hover and see the 12-week history; click and see the four-component decomposition (titer 3.1 g/L · downstream yield 71% · application-equivalent silicone substitution ratio · raw media cost). Below it, a "next experiment" card: *"Construct C-2417 with feed strategy F-7; expected $/g = $31, 78% confidence; runs in 6 days."* Dan sees the company's investor narrative — "reduce the green premium" — turned into a number with a slope.

## Prototype Plan (the shippable demo)

**Surface:**
```bash
pip install silkloop
silkloop ingest benchling --token $TOK --project b-silk
silkloop ingest fermentation runs/*.csv
silkloop ingest lcms qc/*.mzML
silkloop recommend --objective dollars_per_functional_gram --budget 4_runs
silkloop serve  # web dashboard
```

**Demo inputs (synthetic-but-realistic):**
1. A 12-month history of 60 B-SILK fermentation runs across 11 constructs (simulated, with realistic noise).
2. Matched LC-MS QC traces showing the canonical B-SILK monomer + truncation peaks.
3. Application-panel results for film-former tape-pull on hair tresses (silicone benchmark = 100).
4. A Ginkgo strain-optimization CSV drop (~30 candidate constructs with predicted titers).
5. One real B-SILK product brief from the Freaks of Nature SPF launch ([businesswire](https://www.businesswire.com/news/home/20241022687469/en/)).

**Expected output / screen:** the green-premium tile starts at $42/g, the recommender proposes Construct C-2417 + Feed F-7, the back-test shows the same recommender would have hit FY26's projected $11M gross-profit margin two quarters earlier on historical data.

**Proof metrics:** (a) recommender's regret vs. greedy human-pick on the back-test; (b) ingestion latency for a 200MB fermentation run (<5s into DuckDB); (c) query latency for the $/g tile (<100ms warm).


## Build Acceptance Criteria

- Deterministic local fixtures.
- Domain-specific metrics and failure modes.
- Passing unit tests.
- Passing CLI verifier.
- Static dashboard generated locally.
- Benchmark output under the project `outputs/` folder.
- Public-safe README: no founder emails, no private outreach text, no credentials.
