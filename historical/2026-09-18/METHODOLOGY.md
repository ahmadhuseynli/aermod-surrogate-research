# Methodology

This is the public description of the method. The full training assets, run machinery and model files are still kept in the private research workspace.

## Reference model

AERMOD is the teacher. The surrogate is being trained to reproduce AERMOD's hourly response inside a restricted domain; it is not being trained against measured ambient concentration.

That distinction is important. The first question is whether AERMOD itself can be emulated reliably enough for fast prediction, not whether the surrogate is a better model of the atmosphere.

## Target

For the controlled prototype I used concentration normalised by emission rate, C/Q, where that proportionality is valid. A log transform was used during learning because the field spans a very large range from near-zero values to the plume core.

The transform is reversible. The final quantity of interest remains the hourly concentration response.

## Meteorological splitting

Rows from the same meteorological hour are not independent simply because they belong to different receptors. For that reason, I did not rely on a random row-level train/test split.

Development and validation were separated by meteorological time blocks and, later, by entire years. The 2019 and 2018 confirmation tests were opened only after the reported surrogate and scoring rules had been fixed.

## Geometry

The first receptor representation used an angular/polar layout. It failed for narrow stable plumes because the angular spacing was too coarse to resolve the plume core consistently.

The project then moved to plume-relative Cartesian coordinates: downwind distance and crosswind distance. Before fitting the final surrogate, I used interpolation experiments to check whether the spatial representation itself was capable of reconstructing the teacher field. That step was useful because it separated a geometry problem from a learner problem.
## Surrogate structure

The public description is intentionally less detailed than the private implementation. At a useful level, the frozen Phase2H prototype combines:

- a gradient-boosted field model;
- meteorological and plume-relative physical features;
- a learned correction for longitudinal amplitude/dilution;
- a strongly bounded local residual correction built from development data only;
- a separate distance-to-support calculation for applicability context.

The exact production feature list, residual library and trained weights are not part of this release.

## Validation rules

A few rules became non-negotiable as the project matured.

1. Once a year has been inspected and used to change the model, it is no longer called fresh validation.
2. For a fresh year, the student-side prediction package is sealed before the AERMOD concentration truth is opened.
3. Applicability thresholds are fixed without looking at the validation-year concentration error.

Those rules are why 2022, 2024 and 2025 appear in the development history but not as untouched confirmation for the final reported model.

## What I measure

Whole-field normalised L1 is the main public summary metric. I also track amplitude error, stability-regime behaviour, plume shape and the extreme tail.

The last point matters because a field-average score can improve while the controlling maximum is still wrong. That is exactly the current situation: Phase2H improves the field overall, but it is not yet reliable at the largest peaks.

## Applicability

The project has a truth-free support-distance measure that says how similar a query is to the development support. I treat that as context, not as a guarantee. Some difficult cases remain inside apparently well-supported parts of the input space.