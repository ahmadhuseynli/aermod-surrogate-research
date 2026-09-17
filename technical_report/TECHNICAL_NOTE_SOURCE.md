# Atmospheric Dispersion Surrogate Research

## Public technical note

**Research started:** 14 August 2026<br>
**Public archive opened:** 17 September 2026<br>
**Current public archive:** v0.1.1 / Zenodo project DOI 10.5281/zenodo.22819727

This note summarises the first development cycle of an independent AERMOD-surrogate research project. The working project began in a private lab more than a month before this public repository was created. I have kept those two dates separate rather than trying to make the public Git history look older than it is.

The purpose of the work is narrow: use AERMOD as the teacher and test whether a separate surrogate can reproduce its hourly concentration field inside a clearly defined domain. The surrogate is not being presented as a better model of the real atmosphere and is not a regulatory replacement for AERMOD.

## 1. Starting point

The first prototype was intentionally simple: one fixed elevated point source, SO2, flat/rural terrain, no building downwash, no chemistry or deposition, and controlled receptor geometry.

The main target was the hourly field, not an annual maximum. Concentration was normalised by emission rate, C/Q, where that proportionality was valid for the controlled case. A reversible log transform was used during learning because the teacher field spans a very large dynamic range.

The original full-year teacher set contained more than 6.6 million receptor-hour rows.

## 2. The first things that did not work

The early boosted-tree model learned a meaningful part of the response, but training longer gave diminishing returns. That was the first sign that the remaining error was not simply a capacity problem.

The project then moved toward plume-relative geometry. In flat homogeneous terrain the plume should rotate with the wind, so absolute compass direction was an unnecessary burden for the learner.
A larger problem appeared in the teacher representation. The early 10-degree angular receptor grid could miss the core of narrow stable plumes. Adding more trees could not recover information that the spatial sampling never captured.

That changed the direction of the project. Before asking the learner to improve again, I started testing whether the teacher field itself could be reconstructed from the chosen receptor support.

Crosswind interpolation improved first. Longitudinal coverage then failed, and a two-dimensional near-source composition test failed separately. The response was targeted spatial densification rather than a larger model.

## 3. Fresh-year tests changed the model again

A 2024 test, opened after a representation freeze, exposed another crosswind-resolution weakness in narrow stable conditions. Once that result had been used to change the geometry, 2024 was no longer treated as fresh validation.

The 2025 test pointed to a different problem. The main remaining error had moved toward longitudinal amplitude and dilution. That led to an amplitude-residual layer.

An untouched 2022 architecture exam supported that direction: whole-field L1 improved from about 0.21115 to 0.16964 and 119 of 128 cases improved. The absolute error was still too large, so the work continued. After the test was opened, 2022 became development evidence.

Several follow-on residual models were tried and rejected. Regime-specific experts, low-dimensional residual predictors and direct lateral corrections did not survive the frozen development gates. The surviving model used a strongly bounded local residual correction and became the Phase2H prototype.

## 4. One-shot temporal confirmation

Phase2H was sealed before the 2019 teacher concentration truth was opened. No retraining, architecture change or truth-dependent applicability-threshold tuning was allowed for the reported result.

| Metric | 2018 | 2019 |
|---|---:|---:|
| Usable hours | 8,620 | 8,531 |
| Baseline whole-field normalised L1 | 0.1690417 | 0.1721767 |
| Phase2H whole-field normalised L1 | 0.1272474 | 0.1312534 |
| Relative field improvement | 24.72% | 23.77% |
| Baseline amplitude normalised L1 | 0.1221596 | 0.1228541 |
| Phase2H amplitude normalised L1 | 0.0767853 | 0.0808092 |
| Relative amplitude improvement | 37.14% | 34.22% |
The two confirmation years came from the same broad site climatology, so this is not a cross-climate test. They were, however, materially different hourly meteorological realisations. Same-calendar wind-speed correlation was 0.043, the median absolute wind-direction difference was 75 degrees, and no comparable calendar hour had an identical full dynamic state.

The result therefore supports same-domain temporal generalisation across different hourly meteorology.

## 5. The main failure that remains

The global peaks were wrong.

In 2018 the AERMOD maximum was about 3.02 in the project C/Q scale, while Phase2H produced about 7.11 at a different case/receptor. In 2019 AERMOD produced about 3.10, while Phase2H produced about 6.61, again at a different location.

That is not a side issue. A model can improve the field average and still be unsuitable for a peak-driven decision. I therefore do not claim reliable prediction of the controlling receptor or the regulatory extreme tail.

## 6. What I think the first cycle actually showed

The narrow AERMOD response is learnable well enough to produce repeatable improvement on unseen years inside one controlled domain. Plume-relative geometry helped. Teacher-grid resolution mattered more than expected. A bounded amplitude/residual structure improved the frozen baseline consistently.

It did **not** show extremely small error, reliable peak behaviour, transfer to another climate or site, variable source physics, complex terrain, downwash, multiple sources or chemistry/deposition.

## 7. Why the public archive is newer

The private project started on 14 August 2026. The public repository was opened on 17 September after the first research cycle had been frozen and documented. The older milestones in the public development record come from contemporaneous private run logs, project chats, handoff packages and operation history.

The full teacher library, model weights, exact residual library, controller code and operational run archive remain private. The public material is meant to show the scientific question, the evidence, the failures and the boundary of the present claim without publishing the entire working lab.

## 8. Next useful tests

The next work should not be another small tweak on the same setup. The stronger experiments are: improve extreme-tail behaviour without fitting known peaks; test a different site or climate; and then introduce a bounded range of source height, diameter, exit velocity and temperature.

Only after those are stable would I move into terrain, downwash, multiple sources and wider source classes.

## Reference

U.S. Environmental Protection Agency, Support Center for Regulatory Atmospheric Modeling (SCRAM), AERMOD Modeling System code and documentation:
https://www.epa.gov/scram/air-quality-dispersion-modeling-preferred-and-recommended-models

This is an independent project and is not affiliated with or endorsed by the U.S. EPA.