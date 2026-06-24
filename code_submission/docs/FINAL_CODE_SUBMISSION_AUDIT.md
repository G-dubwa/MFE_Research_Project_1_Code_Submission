# Final Code Submission Audit

This package is the cleaned final code-submission candidate after incorporating the completed full parameter-robustness rerun.

## Changes in this final version

1. Removed `.git`, `__MACOSX`, cache files, and stale assessment-irrelevant archive material.
2. Preserved the correct protocol distinction:
   - architecture selection / optional architecture multi-seed appendix: batch size 256;
   - final benchmark and extensions: larger experiment-specific budgets, typically batch size 4096.
3. Kept the optional protocol-matched architecture multi-seed notebook included but disabled by default in the master runner.
4. Ensured `notebooks/source/parameter_robustness_study.ipynb` is configured with `quick_run=False` by default.
5. Replaced the old parameter-robustness completed-output trace with the full rerun outputs from 24 June 2026.
6. Rebuilt the completed-output archive, now retained as `outputs/_archives/source_runs-20260624Tfinal-v7.zip`.
7. Extracted `source_runs-20260624Tfinal-v7.zip` into `outputs/source_runs/` and `arch_selection_results.zip` into `outputs/architecture_selection_multiseed/` so the marker can browse the result folders directly; moved both original zips into `outputs/_archives/` as backup copies.

## Parameter robustness verification

The full rerun output includes:

- `parameter_robustness_nn_vs_benchmarks.csv`
- `parameter_robustness_summary.csv`
- `parameter_robustness_table.tex`
- `robustness_rmse_vs_N.png`
- `robustness_ratio_vs_N.png`
- one training-history CSV per robustness scenario

The NN/DT RMSE ratio ranges from approximately 1.009 to 1.099, with mean approximately 1.049, matching the report's robustness narrative.

## Remaining caveat

The report uses the protocol-matched three-seed architecture-selection table as the active main architecture-selection table. The completed multi-seed evidence (per-seed CSVs, summary CSVs, `selection_result.json`) is included under `outputs/architecture_selection_multiseed/`, extracted from `outputs/_archives/arch_selection_results.zip`. The master runner's `RUN_ARCHITECTURE_MULTI_SEED_APPENDIX` flag remains `False` by default since this evidence does not need to be regenerated to inspect or grade it; set it to `True` only to independently rerun the three-seed notebook.

This evidence does not include a separately saved executed notebook or output manifest specific to this run (unlike the other completed-run sections). See the caveat in `docs/PROVENANCE_GAPS.md` if full executed-notebook provenance for this specific run is required.
