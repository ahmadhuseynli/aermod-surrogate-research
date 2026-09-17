# Methodology

This page describes the public version of the method. The full experiment code, training assets and model weights remain in the private research lab.

## 1. Reference model

AERMOD is used as the teacher. The surrogate is trained to reproduce the reference model's hourly concentration response, not observed ambient concentration in the real atmosphere.

That distinction matters. The first scientific objective is **AERMOD emulation inside a restricted domain**.

## 2. Target

The main target is hourly concentration normalised by emission rate, C/Q, where the linearity assumption is valid for the controlled prototype.

A logarithmic transform was used during learning to reduce the effect of the very large dynamic range between near-zero and plume-centre concentrations while preserving an invertible path back to C/Q.

## 3. Meteorology

The teacher cases use processed meteorological states from the AERMOD/AERMET workflow. Validation is grouped by time rather than randomly splitting receptor rows. That prevents the same meteorological hour from appearing in both training and test sets through different receptors.

## 4. Geometry

Early experiments used a polar/angular receptor layout. That representation failed to resolve some narrow stable plumes. The project therefore moved to plume-relative Cartesian geometry using downwind and crosswind coordinates.

A sequence of interpolation experiments was used before fitting the final surrogate. The purpose was to separate spatial representation error from machine-learning error.

## 5. Surrogate structure

The current public description is intentionally high level. The frozen prototype combines:

- a field model based on gradient-boosted decision trees;
- plume-relative physical features;
- a learned longitudinal amplitude correction;
- a bounded local residual correction derived only from development data;
- a separate support-distance calculation used to describe applicability.

The exact production feature set, residual library and model weights are not included in this public release.

## 6. Validation discipline

The project follows three practical rules:

1. A year used to change the model is no longer treated as independent validation.
2. Student predictions are sealed before teacher concentration truth is opened for a fresh test year.
3. Applicability thresholds are fixed without using the validation-year concentration error.

This is stricter than a random train/test split and is necessary because receptor rows from the same hour are highly related.

## 7. Error measures

The main public metric is whole-field normalised L1 error. Additional diagnostics include amplitude error, stability-regime performance, plume-shape error and extreme-peak behaviour.

No single metric is treated as sufficient. A model can improve average field error while still fail at the largest peak, which is exactly what the current prototype does.

## 8. Applicability

The system assigns support classes based on distance from the frozen development support in a truth-free state space. These classes are useful context, not guarantees of accuracy.

The project does not currently claim that support distance alone explains all large errors.
