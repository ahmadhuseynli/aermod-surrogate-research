# Results

## Two untouched year-level checks

The same frozen Phase2H surrogate was scored on 2019 and 2018. Neither year was used to tune that frozen model before its first evaluation.

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

The two final whole-field errors are therefore around 12.7-13.1% on the frozen normalised-L1 metric. For a more intuitive reading, **1 - normalised L1 is about 87% in both years**.

I use that only as a plain-language description of this metric. It is not classification accuracy, it is not a universal measure of plume quality, and it is not agreement with measured ambient concentrations.

The two relative improvements are also close in size, which is encouraging, but the years come from the same broad site climatology. I do not treat this as evidence for a different climate or site.

## Were 2018 and 2019 just the same weather again?

No. A separate comparison used the meteorological state that actually entered the surrogate.

| Check | Result |
|---|---:|
| Same-calendar wind-speed correlation | 0.043 |
| Same-calendar friction-velocity correlation | 0.145 |
| Same-calendar mechanical mixing-height correlation | 0.123 |
| Median absolute wind-direction difference | 75 degrees |
| Identical full dynamic states at comparable calendar hours | 0 |
| Exact rounded dynamic-state overlap across the two years | about 0.15% |

The right description is therefore **same-domain temporal generalisation across materially different hourly meteorology**.

## Where the improvement came from

The clearest repeatable gain was in the field as a whole and in longitudinal amplitude/dilution. That is consistent with the error mechanism identified during development.

This does not mean every regime improved equally. Convective cases and the far tail remain more difficult than the centre of the distribution.

## The uncomfortable part: the global peaks

The largest concentrations are still a problem.

In 2018 the AERMOD global maximum was about 3.02 in the project C/Q scale. Phase2H produced about 7.11, and the maximum occurred at a different case/receptor.

In 2019 the AERMOD maximum was about 3.10. Phase2H produced about 6.61, again at a different location.

That is why I do not claim reliable prediction of the controlling receptor or the regulatory extreme tail. A model can show strong whole-field agreement and still be unsuitable for a peak-driven decision.

## Earlier architecture exam

Before the final Phase2H freeze, an untouched 2022 test was used as an architecture exam. Whole-field L1 fell from about 0.21115 to 0.16964 and 119 of 128 cases improved.

Once that result had been opened, 2022 became development evidence. It was not reused later as a fresh test for revised models.

## What the numbers mean

There are two different ideas in the public result:

1. **Absolute field agreement:** the final normalised-L1 values are about 0.127-0.131, or roughly 87% when written as 1 - L1.
2. **Improvement over the previous frozen surrogate:** the new model reduced whole-field error by about 24% and amplitude error by about 34-37%.

Neither number should be read as agreement with the real atmosphere. AERMOD is the teacher in this experiment.

The present result is useful because the same model produced similar field performance on two unseen yearly meteorological sequences without truth-dependent retraining. It is still a narrow result, and the peak failure is part of it.
