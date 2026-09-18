# Atmospheric Dispersion Surrogate Research

## Public technical note

**Current public archive:** v0.1.2 / Zenodo project DOI 10.5281/zenodo.22819727

This note summarises the first mature research cycle of an independent AERMOD-surrogate project.

The idea is straightforward: use AERMOD as the teacher and test whether a separate surrogate can reproduce its hourly concentration field quickly inside a clearly defined domain. If that can be done reliably, the surrogate could eventually support large scenario libraries, sensitivity studies, adaptive simulation campaigns and rapid first-pass concentration fields while AERMOD remains the verification and regulatory model.

The surrogate is not being presented as a better model of the real atmosphere and is not a regulatory replacement for AERMOD.

## 1. Starting point

The first prototype was intentionally simple: one fixed elevated point source, SO2, flat/rural terrain, no building downwash, no chemistry or deposition, and controlled receptor geometry.

The main target was the hourly field, not an annual maximum. Concentration was normalised by emission rate, C/Q, where that proportionality was valid for the controlled case. A reversible log transform was used during learning because the teacher field spans a very large dynamic range.

The original full-year teacher set contained more than 6.6 million receptor-hour rows.

## 2. The first things that did not work

The early boosted-tree model learned a meaningful part of the response, but training longer gave diminishing returns. That was the first sign that the remaining error was not simply a capacity problem.

The project then moved toward plume-relative geometry. In flat homogeneous terrain the plume should rotate with the wind, so absolute compass direction was an unnecessary burden for the learner.

A larger problem appeared in the teacher representation. The early angular receptor grid could miss the core of narrow stable plumes. Adding more trees could not recover information that the spatial sampling never captured.

That changed the direction of the project. Before asking the learner to improve again, I started testing whether the teacher field itself could be reconstructed from the chosen receptor support.

Crosswind interpolation improved first. Longitudinal coverage then failed, and a two-dimensional near-source composition test failed separately. The response was targeted spatial densification rather than a larger model.

## 3. Fresh-year tests changed the model again

A 2024 test, opened after a representation freeze, exposed another crosswind-resolution weakness in narrow stable conditions. Once that result had been used to change the geometry, 2024 was no longer treated as fresh validation.

The 2025 test pointed to a different problem. The main remaining error had moved toward longitudinal amplitude and dilution. That led to an amplitude-residual layer.

An untouched 2022 architecture exam supported that direction: whole-field L1 improved from about 0.21115 to 0.16964 and 119 of 128 cases improved. The absolute error was still too large, so the work continued. After the test was opened, 2022 became development evidence.

Several follow-on residual models were tried and rejected. Regime-specific experts, low-dimensional residual predictors and direct lateral corrections did not survive the frozen development gates. The surviving model used a strongly bounded local residual correction and became the Phase2H prototype.

## 4. Frozen temporal confirmation

Phase2H was sealed before the final year-level teacher concentration truth was opened. No retraining, architecture change or truth-dependent applicability-threshold tuning was allowed for the reported result.

| Metric | 2018 | 2019 |
|---|---:|---:|
| Usable hours | 8,620 | 8,531 |
| Baseline whole-field normalised L1 | 0.1690417 | 0.1721767 |
| Phase2H whole-field normalised L1 | 0.1272474 | 0.1312534 |
| Approx. whole-field agreement (1 - L1) | 87.28% | 86.87% |
| Relative field improvement | 24.72% | 23.77% |
| Baseline amplitude normalised L1 | 0.1221596 | 0.1228541 |
| Phase2H amplitude normalised L1 | 0.0767853 | 0.0808092 |
| Relative amplitude improvement | 37.14% | 34.22% |

The final whole-field error is therefore about 12.7-13.1% on the frozen normalised-L1 metric. Written as 1 - L1, that is roughly **87% whole-field agreement** in both untouched year tests.

I use that percentage only as a plain-language reading of this particular field metric. It is not a universal accuracy score and it is not a comparison with measured ambient concentrations.

The two confirmation years came from the same broad site climatology, so this is not a cross-climate test. They were, however, materially different hourly meteorological realisations. Same-calendar wind-speed correlation was 0.043, the median absolute wind-direction difference was 75 degrees, and no comparable calendar hour had an identical full dynamic state.

The result therefore supports same-domain temporal generalisation across different hourly meteorology.

## 5. The main failure that remains

The global peaks were wrong.

In 2018 the AERMOD maximum was about 3.02 in the project C/Q scale, while Phase2H produced about 7.11 at a different case/receptor. In 2019 AERMOD produced about 3.10, while Phase2H produced about 6.61, again at a different location.

That is not a side issue. A model can show strong field-average agreement and still be unsuitable for a peak-driven decision. I therefore do not claim reliable prediction of the controlling receptor or the regulatory extreme tail.

## 6. What the first cycle actually showed

The narrow AERMOD response is learnable well enough to produce repeatable whole-field performance on unseen years inside one controlled domain. Plume-relative geometry helped. Teacher-grid resolution mattered more than expected. A bounded amplitude/residual structure improved the frozen baseline consistently.

The final model achieved around **87% whole-field agreement on the internal normalised-L1 metric** and reduced the previous surrogate's field error by about 24% in both untouched year tests.

It did **not** show extremely small error, reliable peak behaviour, transfer to another climate or site, variable source physics, complex terrain, downwash, multiple sources or chemistry/deposition.

## 7. Why the project could matter

AERMOD is well suited to formal dispersion modelling, but repeated large simulation programmes can be slow and expensive to explore.

A reliable surrogate could make the repeated part of that workflow much faster. The most interesting longer-term uses are not a single shortcut calculation, but large scenario screening, sensitivity analysis, uncertainty mapping and adaptive simulation - where the surrogate identifies unsupported regions and asks AERMOD for new teacher cases.

That creates a practical division of labour: AERMOD remains the reference, verification and regulatory model, while the surrogate handles fast prediction only where its support has been demonstrated.

## 8. Public/private boundary

The full teacher library, model weights, exact residual library, controller code and operational run archive remain private.

The public material is meant to show the scientific question, the evidence, the failures and the boundary of the present claim without publishing the entire working lab.

## 9. Next useful tests

The next work should not be another small tweak on the same setup.

The stronger experiments are to improve extreme-tail behaviour without fitting known peaks, test a different site or climate, and introduce a bounded range of source height, diameter, exit velocity and temperature.

Only after those are stable would it make sense to move into terrain, downwash, multiple sources and wider source classes.

## Reference

U.S. Environmental Protection Agency, Support Center for Regulatory Atmospheric Modeling (SCRAM), AERMOD Modeling System code and documentation:
https://www.epa.gov/scram/air-quality-dispersion-modeling-preferred-and-recommended-models

This is an independent project and is not affiliated with or endorsed by the U.S. EPA.
