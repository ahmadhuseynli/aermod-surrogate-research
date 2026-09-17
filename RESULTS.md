# Results

## Untouched temporal validation

The current model was frozen before the two tests below were scored. Neither year was used to tune the reported frozen model before its first evaluation.

| Metric | 2018 | 2019 |
|---|---:|---:|
| Usable hours | 8,620 | 8,531 |
| Baseline whole-field normalised L1 | 0.1690417 | 0.1721767 |
| Frozen surrogate whole-field normalised L1 | 0.1272474 | 0.1312534 |
| Relative field improvement | 24.72% | 23.77% |
| Baseline amplitude normalised L1 | 0.1221596 | 0.1228541 |
| Frozen surrogate amplitude normalised L1 | 0.0767853 | 0.0808092 |
| Relative amplitude improvement | 37.14% | 34.22% |

The similarity of the two results is useful because the two years were different hourly weather realisations rather than copies of one another.

## 2018 and 2019 were not the same weather sequence

A dedicated comparison used the meteorological state that actually entered the surrogate. Selected findings are shown below.

| Check | Result |
|---|---:|
| Same-calendar wind-speed correlation | 0.043 |
| Same-calendar friction-velocity correlation | 0.145 |
| Same-calendar mechanical mixing-height correlation | 0.123 |
| Median absolute wind-direction difference | 75 degrees |
| Identical full dynamic states at comparable calendar hours | 0 |
| Exact rounded dynamic-state overlap across years | about 0.15% |

The years still share the same broad local climatology. Seasonal temperature and day/night structure are therefore expected to look similar. The correct interpretation is **same-domain temporal generalisation across different hourly meteorology**.

## What improved

The surrogate consistently improved the full field and the longitudinal amplitude response relative to the frozen baseline.

Stable cases were generally easier than convective cases in the two final temporal tests. The remaining convective and tail errors are part of the current research boundary.

## What did not improve enough

Extreme maxima remain a clear weakness.

In 2018, the AERMOD global maximum was about 3.02 in the project C/Q scale, while the surrogate maximum was about 7.11 and occurred at a different case/receptor.

In 2019, the AERMOD global maximum was about 3.10, while the surrogate maximum was about 6.61 and was again located elsewhere.

For that reason, the project does not claim reliable prediction of regulatory extremes or controlling receptors.

## Earlier independent exam

An earlier untouched 2022 test supported the direction of the residual-amplitude architecture: whole-field L1 fell from about 0.21115 to 0.16964, with 119 of 128 cases improving. After that test was opened, 2022 was deliberately reclassified as development evidence and was no longer treated as fresh validation for later model changes.

## Bottom line

The present result is meaningful but narrow. The project has moved beyond proof-of-concept learnability and has shown repeatable improvement on unseen years inside one controlled domain. It has not reached the accuracy or scope needed for a general or regulatory surrogate.
