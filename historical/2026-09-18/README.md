# Atmospheric Dispersion Surrogate Research

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22819727.svg)](https://doi.org/10.5281/zenodo.22819727)

This is an independent research project on a simple question: **can a fast surrogate learn enough of AERMOD's hourly dispersion response to reproduce useful concentration fields without running a full AERMOD case every time?**

The idea is not to replace the physics model or to claim that machine learning knows the atmosphere better than AERMOD. AERMOD is the teacher and the reference. The surrogate is being developed as a fast second layer that could eventually be useful for repeated scenario screening, sensitivity studies, exploratory modelling, large simulation libraries and other situations where thousands of closely related AERMOD-type evaluations would otherwise be needed.

The longer-term direction is a governed system in which AERMOD generates trusted training and verification cases, the surrogate learns the response inside a validated domain, and unsupported cases are sent back to AERMOD instead of being guessed.

**Project page:** https://ahmadhuseynli.github.io/aermod-surrogate-research/  
**Technical note:** https://ahmadhuseynli.github.io/aermod-surrogate-research/assets/AERMOD_SURROGATE_TECHNICAL_NOTE_v0.1.pdf  
**Project DOI:** https://doi.org/10.5281/zenodo.22819727  

## The first prototype

I deliberately started with a small physical domain: one elevated point source, SO2, flat terrain, no building downwash, no chemistry or deposition, and a controlled receptor layout.

The target is not an annual maximum or a single compliance statistic. The model learns the **hourly receptor concentration field**.

In shorthand:

**source + meteorological state + plume-relative receptor geometry -> surrogate -> hourly concentration field**

Keeping the first problem small made it possible to separate different causes of error. That turned out to be important. Some of the largest early problems came from how the AERMOD teacher field was sampled in space, not simply from the machine-learning model.

## Current result

The same frozen Phase2H surrogate was tested on two meteorological years that had been kept out of model development until the prediction and scoring rules were fixed.

| Validation year | Baseline whole-field normalised L1 | Frozen surrogate | Relative improvement | Approx. whole-field agreement* | Amplitude improvement |
|---|---:|---:|---:|---:|---:|
| 2018 | 0.16904 | 0.12725 | 24.72% | 87.28% | 37.14% |
| 2019 | 0.17218 | 0.13125 | 23.77% | 86.87% | 34.22% |

*For readability, whole-field agreement is shown as **1 - normalised L1**. It is useful as an intuitive summary of this particular internal metric, but it is not a general-purpose "accuracy" score and it is not a comparison with measured ambient concentrations.

So the present model is at roughly **87% whole-field agreement on the frozen normalised-L1 metric** in the two untouched same-domain year tests. More importantly, it reduced the previous surrogate's field error by about 24% in both years and reduced amplitude error by about 34-37%.

The two years come from the same broad site climatology but have materially different hourly weather sequences. I therefore treat this as evidence of **same-domain temporal generalisation**. It is not yet evidence for transfer to a different climate, a different source family, complex terrain or building downwash.

The biggest weakness is still the extreme tail. The model improves the field overall, but the largest peak concentration and its location are not yet reliable enough for high-consequence or regulatory use.

## Why this could be useful

A successful dispersion surrogate would not remove AERMOD from the workflow. Its value would be speed inside a domain that has already been demonstrated.

Possible uses, if later validation supports them, include:

- rapid screening of many source/meteorology/receptor combinations;
- sensitivity studies that would otherwise require very large batches of AERMOD runs;
- fast first-pass concentration fields before formal verification;
- adaptive simulation campaigns where the surrogate identifies weak regions and requests new AERMOD cases;
- uncertainty and applicability checks that tell the user when the surrogate should not be trusted;
- eventually, broader operational or forecasting tools built on top of a validated hourly dispersion engine.

The present project is still several steps away from those wider uses. Variable stack conditions, other climates, terrain, downwash and multiple sources all need their own controlled validation.

## How the work developed

This was not a straight sequence of improving scores.

An early angular receptor grid could not resolve some narrow stable plumes. More model capacity did not solve it because the missing information was already absent from the sampled teacher field. Later fresh-year diagnostics exposed another crosswind problem and then a different weakness in longitudinal amplitude and dilution.

Those failures changed the model design. The project moved toward plume-relative geometry, targeted spatial reconstruction and a bounded amplitude/residual correction rather than simply making the learner larger.

The final frozen prototype was then taken into two untouched year-level tests without truth-dependent retraining.

A fuller account is in DEVELOPMENT_RECORD.md and RESEARCH_HISTORY.md.

## Where to look

- PROJECT_OVERVIEW.md - the idea, scope and longer-term purpose.
- DEVELOPMENT_RECORD.md - the main scientific development stages.
- METHODOLOGY.md - teacher data, geometry, target and validation discipline.
- RESULTS.md - frozen results, including the peak failures.
- LIMITATIONS.md - what the present evidence does not support.
- RESEARCH_HISTORY.md - the main turns in the work, including rejected approaches.
- EVIDENCE_AND_PROVENANCE.md - validation roles, public/private boundary and evidence chain.
- ROADMAP.md - the next scientific boundaries to test.
- technical_report/ - the public technical note.

## Public/private split

The private lab retains the large teacher outputs, detailed run manifests, frozen model artifacts, checksums, operational history and implementation details. The public repository is a readable scientific record rather than a mirror of the full working environment.

That split also leaves room for future intellectual-property and commercial decisions without hiding the scientific result or its limitations.

## Regulatory position

This is an independent research project. It is not affiliated with or endorsed by the U.S. Environmental Protection Agency. The surrogate is not an approved regulatory replacement for AERMOD.

Formal regulatory work should continue to use AERMOD and the required approved modelling procedures.

AERMOD documentation and current releases are available through the U.S. EPA Support Center for Regulatory Atmospheric Modeling (SCRAM):
https://www.epa.gov/scram/air-quality-dispersion-modeling-preferred-and-recommended-models
