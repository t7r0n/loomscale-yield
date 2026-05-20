# Research And Plan Review

Project: Biofabric Yield Twin Local
Project: `silkloop`

## Refined Thesis

Bio-material commercialization fails at scale-up unless batch variability, yield, and material properties are tied together.

The implementation is intentionally local and synthetic, but the test harness is shaped around the real operating question: can the proposed artifact create evidence a founder, CTO, or product leader would immediately recognize as useful?

## Plan Excerpt Used

## The Gap

Biofabricated-material scale-up rests on one hard number: cost per gram at commercial titer. Strain optimization is fundamentally a closed-loop search problem: propose a mutation set, ferment, measure titer, repeat. New protein designs, strains, fermentation recipes, and application-performance fingerprints all need to be tracked, queried, and learned from across batches. The gap is a strain-and-batch decision system for fermentation-derived materials: one that closes the loop between sequence design, strain construct, fermentation telemetry, downstream QC, and application performance.

## The Project — `silkloop`

> A closed-loop strain-and-batch decision system for fermentation-derived silk peptides: ingest fermentation telemetry + LC-MS QC + customer application data, recommend the next strain construct, and prove the recommendation with a back-tested learning curve.

**What it is.** A small, opinionated platform composed of (1) a typed data model for construct, strain, fermentation run, harvest, peptide QC, and application panel, (2) a Bayesian-optimization recommender that proposes the next strain-construct plus fermentation set-point pair, and (3) a green-premium dashboard that exposes one number: dollars per functional gram, broken down into titer, yield, downstream losses, and application-equivalent benchmark.

**Why it solves the gap.** Three concrete moves: (a) replaces ad-hoc notebook tracking with a queryable graph of construct lineage; (b) closes the loop with strain-optimization output by ingesting build-and-test results into the same data model; (c) turns ingredient scale-up into a learning curve, not a press release.

**The wow moment.** Open the dashboard. A single tile labelled **$/functional-gram** is sitting at, say, $42 today. Hover and see the 12-week history; click and see the four-component decomposition: titer, downstream yield, application-equivalent substitution ratio, and raw media cost. Below it, a next-experiment card proposes a construct and feed strategy with expected cost, confidence, and turnaround time.

## Prototype Plan (the shippable demo)

**Surface:**
```bash
pip install silkloop
silkloop ingest notebook-export --path ./constructs
silkloop ingest fermentation runs/*.csv
silkloop ingest lcms qc/*.mzML
silkloop recommend --objective dollars_per_functional_gram --budget 4_runs
silkloop serve  # web dashboard
```

**Demo inputs (synthetic-but-realistic):**
1. A 12-month history of 60 fermentation runs across 11 constructs (simulated, with realistic noise).
2. Matched LC-MS QC traces showing canonical peptide monomer and truncation peaks.
3. Application-panel results for film-former tape-pull on hair tresses (silicone benchmark = 100).
4. A strain-optimization CSV drop with about 30 candidate constructs and predicted titers.
5. One synthetic product-brief fixture for application-performance targets.

**Expected output / screen:** the green-premium tile starts at $42/g, the recommender proposes Construct C-2417 + Feed F-7, and the back-test shows how much earlier the learning curve would have reached a margin target on historical data.

**Proof metrics:** (a) recommender's regret vs. greedy human-pick on the back-test; (b) ingestion latency for a 200MB fermentation run (<5s into DuckDB); (c) query latency for the $/g tile (<100ms warm).


## Build Acceptance Criteria

- Deterministic local fixtures.
- Domain-specific metrics and failure modes.
- Passing unit tests.
- Passing CLI verifier.
- Static dashboard generated locally.
- Benchmark output under the project `outputs/` folder.
- Public-safe README: no founder emails, no private outreach text, no credentials.
