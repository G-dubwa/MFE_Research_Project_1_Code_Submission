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
6. Rebuilt the completed-output archive as `outputs/source_runs-20260624Tfinal-v7.zip`.

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

The optional architecture multi-seed appendix notebook is included as supplementary evidence only and is disabled by default because it is computationally expensive. It should not replace the main architecture-selection table unless the report is deliberately rewritten around the appendix evidence.

If the report has been rewritten to use the protocol-matched three-seed
architecture-selection table as the active main architecture table, this package
needs one additional provenance update before final submission: add the actual
executed multi-seed outputs under
`source_runs/01b_architecture_selection_multiseed_protocol_matched/` in the
completed archive. The current archive contains the source notebook but not the
completed multi-seed evidence.
