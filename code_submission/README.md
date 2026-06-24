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

## Report files

This repository is the code-submission package only. It does not contain the LaTeX report source or Overleaf project files. The report is submitted separately. Some final report figures may have been renamed, copied, or manually selected for presentation; the primary reproducibility evidence here is the source notebooks, executed run folders, CSV outputs, logs, manifests and documentation.

## Files Included

```text
code_submission/
├── README.md
├── requirements.txt
├── 01_reproduce_report_results.ipynb
├── outputs/
│   ├── README.md
│   ├── output_manifest_summary.csv
│   ├── source_runs/
│   │   ├── 01_architecture_selection/
│   │   ├── 02_black_scholes_final_benchmark/
│   │   ├── 03_parameter_robustness_and_parameter_conditioning/
│   │   ├── 04_transaction_costs/
│   │   ├── 05_heston_fullinfo_true_vol/
│   │   └── 06_heston_observable_vol/
│   ├── architecture_selection_multiseed/
│   │   ├── seed_2026_results.csv
│   │   ├── seed_2027_results.csv
│   │   ├── seed_2028_results.csv
│   │   ├── multiseed_summary_numeric.csv
│   │   ├── multiseed_summary_formatted.csv
│   │   └── selection_result.json
│   └── _archives/
│       ├── source_runs-20260624Tfinal-v7.zip
│       └── arch_selection_results.zip
├── docs/
│   ├── RESULT_FILE_MAP.md
│   ├── PROTOCOL_SUMMARY.md
│   ├── PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md
│   ├── ARCHITECTURE_MULTI_SEED_APPENDIX.md
│   ├── PROVENANCE_GAPS.md
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

1. Open `outputs/source_runs/`.
2. Inspect the extracted source-run folders.
3. Use `outputs/architecture_selection_multiseed/` for the three-seed architecture-selection evidence.
4. Use `docs/RESULT_FILE_MAP.md` to find the CSVs supporting each main report claim.
5. Use `docs/PROTOCOL_SUMMARY.md` and `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md` for protocol notes.
6. Use `outputs/output_manifest_summary.csv` as a file index.
7. Original zip archives are stored as backup copies in `outputs/_archives/`.


### Traceability note: architecture selection

The report's active architecture-selection table uses the three-seed, twelve-candidate architecture-selection rerun. The supporting evidence is included in:

```text
outputs/architecture_selection_multiseed/
```

This folder contains the per-seed and summary files:

```text
seed_2026_results.csv
seed_2027_results.csv
seed_2028_results.csv
multiseed_summary_numeric.csv
multiseed_summary_formatted.csv
selection_result.json
```

The selected architecture is the shared normalised `64x3` tanh/sigmoid MLP, chosen by lowest mean validation loss across three independent seeds (2026, 2027, 2028) at batch size 256. The completed source-run archive (`source_runs-20260624Tfinal-v7.zip`) was generated before this three-seed evidence was added, so the multi-seed architecture evidence is supplied separately under `outputs/architecture_selection_multiseed/` rather than inside `outputs/source_runs/01_architecture_selection/`.

The runner notebook also contains the optional source notebook `architecture_selection_multiseed_protocol_matched.ipynb`, but the expensive multi-seed rerun is disabled by default (`RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False`). The submitted CSV/JSON files under `outputs/architecture_selection_multiseed/` are the primary evidence for the architecture-selection table unless the optional multi-seed notebook is explicitly rerun.

The original single-seed architecture-selection trace remains available at `outputs/source_runs/01_architecture_selection/architecture_selection_metrics_from_executed_notebook.csv` for reference, but it is no longer the active selection evidence.


## Training-Protocol Summary

The package does not use batch size 256 everywhere. The correct distinction is:

```text
Architecture selection and optional multi-seed architecture appendix: batch size 256.
Final selected-model retraining, parameter studies, transaction costs and Heston runs: usually batch size 4096.
```

This is documented in `docs/PROTOCOL_SUMMARY.md`.

## Parameter Robustness Source Patch

The standalone parameter-robustness source notebook is configured with `quick_run=False`, and the completed output archive includes the full report-grade robustness rerun outputs. See `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md`.

## Running in Google Colab

The submitted package includes completed outputs, so rerunning is optional. If rerunning, use a GPU runtime.

The orchestration notebook `01_reproduce_report_results.ipynb` exposes its controls in the first code cell (`# 0. User controls`). The actual flag names in that cell are:

```python
RUN_MODE = "full_generation"  # "full_generation", "smoke", or "extract_only"
RUN_ARCHITECTURE_SELECTION = True
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False  # optional appendix robustness run; expensive
RUN_BLACK_SCHOLES_FINAL = True
RUN_PARAMETER_ROBUSTNESS = True
RUN_TRANSACTION_COSTS = True
RUN_HESTON_FULLINFO = True
RUN_HESTON_OBSVOL = True
GLOBAL_SMOKE_MODE = (RUN_MODE == "smoke")
```

`GLOBAL_SMOKE_MODE` is derived from `RUN_MODE` and is propagated into each source notebook's own quick-run flag. In smoke mode, the runner patches available quick-run flags in the source notebooks, including the Black--Scholes final benchmark `quick_run` flag, parameter robustness `quick_run`, transaction-cost `RUN_FULL`, and Heston `RUN_FULL` / `RUN_MULTI_SEED_HEADLINE` flags. Where a source notebook exposes a quick/smoke flag, smoke mode also collapses any internal multi-seed loop to a single representative seed (for example, the Heston notebook's `RUN_MULTI_SEED_HEADLINE` and the architecture-selection notebook's single `GLOBAL_SEED`).

### Recommended smoke test

Use this when you only want to check that the orchestration pipeline does not break.

1. Upload or open the code submission folder in Google Drive.
2. Open `code_submission/01_reproduce_report_results.ipynb` in Google Colab.
3. Set `Runtime > Change runtime type > GPU`.
4. In the first code cell, set:

```python
RUN_MODE = "smoke"
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False
```

5. Run all cells.
6. Confirm that the notebook creates a new output folder/zip and that each enabled section completes without path or import errors.

The smoke test is not expected to reproduce the final report numbers exactly. It is only a pipeline-integrity check. For submission checking, a one-seed smoke test is sufficient to verify that the orchestration notebook, paths, imports and output-saving logic work. It should not be treated as a replacement for the submitted full-result evidence. The report-grade evidence is the completed extracted output folders under `outputs/source_runs/` plus the three-seed architecture evidence under `outputs/architecture_selection_multiseed/`.

### Full rerun

Use this only if you want to regenerate report-grade outputs.

```python
RUN_MODE = "full_generation"
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False
```

The full run is computationally expensive and may take several hours on a Colab GPU. Exact bitwise reproducibility is not guaranteed because GPU training and notebook execution can be nondeterministic. Use approximate agreement with the reported headline values, not exact figures.

### Optional architecture multi-seed rerun

The multi-seed architecture-selection evidence used in the report is already supplied under:

```text
outputs/architecture_selection_multiseed/
```

Only set:

```python
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = True
```

if you deliberately want to regenerate the three-seed architecture-selection run. This is not required for a normal smoke test, and the rerun will not necessarily reproduce the submitted CSV/JSON values exactly (see the reproducibility note below).

### Reproduction mechanics

1. Open `01_reproduce_report_results.ipynb` in Google Colab.
2. Set `Runtime > Change runtime type > GPU`.
3. Set the controls in the first code cell as described above.
4. Run all cells.
5. Authorize Google Drive if prompted.
6. Wait for the final output zip.
7. Inspect `source_runs/` or the final zip created by the notebook.

Google Drive saving is controlled inside the notebook. The default runner saves
outputs into an organised local runtime folder and, when enabled, into:

```text
MyDrive/MFE_neural_hedging_report_outputs/
```

## Expected Runtime and Hardware

Use a Colab GPU runtime. The full run is computationally expensive and may take
several hours on a Colab GPU. The submitted output evidence is included so the
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

See `docs/RESULT_FILE_MAP.md` for a truthful map based on the extracted output
folders. See `docs/PROTOCOL_SUMMARY.md` and
`docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md` for the batch-size protocol and
parameter-robustness rerun note. See `docs/PROVENANCE_GAPS.md` for the
provenance status of the architecture-selection evidence and any other
report/package consistency notes.

Important folders inside `outputs/`:

- `outputs/architecture_selection_multiseed/`
- `outputs/source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/`
- `outputs/source_runs/03_parameter_robustness_and_parameter_conditioning/`
- `outputs/source_runs/04_transaction_costs/transaction_cost_outputs/`
- `outputs/source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/`
- `outputs/source_runs/06_heston_observable_vol/heston_delta_vega_outputs/`

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

## Architecture multi-seed source notebook

The package includes the source notebook used to produce the three-seed architecture-selection evidence:

```text
notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

The completed evidence from running this notebook is already included under `outputs/architecture_selection_multiseed/` (see the traceability note above) and is the active architecture-selection evidence for the report.

The important correction versus an earlier draft is that the batch size is `256`, matching the original architecture-selection experiment. An earlier `4096` setting gave far fewer optimiser updates and was not directly comparable to the original Table 1 protocol.

The master runner contains:

```python
RUN_ARCHITECTURE_MULTI_SEED_APPENDIX = False
```

This remains the default because the supplied `outputs/architecture_selection_multiseed/` evidence already covers the architecture-selection table; rerunning through the master runner is only needed if you want to independently regenerate that evidence. Set this to `True` only if you deliberately want to do so. A fresh rerun will not necessarily reproduce the submitted CSV/JSON values exactly, since GPU training is not bitwise-deterministic.
