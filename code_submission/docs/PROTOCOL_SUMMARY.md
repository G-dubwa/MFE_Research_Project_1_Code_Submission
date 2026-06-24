# Protocol Summary for Code Submission

This package intentionally does **not** use one batch size everywhere. The rule is that protocols are fixed within each direct comparison, while later experiment families use larger or modified training budgets appropriate to their purpose.

## Batch-size distinction

| Experiment family | Batch size | Reason |
|---|---:|---|
| Architecture selection / candidate comparison | 256 | Original Table 1 protocol; fair comparison across candidate architectures. |
| Optional multi-seed architecture appendix | 256 | Protocol-matched robustness check for architecture selection. |
| Final Black--Scholes selected-model retraining | 4096 | Heavier independent retraining of the already-selected architecture. |
| Parameter robustness / parameter conditioning | 4096 | Retraining selected architecture or parameter-conditioned model. |
| Transaction costs | 4096 | Extension experiment with cost-aware objective. |
| Heston full-info and observable-volatility modes | 4096 | Larger PyTorch Heston stock/option hedging runs. |

## Selected Black--Scholes architecture

```text
Shared normalized Markov MLP
Inputs: log(S_t/K), tau/T
Hidden layers: 3
Width: 64
Hidden activation: tanh
Output activation: sigmoid
Premium: learned scalar, except parameter-conditioned runs use analytic BS premium per path
Loss: terminal MSE hedge error
```

## Interpretation

The architecture-selection candidates were trained with batch size 256. After selecting the shared normalized 64x3 tanh-sigmoid MLP, the selected model was independently retrained for the final benchmark and later extension experiments under larger experiment-specific budgets, typically batch size 4096.

The optional multi-seed architecture notebook is included only as an appendix robustness check and is disabled by default in the master runner.
