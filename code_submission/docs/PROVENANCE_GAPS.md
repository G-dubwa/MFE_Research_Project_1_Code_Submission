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

## Resolved: architecture-selection multi-seed evidence

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

**Remaining caveat:** the included evidence is the per-seed and summary
CSV/JSON results of the multi-seed run. It does not include a separately
saved executed notebook or output manifest specific to this run (unlike the
other `source_runs/` sections, which each include an `executed_*.ipynb`
copy). If full executed-notebook provenance for this specific run is required,
rerun `architecture_selection_multiseed_protocol_matched.ipynb` (via
`RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = True` in the master runner, or
standalone) and add the executed notebook and manifest alongside the existing
CSV/JSON files.

## Parameter-Conditioned Table Consistency

The completed archive contains the parameter-conditioned robustness exports:

```text
source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness_with_extrapolation.csv
source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness_with_extrapolation.tex
```

If the final report table differs from these exports, use one source of truth:

- Preferred: update the report table to match the exported CSV/TeX values.
- Alternative: if a later executed notebook produced the report values, replace
  the CSV/TeX exports with outputs regenerated from that executed notebook and
  document the replacement in `RESULT_FILE_MAP.md`.

Do not leave the report and exported evidence disagreeing.

