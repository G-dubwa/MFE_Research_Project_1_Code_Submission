# Parameter Robustness Completed Outputs

This folder contains the full report-grade parameter-robustness rerun outputs generated on 24 June 2026.

The rerun used:

- `quick_run = False`
- Train/validation/test paths: 50,000 / 15,000 / 50,000
- Batch size: 4096
- Max epochs: 150
- Early-stopping patience: 15
- Selected architecture: shared normalized Markov MLP, width 64, depth 3, tanh hidden activation, sigmoid output

Key files:

- `parameter_robustness_nn_vs_benchmarks.csv`
- `parameter_robustness_summary.csv`
- `parameter_robustness_table.tex`
- `robustness_rmse_vs_N.png`
- `robustness_ratio_vs_N.png`
- `history_*.csv`

The NN/DT RMSE ratio ranges from approximately 1.009 to 1.099, with mean approximately 1.049, matching the report's robustness narrative.
