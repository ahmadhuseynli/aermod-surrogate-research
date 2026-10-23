# Development record

This is a compact account of how the project changed as the evidence changed. It is organised by scientific stage rather than by calendar date.

The full working record is much larger and remains in the private research lab.

## Initial controlled surrogate

The first question was intentionally narrow: one elevated point source, SO2, flat terrain and a fixed source configuration.

The first teacher dataset and boosted-tree surrogate were built around hourly C/Q rather than annual summary statistics. Early work compared raw C/Q with a transformed target and tested whether simply increasing model capacity would close the error.

It did not. Longer boosting runs improved the fit but reached diminishing returns. The problem moved from "more trees" toward representation and information content.

## Representation and information limits

Rotation and mirror tests were used to check whether the model had learned avoidable compass-direction artefacts. The work moved toward plume-relative geometry.

A more important result followed: the angular teacher grid was too coarse for some narrow stable plumes. A model cannot recover a plume core that the teacher sampling never resolves properly.

Additional meteorological fields did not remove that problem. The stronger interpretation was that spatial teacher resolution itself had become a limiting factor in the stable regime.

That changed the direction of the project.

## Rebuilding the spatial representation

Crosswind and downwind reconstruction were then tested separately.

Crosswind interpolation improved first. Longitudinal support remained weak. A two-dimensional near-source composition experiment also failed.

The response was targeted spatial densification and better plume-relative geometry, not a larger learner.

## Fresh-year diagnostics

Fresh meteorological years were used as diagnostic exams. Once a year was opened and used to change the model, it was no longer treated as independent validation.

A 2024 test exposed another crosswind-resolution weakness in narrow stable plumes. A 2025 test then showed that much of the remaining error had moved into longitudinal amplitude and dilution.

Those tests became development evidence and led to an amplitude-residual design.

## Residual architecture

An untouched 2022 architecture exam supported the residual-amplitude direction but still showed too much absolute error.

Several more complicated residual models were then tested and rejected. Regime-specific experts, low-dimensional residual predictors and direct lateral corrections did not survive the frozen development gates.

The version that remained used a strongly bounded local residual correction and became the frozen Phase2H prototype.

## Frozen temporal confirmation

The prediction package and scoring rules were fixed before the final year-level concentration truth was opened.

On 2019, whole-field normalised L1 fell from 0.1721767 for the frozen baseline to 0.1312534 for Phase2H, a 23.77% relative reduction. Amplitude error fell by 34.22%.

The same frozen surrogate was then taken into 2018 without retraining. Whole-field normalised L1 fell from 0.1690417 to 0.1272474, a 24.72% relative reduction, while amplitude error fell by 37.14%.

For readability, those final whole-field errors correspond to about **86.9% and 87.3% agreement when expressed as 1 - normalised L1**. That shorthand is tied to this internal metric; it is not a universal accuracy score.

A separate weather-state comparison showed that the two years were not simply copies of the same hourly sequence. Same-calendar wind-speed correlation was 0.043, the median absolute wind-direction difference was 75 degrees, and no comparable calendar hour had an identical full dynamic state.

The global peak remained wrong in both magnitude and location. That failure is kept as part of the result rather than hidden behind the field-average improvement.

## Public research record

The public repository contains the scientific question, selected validation tables, failure history, limitations, roadmap and a technical note.

The large teacher library, trained weights, exact residual library, detailed controller code and complete operational record remain private.

The public record is intended to make the work understandable and auditable without exposing the entire working lab or closing off later IP and commercial decisions.
