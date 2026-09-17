# Atmospheric Dispersion Surrogate Research

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22819727.svg)](https://doi.org/10.5281/zenodo.22819727)

This repository is the public record of an independent research project on fast AERMOD emulation.

The research did not start when this public repository appeared. Work began in a private lab on **14 August 2026**. I kept the working project private while the model, validation rules and failure analysis were still changing, then opened this cleaned public archive after the first small research cycle had reached a sensible stopping point.

I have not backdated the GitHub history. The dated development record in this repository comes from contemporaneous private run logs, frozen artifacts and project notes.

## The question

The question is simple to state: can a separate model learn enough of AERMOD's hourly dispersion response to reproduce a concentration field quickly for cases it has not already seen?

For the first prototype I deliberately kept the physics narrow: one elevated point source, SO2, flat terrain, no downwash, no chemistry or deposition, and a controlled receptor layout. AERMOD remains the teacher, the verification reference and the regulatory model.

This is not presented as a regulatory replacement for AERMOD.

**Project page:** https://ahmadhuseynli.github.io/aermod-surrogate-research/<br>
**Technical note:** https://ahmadhuseynli.github.io/aermod-surrogate-research/assets/AERMOD_SURROGATE_TECHNICAL_NOTE_v0.1.pdf<br>
**Latest archival release:** https://github.com/ahmadhuseynli/aermod-surrogate-research/releases/tag/v0.1.1<br>
**Project DOI:** https://doi.org/10.5281/zenodo.22819727<br>
**Version DOI (v0.1.1):** https://doi.org/10.5281/zenodo.22819728
## Current result

The same frozen Phase2H surrogate was tested on two meteorological years that had been kept out of model development until the scoring rules were fixed.

| Validation year | Baseline whole-field normalised L1 | Frozen surrogate | Relative improvement | Amplitude improvement |
|---|---:|---:|---:|---:|
| 2018 | 0.16904 | 0.12725 | 24.72% | 37.14% |
| 2019 | 0.17218 | 0.13125 | 23.77% | 34.22% |

The two years are from the same broad site climatology, but their hourly weather sequences are materially different. I therefore treat this as evidence of **same-domain temporal generalisation**. It is not evidence yet for transfer to a different climate, a different source family or complex terrain.

The result is also not a claim that the model is “24% accurate”. Those percentages are reductions in one frozen whole-field error measure relative to an earlier baseline surrogate.

The biggest weakness is still the extreme tail. The model improves the field overall, but the largest peak concentration and its location are not yet reliable enough for high-consequence or regulatory use.

## Why the history matters

This project did not progress as a sequence of better and better model scores. Several of the useful results were failures.

An early 10-degree receptor grid could not resolve narrow stable plumes. More trees did not fix that because the missing information was in the teacher representation, not in the learner. Later, a fresh 2024 test exposed another crosswind-resolution problem. A 2025 test then showed that the dominant remaining error had shifted toward longitudinal amplitude and dilution.

Those failures changed what was built next. They are kept in the public history because they explain the present architecture better than a polished success-only account would.
## A short dated trail

- **14 August 2026** — the project started in the private working lab with the narrow point-source/SO2 prototype and teacher-data definition.
- **17 August 2026** — target-robustness work was completed for the first controlled surrogate experiments.
- **20 August 2026** — the information-sufficiency campaign showed that part of the stable-plume problem came from spatial teacher resolution rather than simply missing atmospheric variables.
- **12 September 2026** — the frozen model was taken into a one-shot 2019 temporal test. No 2019 truth-dependent retuning was allowed.
- **14 September 2026** — the same frozen model was tested on 2018 as a second temporal confirmation.
- **17 September 2026** — the first private research cycle was documented and a separate public archive was opened. Zenodo preservation followed after the GitHub release was frozen.

The public GitHub commit dates therefore describe **when the archive was published**, not when the underlying experiments were run.

## Where to look

- [`PROJECT_OVERVIEW.md`](PROJECT_OVERVIEW.md) — what the project is trying to do and why the first scope is small.
- [`DEVELOPMENT_RECORD.md`](DEVELOPMENT_RECORD.md) — dated milestones reconstructed from the private laboratory record.
- [`METHODOLOGY.md`](METHODOLOGY.md) — the public description of teacher data, geometry, target and validation discipline.
- [`RESULTS.md`](RESULTS.md) — the reported frozen results, including the peak failures.
- [`LIMITATIONS.md`](LIMITATIONS.md) — what the current evidence does not support.
- [`RESEARCH_HISTORY.md`](RESEARCH_HISTORY.md) — the main turns in the work, including rejected approaches.
- [`EVIDENCE_AND_PROVENANCE.md`](EVIDENCE_AND_PROVENANCE.md) — what is public, what remains private and how the dates are sourced.
- [`technical_report/`](technical_report/) — the public technical note.

## Public/private split

The private lab still holds the large teacher outputs, detailed run manifests, frozen model artifacts, checksums, operational history and implementation details. They are not all needed to make the public scientific claim understandable, and some are being kept private while longer-term IP and commercial decisions are still open.

The public material is intended to be enough for someone technical to see what was attempted, what was measured, what failed and exactly where the present evidence stops.

## Regulatory position

This is an independent research project. It is not affiliated with or endorsed by the U.S. Environmental Protection Agency. Formal regulatory work should continue to use AERMOD and the required approved modelling procedures.

AERMOD documentation and current releases are available through the U.S. EPA Support Center for Regulatory Atmospheric Modeling (SCRAM):
https://www.epa.gov/scram/air-quality-dispersion-modeling-preferred-and-recommended-models