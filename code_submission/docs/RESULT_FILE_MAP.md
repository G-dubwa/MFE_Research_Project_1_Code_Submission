# Result File Map

This map is based on the actual completed run zip in `outputs/source_runs-20260624Tfinal-v7.zip`. It maps the main report claims to reproducibility outputs. Some generated figure filenames differ from final LaTeX figure filenames because the report may use renamed or presentation-ready copies. The primary reproducibility evidence is the CSV outputs and executed notebooks.

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

## Protocol-matched multi-seed architecture appendix

Optional source notebook:

```text
notebooks/source/architecture_selection_multiseed_protocol_matched.ipynb
```

If run through the master runner with `RUN_ARCHITECTURE_MULTI_SEED_APPENDIX=True`, expected collected outputs are:

```text
source_runs/01b_architecture_selection_multiseed_protocol_matched/results/multiseed_per_seed_results.csv
source_runs/01b_architecture_selection_multiseed_protocol_matched/results/multiseed_summary_numeric.csv
source_runs/01b_architecture_selection_multiseed_protocol_matched/results/multiseed_summary_formatted.csv
source_runs/01b_architecture_selection_multiseed_protocol_matched/results/selection_result.json
source_runs/01b_architecture_selection_multiseed_protocol_matched/results/appendix_interpretation_note.md
```

Use this as appendix robustness evidence only. The main report architecture section remains based on the original single-seed Table 1 protocol unless explicitly rewritten.


## Protocol summary documents

- `docs/PROTOCOL_SUMMARY.md`: explains why architecture selection uses batch size 256 while final selected-model retraining and extensions generally use batch size 4096.
- `docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md`: records the final `quick_run=False` source patch and confirms the completed full robustness rerun outputs.
- `docs/PROVENANCE_GAPS.md`: records known report/package consistency gaps if the final report uses results not present in the completed archive.
