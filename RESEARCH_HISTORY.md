# Research history

This was not a clean sequence of successful models. Most of the useful changes came after something failed in a way that could be isolated.

This page focuses on what changed scientifically rather than on calendar dates.

## First attempt: increase model capacity

The first boosted-tree surrogate learned a meaningful part of the hourly response, so the obvious next test was to train longer and add capacity.

That helped, but not enough. The improvement flattened out. It became hard to justify another round of "more trees" when the remaining error looked structured rather than random.

## Compass direction was the wrong frame

The early feature set still carried unnecessary absolute-direction information. In flat homogeneous terrain the plume should rotate with the wind, so the representation was changed toward plume-relative downwind and crosswind coordinates.

Rotation and mirror checks were useful here because they exposed whether the model had learned directional artefacts that should not have existed physically.

## Then the teacher grid failed

An angular receptor grid was too coarse for some narrow stable plumes. The important point was that this was not something a better learner could fix. If the plume core falls between sampled directions, the missing spatial information is already gone before machine learning starts.

That result changed the project more than another small accuracy gain would have. The next work focused on whether the AERMOD field was being represented finely enough to be learnable at all.

## Cartesian plume geometry

The next experiments treated crosswind and downwind interpolation as scientific tests in their own right. Crosswind reconstruction looked promising first. Longitudinal coverage did not. A two-dimensional near-source composition test also failed.

The response was targeted densification, not a larger neural or boosting model. The project was still trying to remove representation error before blaming the learner.

## Fresh yearly diagnostics

A fresh 2024 check exposed another crosswind-resolution weakness in narrow stable plumes. The geometry was refined and that year was then treated as spent development evidence.

The 2025 check showed a different pattern. The main remaining error was no longer primarily lateral shape. Longitudinal amplitude and dilution were now the clearer weakness.

That finding led to an amplitude-residual layer rather than another wholesale change to receptor geometry.

## Architecture exam

A pooled residual architecture was frozen and tested on 2022. It improved 119 of 128 cases and reduced overall field error by about 19.7%.

That supported the direction, but the absolute error was still too large to call the problem solved. Once the result was opened, 2022 joined the development evidence.

## Several plausible ideas did not survive

Regime-specific residual experts, low-dimensional residual predictors and direct lateral corrections were all tried. They did not improve robustly enough under the frozen development gates to justify replacing the simpler design.

The surviving model used a strongly bounded local residual correction. That became Phase2H.

## Final same-domain temporal checks

Phase2H was then taken into 2019 and 2018 without retraining.

Whole-field normalised L1 was 0.13125 and 0.12725. In the simple form **1 - normalised L1**, the two fields correspond to about **86.9% and 87.3% agreement on this internal metric**.

Relative to the frozen baseline, whole-field error improved by 23.77% and 24.72%, while amplitude error improved by roughly 34-37%.

The weather-state audit showed that the two years were not repeating the same hourly sequence, although they remain part of the same broad climatology.

The global maxima were still wrong in magnitude and location. That is the main reason I treat this as a useful research milestone rather than a finished surrogate engine.

## Why the project paused here

Another small tuning cycle on the same source and climate would add less scientific value than expanding one boundary cleanly.

The next serious tests should address the extreme tail, a genuinely different meteorological/site regime and variable source physics.

The public repository is a cleaned scientific record of this work. The full working laboratory, teacher library and model artifacts remain private.
