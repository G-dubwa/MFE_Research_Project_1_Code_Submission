# Neural Hedging Research Project Code Submission

## Purpose

This folder is the code-submission package for the research project:

```text
Neural Network Architectures for Option Hedging:
Benchmarking under Black--Scholes and Extensions to Costs and Stochastic Volatility
```

It is a reproducibility package for the numerical experiments. It shows which
notebook to run, which source notebooks are executed, where outputs are saved,
and which CSV files support the report's main numerical claims.

This package is not intended to be a polished plotting package for the final
LaTeX report. Some final report figures may have been renamed, copied, or
manually selected for presentation. The authoritative reproducibility evidence is
the regenerated CSV files, executed notebooks, logs, and manifests in the run
folders.

## Files Included

```text
code_submission/
├── README.md
├── requirements.txt
├── 01_reproduce_report_results.ipynb
├── outputs/
│   ├── source_runs-20260624Tfinal-v7.zip
│   └── output_manifest_summary.csv
├── docs/
│   ├── RESULT_FILE_MAP.md
│   ├── PROTOCOL_SUMMARY.md
│   ├── PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md
│   ├── ARCHITECTURE_MULTI_SEED_APPENDIX.md
│   └── FINAL_CODE_SUBMISSION_AUDIT.md
└── notebooks/
    └── source/
        ├── architecture_selection_multiseed_protocol_matched.ipynb
        ├── ideal_minimal_task_hyperparameter_tuning_with_architectures.ipynb
        ├── final_benchmark_comparison.ipynb
        ├── parameter_robustness_study.ipynb
        ├── transaction_cost_neural_hedging_extension.ipynb
        └── heston_stock_option_neural_hedging_COS_obsvol_multiseed_corrected.ipynb
```

## Quick Start

For inspection without rerunning the long experiments:

1. Open `outputs/source_runs-20260624Tfinal-v7.zip`.
2. Inspect the six `source_runs/` folders.
3. Use `docs/RESULT_FILE_MAP.md` to find the CSVs supporting the main claims.
4. Use `docs/PROTOCOL_SUMMARY.md` and
   `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md` for protocol notes.
5. Use `outputs/output_manifest_summary.csv` for a complete file listing.


### Traceability note: architecture selection

The architecture-selection executed notebook saved its detailed run folder to Google Drive during execution. To keep the submitted package self-contained, this package includes `source_runs/01_architecture_selection/architecture_selection_metrics_from_executed_notebook.csv`, extracted from the executed notebook logs. This file makes the architecture-selection table traceable without requiring a multi-hour rerun.


## Training-Protocol Summary

The package does not use batch size 256 everywhere. The correct distinction is:

```text
Architecture selection and optional multi-seed architecture appendix: batch size 256.
Final selected-model retraining, parameter studies, transaction costs and Heston runs: usually batch size 4096.
```

This is documented in `docs/PROTOCOL_SUMMARY.md`.

## Parameter Robustness Source Patch

The standalone parameter-robustness source notebook is configured with `quick_run=False`, and the completed output archive includes the full report-grade robustness rerun outputs. See `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md`.

## Full Reproduction Instructions

1. Open `01_reproduce_report_results.ipynb` in Google Colab.
2. Set `Runtime > Change runtime type > GPU`.
3. Run all cells.
4. Authorize Google Drive if prompted.
5. Wait for the final output zip.
6. Inspect `source_runs/` or the final zip created by the notebook.

Google Drive saving is controlled inside the notebook. The default runner saves
outputs into an organised local runtime folder and, when enabled, into:

```text
MyDrive/MFE_neural_hedging_report_outputs/
```

## Expected Runtime and Hardware

Use a Colab GPU runtime. The full run is computationally expensive and may take
several hours on a Colab GPU. The submitted output zip is included so the
numerical evidence can be inspected without rerunning everything.

## Experiment Workflow

The runner executes the active source notebooks in this order:

1. `01_architecture_selection`
2. `02_black_scholes_final_benchmark`
3. `03_parameter_robustness_and_parameter_conditioning`
4. `04_transaction_costs`
5. `05_heston_fullinfo_true_vol`
6. `06_heston_observable_vol`

The Heston notebook is executed twice:

- full-information mode with `USE_OBSERVABLE_VOL = False`;
- observable-volatility mode with `USE_OBSERVABLE_VOL = True`.

Older Heston proxy notebooks, uncorrected Heston notebooks, and early prototype
notebooks are not part of the final runner workflow.

## Key Output Files and How They Map to the Report

See `docs/RESULT_FILE_MAP.md` for a truthful map based on the actual completed
run zip. See `docs/PROTOCOL_SUMMARY.md` and
`docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md` for the batch-size protocol and
parameter-robustness rerun note.

Important folders inside the completed zip:

- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/`
- `source_runs/03_parameter_robustness_and_parameter_conditioning/`
- `source_runs/04_transaction_costs/transaction_cost_outputs/`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/`

Some generated figure filenames differ from the final report figure filenames
because the report uses presentation-ready copies. The numerical CSV outputs are
the primary reproducibility evidence.

## Notes on Heston Pricing

In the Heston experiment, stock and variance paths are simulated under Heston
dynamics. The liquid hedging option is marked to model at each rebalancing date
using the Heston COS pricing routine.

The frozen-volatility Black--Scholes proxy is retained only as a diagnostic
because it creates a structural drift issue under Heston. Carr--Madan Fourier
pricing is used as an independent validation check for the COS implementation,
not as the pricing method used in the final hedge.

## Notes on Observable-Volatility Mode

Full-information mode gives the neural network direct access to the simulated
variance state `v_t/theta`.

Observable-volatility mode replaces direct access to `v_t` with a causal
realised-variance/EWMA proxy. The network still observes the contemporaneous
liquid-option quote `C_t^h/S_t`. That quote is available at the hedging date, so
this is not future-information leakage, but it carries implied information about
the latent variance state.

Observable-volatility mode should therefore be read as an
observable-market-information robustness check, not as a pure stock-return-only
volatility-filtering experiment.

## Notes on Reproducibility and Random Seeds

The source notebooks set seeds where practical. Exact bitwise reproducibility is
not guaranteed because GPU training and notebook execution can be nondeterministic.
Use approximate agreement with the reported headline values rather than expecting
identical floating-point output.

## Expected Headline Checks

After a successful full run, the regenerated CSVs should approximately support:

- Black--Scholes neural hedge RMSE near `0.00784`, close to BS delta and DT MSE benchmarks near `0.00781`.
- Parameter-conditioned hedger fixes the single-scenario generalization failure over the tested `K, sigma` grid.
- Transaction-cost cost-aware NN improves net RMSE and Loss CVaR95 relative to the cost-adjusted frictionless-delta benchmark at positive transaction costs.
- Heston full-information stock+option NN has RMSE near `0.00743` in the representative run.
- Heston full-information multi-seed stock+option NN beats the same-path BS-proxy Greek heuristic in `3/3` seeds, with average RMSE improvement near `22.7%`.
- Heston observable-volatility multi-seed stock+option NN beats the same-path BS-proxy Greek heuristic in `3/3` seeds, with average RMSE improvement near `26.6%`.

## What This Code Package Is Not

This package is not an Overleaf/LaTeX asset generator. It is a reproducibility
package showing how the numerical results were generated. Some final report
figures may have been renamed, copied, or manually selected for presentation.

## Troubleshooting

- If Colab disconnects, inspect the latest saved Google Drive folder and the
  partially completed `source_runs/` folder.
- If a section fails, inspect the executed notebook saved in that section folder.
- If Google Drive saving is slow, run with local output first, then download the
  final zip manually.
- If exact filenames differ from the LaTeX report, use
  `docs/RESULT_FILE_MAP.md` and `outputs/output_manifest_summary.csv` to trace
  the numerical source files.

## Optional appendix architecture multi-seed robustness run

The package includes an optional protocol-matched multi-seed architecture notebook:

```text
notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

It is intended only for an appendix robustness table. It should not replace the main architecture-selection table unless the report is deliberately rewritten around the new multi-seed evidence.

The important correction versus the first draft is that the batch size is `256`, matching the original architecture-selection experiment. The earlier `4096` setting gives far fewer optimiser updates and is not directly comparable to the original Table 1 protocol.

The master runner contains:

```python
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False
```

Set this to `True` only if you want to regenerate the appendix table. The completed output zip supplied with this package does not include newly rerun protocol-matched multi-seed outputs because the notebook is optional and expensive.
