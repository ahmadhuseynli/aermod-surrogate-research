# Atmospheric Dispersion Surrogate Research

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22819727.svg)](https://doi.org/10.5281/zenodo.22819727)

**Independent research project exploring whether a machine-learning surrogate can reproduce AERMOD-type hourly concentration fields inside a carefully limited domain.**

This project started with a simple question: if AERMOD is used as the reference model, can a separate surrogate learn enough of its hourly dispersion response to make fast predictions for cases it has not seen before?

The work is still a research prototype. It is **not** a regulatory replacement for AERMOD, and it is not presented as one.

**Public project page:** https://ahmadhuseynli.github.io/aermod-surrogate-research/  
**Technical note:** https://ahmadhuseynli.github.io/aermod-surrogate-research/assets/AERMOD_SURROGATE_TECHNICAL_NOTE_v0.1.pdf  
**Latest archival release:** https://github.com/ahmadhuseynli/aermod-surrogate-research/releases/tag/v0.1.1  
**Project DOI (all versions):** https://doi.org/10.5281/zenodo.22819727  
**Version DOI (v0.1.1):** https://doi.org/10.5281/zenodo.22819728

## Where the project stands

The current frozen prototype has been tested on two meteorological years that were kept untouched until the model and evaluation rules were fixed.

| Validation year | Baseline whole-field normalized L1 | Frozen surrogate | Relative improvement | Amplitude improvement |
|---|---:|---:|---:|---:|
| 2018 | 0.16904 | 0.12725 | 24.72% | 37.14% |
| 2019 | 0.17218 | 0.13125 | 23.77% | 34.22% |

The two years came from the same broad site climatology, but the hourly weather histories were materially different. The result therefore supports **same-domain temporal generalisation**, not a claim of generalisation to other climates, source types or terrain.

The main unresolved problem is the extreme tail. The model improves the concentration field as a whole, but it does not yet reproduce the largest peak concentrations or their location reliably enough for regulatory use.

## What is being modelled

The first prototype is intentionally narrow:

- one elevated point source;
- SO2 as a passive pollutant for the prototype;
- flat/rural terrain;
- no building downwash;
- no chemistry or deposition;
- controlled receptor geometry;
- hourly concentration field as the main target.

AERMOD remains the teacher, verification reference and regulatory model.

## Why the project is useful

The project is less about replacing a dispersion model and more about learning where a surrogate can and cannot reproduce one. That has required work on meteorological preprocessing, plume-relative geometry, spatial resolution, feature design, model training, residual error analysis, out-of-domain checks and strict validation without repeatedly tuning against the same test year.

A large part of the research has come from failed ideas. For example, an early angular receptor representation was too coarse for narrow stable plumes. Later, a fresh-year test showed that a crosswind spacing that looked acceptable during development was still too coarse. Those failures changed the design rather than being hidden.

## Repository map

- [`PROJECT_OVERVIEW.md`](PROJECT_OVERVIEW.md) - the project in plain language.
- [`METHODOLOGY.md`](METHODOLOGY.md) - how the teacher data, geometry and surrogate are handled.
- [`RESULTS.md`](RESULTS.md) - the current validation evidence.
- [`LIMITATIONS.md`](LIMITATIONS.md) - what the model cannot currently support.
- [`RESEARCH_HISTORY.md`](RESEARCH_HISTORY.md) - the main scientific turns, including failures.
- [`ROADMAP.md`](ROADMAP.md) - the next research questions.
- [`data/`](data/) - small public summary tables only; no training data or model weights.
- [`technical_report/`](technical_report/) - the public technical note in PDF and DOCX form.
- [`docs/`](docs/) - the GitHub Pages website.

## Reproducibility and evidence

The private research lab keeps the full experiment history, frozen artifacts, checksums, run records and teacher outputs. This public repository exposes a readable summary and selected validation tables rather than the full internal pipeline.

That split is intentional. It lets the scientific claims be described clearly while keeping large data, operational tooling and research implementation details out of the public release for now.

## Regulatory position

This work is an independent research prototype. It is not affiliated with or endorsed by the U.S. Environmental Protection Agency. The surrogate is not an approved substitute for AERMOD. Formal regulatory modelling should continue to use the required approved model, inputs and procedures.

## Current release

**v0.1.1 - Zenodo archival release**

This release preserves the same scientific/model state reported in v0.1.0. No model, validation result or reported conclusion changed. v0.1.1 adds citation and Zenodo metadata so the public research prototype has a permanent DOI.

For a citation tied to this exact archived version, use **10.5281/zenodo.22819728**. For a citation that should always resolve to the latest archived version of the project, use **10.5281/zenodo.22819727**.

## Reference model

AERMOD documentation and current model releases are available from the U.S. EPA Support Center for Regulatory Atmospheric Modeling (SCRAM):

https://www.epa.gov/scram/air-quality-dispersion-modeling-preferred-and-recommended-models
