# Evidence and provenance

## Public record and private lab

The public repository is a cleaned research record. The working project itself was developed in a private laboratory that contains much more material than is useful or appropriate to publish directly.

That private environment changes frequently and includes large teacher outputs, controller files, local run paths, model artifacts and detailed operational logs. The public repository keeps the scientific question, validation logic, reported results and limitations readable without mirroring the entire lab.

GitHub commit history therefore records changes to the public archive. It should not be read as a complete chronology of every underlying experiment.

## What exists in the private evidence chain

The private archive retains, among other things:

- AERMOD teacher outputs and run manifests;
- frozen model/data hashes;
- preregistered experiment decisions;
- run-by-run operation history;
- pre-truth validation seals;
- failed experiments and recovery records;
- trained model artifacts and implementation code.

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

Whole-field normalised L1 was 0.1272474 and 0.1312534, which can also be read as roughly 87.3% and 86.9% whole-field agreement when expressed as 1 - normalised L1.

That is an intuitive restatement of the internal metric, not a claim of universal model accuracy and not a comparison with measured ambient air concentrations.

## What is intentionally not public

The full teacher library, trained weights, exact production residual library, internal controller, local machine paths and detailed orchestration are not part of this release.

That is partly practical and partly deliberate. The public record is meant to expose enough evidence to understand the work while keeping the complete research machinery and future IP/commercial options separate.
