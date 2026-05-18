# Biofabric Yield Twin Local

Offline fermentation and mycelium-material batch-yield simulator for biofabricated materials.

This is a local-first, synthetic-data prototype inspired by a company-specific project plan for **Bolt Threads**. It is built to demonstrate the engineering shape of `silkloop` without private data, credentials, external APIs, or hosted services.

## Why it matters

Bio-material commercialization fails at scale-up unless batch variability, yield, and material properties are tied together.

## What it does

- Generates deterministic synthetic `biofabric batch` scenarios.
- Scores each scenario against domain-specific quality gates.
- Produces evidence-backed findings for realistic failure modes.
- Writes a static dashboard, JSON reports, benchmark output, and a portable demo pack.
- Exposes a JSONL tool loop for local agent integration.

## Metrics

- `yield_prediction`
- `property_window_hit`
- `scaleup_risk`
- `waste_reduction`

## Failure modes

- `contamination_signal`
- `tensile_miss`
- `substrate_variance`
- `drying_curve_drift`

## Quickstart

```bash
uv sync --extra dev
uv run biofabric-twin init-demo --force
uv run biofabric-twin run-suite
uv run biofabric-twin verify
uv run biofabric-twin dashboard
uv run biofabric-twin benchmark --iterations 100
uv run biofabric-twin export-demo-pack
```

## Expected outputs

- `data/scenarios.json`
- `outputs/summary.json`
- `outputs/reports.json`
- `outputs/evidence_pack.md`
- `outputs/dashboard.html`
- `outputs/benchmark.json`
- `outputs/demo-pack.zip`

## Validation

```bash
uv run ruff check .
uv run pytest -q
uv run biofabric-twin run-suite
uv run biofabric-twin verify
uv run biofabric-twin benchmark --iterations 100
```

## Demo hook

A batch twin explains why a beautiful lab sample will miss tensile targets at pilot scale.
