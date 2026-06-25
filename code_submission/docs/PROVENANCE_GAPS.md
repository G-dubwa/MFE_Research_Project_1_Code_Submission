# Provenance Gaps and Status

This repository is structurally clean and contains the completed output archives:

```text
code_submission/outputs/_archives/source_runs-20260624Tfinal-v7.zip
code_submission/outputs/_archives/arch_selection_results.zip
```

extracted for inspection into `code_submission/outputs/source_runs/` and
`code_submission/outputs/architecture_selection_multiseed/` respectively.

The main archive supports the original single-seed architecture-selection
trace, the Black--Scholes final benchmark, the full parameter-robustness rerun,
transaction costs, and the Heston full-information / observable-volatility
runs.

## Architecture-Selection Provenance Note

The original completed output archive did not contain the three-seed
architecture-selection rerun. This has been resolved in the submitted package
by including the multi-seed evidence separately under:

```text
code_submission/outputs/architecture_selection_multiseed/
```

This folder contains the three per-seed CSVs (`seed_2026_results.csv`,
`seed_2027_results.csv`, `seed_2028_results.csv`), the numeric/formatted
summary CSVs (`multiseed_summary_numeric.csv`,
`multiseed_summary_formatted.csv`) and the selected-architecture JSON file
(`selection_result.json`). The source notebook is:

```text
code_submission/notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

The selected architecture, `shared_norm_64u_3L_tanh_sigmoid`, has the lowest
mean validation loss across the three seeds; the runner-up
(`shared_norm_32u_3L_tanh_sigmoid`) is close, so the report describes this as a
selected architecture rather than a dominant one.

The original zips are retained only as archive copies under:

```text
code_submission/outputs/_archives/
```

The included architecture-selection evidence is the submitted per-seed and
summary CSV/JSON results of the multi-seed run. The optional source notebook is
included and can be rerun if full executed-notebook provenance is required. The
submitted CSV and JSON files are the active evidence for the report's
architecture-selection table.

## Resolved: Parameter-Conditioned Table Consistency

The final report table for the parameter-conditioned hedger has been updated to
match the CSV values in:

```text
outputs/source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness_with_extrapolation.csv
```

Values are reported in the PDF rounded to six decimal places. The code
submission CSV remains the source of truth for the full-precision values.
