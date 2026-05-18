# Biofabric Yield Twin Local

Offline fermentation and mycelium-material batch-yield simulator for biofabricated materials.

The useful claim is narrow and testable: Bio-material commercialization fails at scale-up unless batch variability, yield, and material properties are tied together. A batch twin explains why a beautiful lab sample will miss tensile targets at pilot scale.

## Failure model

Offline fermentation and mycelium-material batch-yield simulator for biofabricated materials.

## Measurement loop

- Builds 150 synthetic `biofabric batch` cases for the `silkloop` workflow, including clean and degraded paths.
- Grades `biofabric batch` runs on `yield_prediction`, `property_window_hit`, `scaleup_risk`, and `waste_reduction` so the pass/fail result has named evidence behind it.
- Exercises failure modes around `contamination_signal`, `tensile_miss`, `substrate_variance`, and `drying_curve_drift` instead of leaving those edge cases as prose.
- Materializes the `silkloop` review packet as JSON, dashboard HTML, benchmark output, and a portable demo bundle.

## Commands

```bash
uv sync --extra dev
uv run biofabric-twin init-demo --force
uv run biofabric-twin run-suite
uv run biofabric-twin verify
uv run biofabric-twin dashboard
uv run biofabric-twin benchmark --iterations 100
uv run biofabric-twin export-demo-pack
```

## Outputs

- `data/scenarios.json`
- `outputs/summary.json`
- `outputs/reports.json`
- `outputs/evidence_pack.md`
- `outputs/dashboard.html`
- `outputs/benchmark.json`
- `outputs/demo-pack.zip`

## Test path

```bash
uv run ruff check .
uv run pytest -q
uv run biofabric-twin run-suite
uv run biofabric-twin verify
uv run biofabric-twin benchmark --iterations 100
```

## Local-only contract

`Biofabric Yield Twin Local` checks in synthetic fixtures only. Runtime state, dashboards, caches, virtual environments, and generated packs stay out of git.
