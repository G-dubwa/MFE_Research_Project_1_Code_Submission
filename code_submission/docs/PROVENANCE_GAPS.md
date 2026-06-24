# Provenance Gaps To Resolve Before Final Report Submission

This repository is structurally clean and contains the completed output archive:

```text
code_submission/outputs/source_runs-20260624Tfinal-v7.zip
```

The archive supports the original single-seed architecture-selection trace, the
Black--Scholes final benchmark, the full parameter-robustness rerun, transaction
costs, and the Heston full-information / observable-volatility runs.

## Architecture Multi-Seed Evidence

The source notebook is present:

```text
code_submission/notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

However, the completed-output archive does not currently contain an executed
multi-seed architecture-selection output section such as:

```text
source_runs/01b_architecture_selection_multiseed_protocol_matched/
```

If the final report uses the three-seed architecture-selection table as the
active main architecture table, this is a provenance gap. The repository should
be updated with actual outputs from the executed notebook, including per-seed
CSV files, summary CSV files, `selection_result.json`, the executed notebook,
and an output manifest. These files must come from a real executed run, not from
manual transcription of report values.

Until those outputs are added, the included completed archive supports the
original single-seed architecture-selection result only. The multi-seed notebook
is reproducible source code, not completed evidence.

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

