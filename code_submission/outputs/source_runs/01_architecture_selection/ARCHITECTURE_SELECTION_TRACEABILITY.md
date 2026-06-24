# Architecture Selection Traceability Patch

This folder originally contained the executed architecture-selection notebook but no exported CSV because the notebook wrote its results to a Google Drive run directory during execution.

To make the report's architecture-selection table traceable inside the submitted package, `architecture_selection_metrics_from_executed_notebook.csv` was extracted from the executed notebook's logged training output. This does **not** rerun or alter the experiment; it only records the metrics already present in the executed notebook.

Selected model by validation loss:

```text
shared_norm_64u_3L_tanh_sigmoid
validation_loss = 6.16748e-05
test_rmse = 0.00781958
learned_premium = 0.16405
runtime_seconds = 62.6
```

The original executed notebook remains in this folder for auditability.
