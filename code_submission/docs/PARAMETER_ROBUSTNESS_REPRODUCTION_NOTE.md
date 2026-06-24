# Parameter Robustness Reproduction Note

The submitted source notebook `notebooks/source/parameter_robustness_study.ipynb` is configured for the full report-grade robustness run by default:

```python
quick_run = False
```

Full rerun settings:

- Train paths: 50,000
- Validation paths: 15,000
- Test paths: 50,000
- Batch size: 4096
- Max epochs: 150
- Early-stopping patience: 15
- Selected architecture: shared normalized Markov MLP, width 64, depth 3, tanh hidden activation, sigmoid output

The completed-output archive now includes the full rerun outputs under:

```text
source_runs/03_parameter_robustness_and_parameter_conditioning/
```

Key files include `parameter_robustness_nn_vs_benchmarks.csv`, `parameter_robustness_summary.csv`, `parameter_robustness_table.tex`, and the robustness RMSE/ratio figures.

The rerun supports the report table: the NN/DT RMSE ratio ranges from approximately 1.009 to 1.099 with mean approximately 1.049.
