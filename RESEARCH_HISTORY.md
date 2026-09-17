# Research history

The useful part of this project is not a straight line of successful models. Several failures changed the direction of the work.

## August 2026 - start small

The project began with one fixed elevated point source and a simple question: can a surrogate learn the hourly AERMOD field at all?

Initial boosted-tree experiments showed that the response was learnable, but simply adding more trees gave diminishing returns.

## Directional representation

Absolute compass direction was replaced with plume-relative geometry. In flat homogeneous terrain this is physically more sensible because the plume should rotate with the wind rather than learn a preference for north, south, east or west.

## The first major failure: spatial resolution

A 10-degree angular teacher grid looked convenient but was too coarse for narrow stable plumes. Increasing model capacity could not recover information that was not present in the spatial sampling.

This shifted the project from “find a better ML model” to “make sure the teacher representation is actually resolvable.”

## Cartesian plume geometry

The next phase studied crosswind and downwind interpolation directly. Crosswind reconstruction worked well, but downwind coverage and then two-dimensional near-source coupling failed in separate experiments.

Those failures led to targeted densification rather than a larger learner.

## Fresh 2024 check

A new meteorological year was opened after the representation had been frozen. It exposed another narrow-stable-plume problem: the development crosswind spacing was still too coarse.

Because the 2024 result had now been inspected, that year was treated as spent development evidence. The geometry was refined, but the repaired design was not called “independently validated” on the same year.

## Fresh 2025 check

The next fresh year showed that the dominant remaining error was not mainly lateral shape. It was longitudinal amplitude and dilution.

That result led to an amplitude-residual layer rather than another wholesale geometry change.

## Untouched 2022 exam

A pooled residual architecture was frozen and then tested on 2022. It improved 119 of 128 cases and reduced overall field error by about 19.7%. That supported the architectural direction, but the remaining absolute error was still too large.

After the test, 2022 became development evidence.

## Residual architecture campaign

Several plausible follow-on models were tried and rejected. Regime-specific experts, low-dimensional residual predictors and direct lateral corrections did not survive the frozen development gates.

The model that did survive used a strongly shrunk local residual correction. That became the final Phase2H prototype.

## Untouched 2019 and 2018 tests

Phase2H was then evaluated without retraining on 2019 and 2018. Whole-field error improved by 23.77% and 24.72% respectively against the frozen baseline.

A separate meteorological audit showed that the two years had materially different hourly states even though they came from the same broad site climatology.

## Current pause

The project has answered the first narrow question well enough to stop micro-tuning the same setup. The next useful step should expand one scientific boundary at a time rather than continue making small changes to the existing prototype.
