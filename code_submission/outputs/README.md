# Output Evidence Folder

This folder contains the numerical evidence supporting the report.

## Primary inspection route

The primary inspection route is the extracted folder structure:

```text
source_runs/
architecture_selection_multiseed/
```

Zip files, where retained, are stored in `_archives/` as backup copies only.

## Main completed source runs

```text
source_runs/
```

This folder contains the completed source-run folders for the main report experiments:

```text
source_runs/01_architecture_selection/
source_runs/02_black_scholes_final_benchmark/
source_runs/03_parameter_robustness_and_parameter_conditioning/
source_runs/04_transaction_costs/
source_runs/05_heston_fullinfo_true_vol/
source_runs/06_heston_observable_vol/
```

The CSV files, executed notebooks, logs and manifests inside these folders are the primary evidence for the report's numerical claims.

## Architecture-selection multi-seed evidence

```text
architecture_selection_multiseed/
```

This folder contains the three-seed, twelve-candidate architecture-selection evidence used for the active architecture-selection table in the report:

```text
seed_2026_results.csv
seed_2027_results.csv
seed_2028_results.csv
multiseed_summary_numeric.csv
multiseed_summary_formatted.csv
selection_result.json
```

The selected architecture is the shared normalised `64x3` tanh/sigmoid MLP (`shared_norm_64u_3L_tanh_sigmoid`), selected by lowest mean validation loss across three independent seeds (2026, 2027, 2028) at batch size 256. The runner-up (`shared_norm_32u_3L_tanh_sigmoid`) is close, so the report describes this as a selected architecture rather than a dominant one. `selection_result.json` also records the per-seed winners: seeds 2026 and 2027 both select the same architecture, while seed 2028 selects a close competitor (`shared_norm_64u_2L_relu_sigmoid`).

There is no separate supplementary top-competitor investigation folder in this submission; this folder is the complete architecture-selection evidence.

## Archives

```text
_archives/
```

This folder contains original zip files retained as backup copies. The extracted folders are the preferred inspection path.

```text
_archives/source_runs-20260624Tfinal-v7.zip
_archives/arch_selection_results.zip
```

## Manifest

```text
output_manifest_summary.csv
```

This file lists output files from the completed run archives (`source_runs-20260624Tfinal-v7.zip` and `arch_selection_results.zip`) and can be used as a quick index. It has been regenerated to include the three-seed architecture-selection files under `architecture_selection_multiseed/` alongside the main `source_runs/` files.
