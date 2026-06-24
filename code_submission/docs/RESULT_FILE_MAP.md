# Result File Map

## Quick Report Evidence Map

| Report area | Primary evidence location |
|---|---|
| Architecture selection table | `outputs/architecture_selection_multiseed/multiseed_summary_numeric.csv` and `outputs/architecture_selection_multiseed/selection_result.json` |
| Per-seed architecture-selection results | `outputs/architecture_selection_multiseed/seed_2026_results.csv`, `seed_2027_results.csv`, `seed_2028_results.csv` |
| Black--Scholes final benchmark | `outputs/source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/` |
| Parameter robustness and parameter-conditioned hedger | `outputs/source_runs/03_parameter_robustness_and_parameter_conditioning/` |
| Transaction costs | `outputs/source_runs/04_transaction_costs/transaction_cost_outputs/` |
| Heston full-information COS experiment | `outputs/source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/` |
| Heston observable-volatility experiment | `outputs/source_runs/06_heston_observable_vol/heston_delta_vega_outputs/` |
| Archived copies of original zips | `outputs/_archives/` |

This map is based on the extracted output folders under `outputs/source_runs/` and `outputs/architecture_selection_multiseed/` (originally packaged as `outputs/_archives/source_runs-20260624Tfinal-v7.zip` and `outputs/_archives/arch_selection_results.zip`). It maps the main report claims to reproducibility outputs. Some generated figure filenames differ from final LaTeX figure filenames because the report may use renamed or presentation-ready copies. The primary reproducibility evidence is the CSV outputs and executed notebooks.

## Completed Run Sections

- `01_architecture_selection/`: 4 files
- `02_black_scholes_final_benchmark/`: 39 files
- `03_parameter_robustness_and_parameter_conditioning/`: full report-grade parameter-robustness rerun outputs
- `04_transaction_costs/`: 18 files
- `05_heston_fullinfo_true_vol/`: 106 files
- `06_heston_observable_vol/`: 106 files

## Key Output Files


### Architecture selection

Folder: `source_runs/01_architecture_selection/`

Main files:
- `source_runs/01_architecture_selection/architecture_selection_metrics_from_executed_notebook.csv`
- `source_runs/01_architecture_selection/executed_ideal_minimal_task_hyperparameter_tuning_with_architectures.ipynb`
- `source_runs/01_architecture_selection/ARCHITECTURE_SELECTION_TRACEABILITY.md`

Note: the CSV was extracted from the executed notebook logs because the original notebook saved detailed result files to a Google Drive path during the run. It records the same metrics visible in the executed notebook and supports the architecture-selection table.

### Black--Scholes final benchmark

Folder: `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/`

Main files:
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/final_benchmark_metrics.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/path_count_comparison.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/data_generation_comparison.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/collapse_compact.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness_with_extrapolation.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/average_delta_by_moneyness.csv`

### Robustness and parameter conditioning

Source notebook:
- `notebooks/source/parameter_robustness_study.ipynb`

The source notebook is configured for report-grade reruns with `quick_run=False`. The completed archive now includes the full 50k/15k/50k, 150-epoch robustness rerun outputs, including `parameter_robustness_nn_vs_benchmarks.csv`, `parameter_robustness_summary.csv`, `parameter_robustness_table.tex`, and robustness figures.

Parameter-conditioned/generalization outputs from the final benchmark notebook are available under:
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/universal_robustness_with_extrapolation.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/robustness_compact.csv`
- `source_runs/02_black_scholes_final_benchmark/final_benchmark_outputs/robustness_rmse.csv`

### Transaction costs

Folder: `source_runs/04_transaction_costs/transaction_cost_outputs/`

Main files:
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_compact_results.csv`
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_training_summary.csv`
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_notrade_band_selection.csv`
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_representative_table.csv`
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_rmse_vs_lambda.png`
- `source_runs/04_transaction_costs/transaction_cost_outputs/transaction_cost_cvar95_vs_lambda.png`

### Heston full-information run

Folder: `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/`

Main files:
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_revised_results_fair_premium_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_multiseed_headline_fair_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_multiseed_pairwise_improvements_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_proxy_option_drift_diagnostics_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_same_path_bs_proxy_option_drift_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_cos_carr_madan_validation_traded_range_fullinfo.csv`
- `source_runs/05_heston_fullinfo_true_vol/heston_delta_vega_outputs/heston_cos_greek_finite_difference_check_fullinfo.csv`

### Heston observable-volatility run

Folder: `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/`

Main files:
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_revised_results_fair_premium_obsvol.csv`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_multiseed_headline_fair_obsvol.csv`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_multiseed_pairwise_improvements_obsvol.csv`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_observable_variance_proxy_fidelity_obsvol.csv`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_cos_carr_madan_validation_traded_range_obsvol.csv`
- `source_runs/06_heston_observable_vol/heston_delta_vega_outputs/heston_cos_greek_finite_difference_check_obsvol.csv`

## Architecture-selection multi-seed evidence (active main table)

Source notebook:

```text
notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

Completed evidence (already included, not requiring a rerun):

```text
outputs/architecture_selection_multiseed/seed_2026_results.csv
outputs/architecture_selection_multiseed/seed_2027_results.csv
outputs/architecture_selection_multiseed/seed_2028_results.csv
outputs/architecture_selection_multiseed/multiseed_summary_numeric.csv
outputs/architecture_selection_multiseed/multiseed_summary_formatted.csv
outputs/architecture_selection_multiseed/selection_result.json
```

This is the active main architecture-selection table evidence, selecting the shared normalised `64x3` tanh/sigmoid MLP by lowest mean validation loss across seeds 2026, 2027 and 2028 at batch size 256. The master runner's `RUN_ARCHITECTURE_MULTI_SEED_APPENDIX=False` default does not need to be changed to inspect this evidence; set it to `True` only to independently regenerate it.

The original single-seed architecture-selection trace (`source_runs/01_architecture_selection/architecture_selection_metrics_from_executed_notebook.csv`) remains available for reference but is no longer the active selection evidence.

## Protocol summary documents

- `docs/PROTOCOL_SUMMARY.md`: explains why architecture selection uses batch size 256 while final selected-model retraining and extensions generally use batch size 4096.
- `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md`: records the final `quick_run=False` source patch and confirms the completed full robustness rerun outputs.
- `docs/PROVENANCE_GAPS.md`: records the provenance status of the architecture-selection evidence and any other report/package consistency notes.
