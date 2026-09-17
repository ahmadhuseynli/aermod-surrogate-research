# Development record

This page exists because the public GitHub repository is newer than the research itself.

The working project began on **14 August 2026** in a private research workspace. The public repository was created only after the first development cycle had been frozen and written up. I have not changed or backdated Git commit dates to make the public repository look older.

The dates below are taken from contemporaneous project chats, run logs, frozen handoff packages and the private operation history. They are a short public reconstruction, not a replacement for the full laboratory archive.

## 14–17 August 2026 — first controlled surrogate

The first question was intentionally narrow: one elevated point source, SO2, flat terrain and a fixed source configuration. The first teacher dataset and boosted-tree surrogate were built around hourly C/Q rather than annual summary statistics.

Early work compared raw C/Q with a transformed target and tested whether simply increasing model capacity would close the error. It did not. Longer boosting runs improved the fit but reached diminishing returns.

By 17 August the target-robustness work had been completed and the problem had shifted from “more trees” toward representation and information content.

## 18–20 August 2026 — representation and information limits

Rotation and mirror tests were used to check whether the model had learned avoidable compass-direction artefacts. The work moved toward plume-relative geometry.

A more important result followed: the 10-degree angular teacher grid was too coarse for some narrow stable plumes. A model cannot recover a peak that the teacher sampling never resolves properly.

The information-sufficiency campaign completed on 20 August. Its strongest conclusion was not that more meteorological variables were obviously missing; it was that spatial teacher resolution had become a real limiting factor in the stable regime. That changed the next phase of the project.
## September 2026 — fresh-year tests and the residual architecture

The next phase used fresh meteorological years as diagnostic exams. Once a year was opened and used to change the design, it was no longer treated as independent evidence.

A 2024 test exposed another crosswind-resolution weakness in narrow stable plumes. A 2025 test then showed that much of the remaining error had moved into longitudinal amplitude and dilution. Those two years became development evidence.

An untouched 2022 architecture exam supported the residual-amplitude direction, but its absolute error was still too large. Several more complicated residual models were then tried and rejected. The surviving version used a strongly bounded local residual correction and became the frozen Phase2H prototype.

## 12 September 2026 — 2019 one-shot temporal confirmation

The student-side prediction package was sealed before the 2019 AERMOD concentration truth was opened. No retraining, architecture change or truth-dependent applicability-threshold tuning was allowed afterward for the reported result.

Whole-field normalised L1 fell from 0.1721767 for the frozen baseline to 0.1312534 for Phase2H, a 23.77% relative reduction. Amplitude error fell by 34.22%.

The global peak was still wrong in both magnitude and location. That failure was kept as part of the result rather than hidden behind the field-average improvement.

## 14 September 2026 — second confirmation on 2018

The same frozen surrogate was taken into 2018 without retraining. Whole-field normalised L1 fell from 0.1690417 to 0.1272474, a 24.72% relative reduction, while amplitude error fell by 37.14%.

A separate weather-state comparison later showed that 2018 and 2019 were not simply copies of the same hourly sequence: same-calendar wind-speed correlation was 0.043, the median absolute wind-direction difference was 75 degrees, and no comparable calendar hour had an identical full dynamic state.

The correct interpretation remains narrow: repeatable temporal improvement inside the same broad climatological domain.

## 17 September 2026 — public archive

After the first research cycle was documented, a separate public repository was created from the private record. The public archive contains the scientific question, selected validation tables, failure history, limitations and a technical note. The production research workspace remains private.

The GitHub repository creation date is therefore a publication date, not a project-start date. Zenodo preservation was added after the public release so that the archive could be cited permanently.