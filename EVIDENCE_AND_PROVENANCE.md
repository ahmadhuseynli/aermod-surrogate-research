# Evidence and provenance

## Why this public repository is newer than the work

The working project began on **14 August 2026** in a private research workspace. The public GitHub repository was opened on **17 September 2026**, after the first development cycle had been frozen and documented.

That separation was intentional. During development, the private lab was changing frequently and contained large teacher outputs, controller files, local run paths and model artifacts that did not belong in a public repository.

I have not backdated the public Git history. The older dates shown in [`DEVELOPMENT_RECORD.md`](DEVELOPMENT_RECORD.md) come from contemporaneous private project records.

## What exists in the private evidence chain

The private archive retains, among other things:

- AERMOD teacher outputs and run manifests;
- frozen model/data hashes;
- preregistered experiment decisions;
- run-by-run operation history;
- pre-truth validation seals;
- failed experiments and recovery records;
- trained model artifacts and implementation code.

The public repository is a readable research record, not a mirror of that full laboratory workspace.
## Validation roles

| Year | Role when first opened | What happened afterward |
|---|---|---|
| 2024 | fresh representation test | crosswind-resolution failure diagnosed; year became development evidence |
| 2025 | fresh error-mechanism test | amplitude/dilution weakness diagnosed; year became development evidence |
| 2022 | untouched architecture exam | architecture direction supported; year became development evidence |
| 2019 | one-shot temporal confirmation | frozen model scored; year then became spent evidence |
| 2018 | second one-shot temporal confirmation | same frozen model scored; year then became spent evidence |

An opened year is not later presented as fresh validation for a revised model.

## The frozen model reported here

The 2018 and 2019 results use the same Phase2H surrogate. No validation-year retraining, architecture change or post-hoc support-threshold tuning is included in those reported numbers.

The public repository reports the scientific state that existed at the end of the first private research cycle. The Zenodo archival release adds preservation and citation metadata; it does not change the scientific model or the reported validation results.

## What is intentionally not public

The full teacher library, trained weights, exact production residual library, internal controller, local machine paths and detailed orchestration are not part of this release.

That is partly practical and partly deliberate. The public record is meant to expose enough evidence to understand the work without publishing every implementation detail before the longer-term IP and commercial direction is decided.