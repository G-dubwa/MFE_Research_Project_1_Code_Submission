# Neural Hedging Code Submission

This repository has been cleaned so that the assessment-facing material is in one place:

```text
code_submission/
```

Start here:

```text
code_submission/README.md
```

The main Colab entry notebook is:

```text
code_submission/01_reproduce_report_results.ipynb
```

The completed run outputs are included under:

```text
code_submission/outputs/
```

This package intentionally excludes old project material from the submission
repository. The assessment-facing material is the curated `code_submission/`
folder and the root README.

## Final Protocol Notes

- Architecture selection and the optional multi-seed architecture appendix use
  batch size `256`.
- Final selected-model retraining and extension experiments generally use batch
  size `4096`.
- The optional architecture multi-seed appendix notebook is included under
  `code_submission/notebooks/source/`, but it is disabled by default in the
  master runner because it is expensive.
- The parameter-robustness source notebook is patched to `quick_run=False` for
  full reruns. The included completed-output archive now contains the full
  parameter-robustness rerun outputs.

## Repository Layout

| Path | Purpose |
|---|---|
| `code_submission/` | Final submission package for assessment and reproduction |
| `code_submission/README.md` | Submission instructions, workflow, expected runtime, and result notes |
| `code_submission/01_reproduce_report_results.ipynb` | Single notebook entry point |
| `code_submission/notebooks/source/` | Source notebooks used by the runner |
| `code_submission/outputs/` | Extracted completed output folders, architecture-selection evidence, manifest, and archived backup zips |
| `code_submission/docs/RESULT_FILE_MAP.md` | Map from report claims to concrete output files |
| `code_submission/docs/PROTOCOL_SUMMARY.md` | Batch-size and protocol notes |
| `code_submission/docs/PARAMETER_ROBUSTNESS_REPRODUCTION_NOTE.md` | Parameter-robustness rerun settings and output note |
| `code_submission/docs/PROVENANCE_GAPS.md` | Provenance status, resolved evidence notes, and remaining caveats |
