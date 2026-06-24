# Protocol-matched architecture-selection multi-seed notebook

This notebook is a patched version of Micaela's `architecture_selection_multiseed.ipynb` intended for appendix-only robustness evidence.

## Main changes

- Uses `batch_size=256`, matching the original architecture-selection experiment. The earlier draft used `4096`, which gave each candidate far fewer optimiser updates and made the result not comparable to Table 1.
- Keeps the original Black--Scholes setup: `S0=1`, `K=0.9`, `sigma=0.4`, `T=0.5`, `r=0`, `N=125`.
- Keeps the original training defaults: `M_train=100000`, `M_val=20000`, `M_test=50000`, `max_epochs=60`, early-stopping patience `8`, reduce-LR patience `4`, Adam learning rate `1e-3`.
- Writes to local relative output folders under `./mfe_deep_hedging_runs/`, not Google Drive, so the master reproducibility runner can collect CSV/JSON/MD outputs.
- Exports `multiseed_per_seed_results.csv`, per-seed CSVs, `multiseed_summary_numeric.csv`, `multiseed_summary_formatted.csv`, `selection_result.json`, `appendix_interpretation_note.md`, and an output manifest.
- Disables the optional original-seed sanity check by default.

## Recommended report use

This three-seed run is now the active main architecture-selection evidence for the report (see `docs/PROVENANCE_GAPS.md`). The completed evidence from running this notebook is included under `outputs/architecture_selection_multiseed/`: `seed_2026_results.csv`, `seed_2027_results.csv`, `seed_2028_results.csv`, `multiseed_summary_numeric.csv`, `multiseed_summary_formatted.csv`, and `selection_result.json`.

Per `selection_result.json`, the winner by lowest mean validation loss across the three seeds is `shared_norm_64u_3L_tanh_sigmoid`, with `shared_norm_32u_3L_tanh_sigmoid` as the closest competitor by mean validation loss. Per-seed winners are `shared_norm_64u_3L_tanh_sigmoid` for seeds 2026 and 2027, and `shared_norm_64u_2L_relu_sigmoid` for seed 2028.

A safe wording is:

> Across three independent seeds, the shared normalized MLP architectures remain the leading family. The selected 64x3 tanh sigmoid model and its closest competitors achieve similar error levels, so the architecture choice is interpreted as selecting a reliable representative architecture rather than identifying a unique global optimum.

## Runtime note

This notebook trains 12 architectures across 3 seeds, so it is significantly more expensive than the original single-seed architecture table. Run on Colab with GPU. Use `SMOKE_TEST=True` only to check plumbing; do not use smoke-test outputs in the report.
