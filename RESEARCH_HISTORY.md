# Research history

This was not a clean sequence of successful models. Most of the useful changes came after something failed in a way that could be isolated.

For the dated version of the story, see [`DEVELOPMENT_RECORD.md`](DEVELOPMENT_RECORD.md). This page is more about what changed scientifically.

## First attempt: increase model capacity

The first boosted-tree surrogate learned a meaningful part of the hourly response, so the obvious next test was to train longer and add capacity.

That helped, but not enough. The improvement flattened out. It became hard to justify another round of “more trees” when the remaining error looked structured rather than random.

## Compass direction was the wrong frame

The early feature set still carried unnecessary absolute-direction information. In flat homogeneous terrain the plume should rotate with the wind, so the representation was changed toward plume-relative downwind and crosswind coordinates.

Rotation and mirror checks were useful here because they exposed whether the model had learned directional artefacts that should not have existed physically.

## Then the teacher grid failed

A 10-degree angular receptor grid was too coarse for some narrow stable plumes. The important point was that this was not something a better learner could fix. If the plume core falls between sampled directions, the missing spatial information is already gone before machine learning starts.

That result changed the project more than another small accuracy gain would have. The next work focused on whether the AERMOD field was being represented finely enough to be learnable at all.
## Cartesian plume geometry

The next experiments treated crosswind and downwind interpolation as scientific tests in their own right. Crosswind reconstruction looked promising first. Longitudinal coverage did not. After that, a two-dimensional near-source composition test failed as well.

The response was targeted densification, not a larger neural or boosting model. The project was still trying to remove representation error before blaming the learner.

## Fresh 2024: another spatial problem

When 2024 was opened as a fresh check, narrow stable plumes exposed another weakness in the crosswind support. That was disappointing, but useful. The geometry was refined and 2024 was immediately treated as spent development evidence.

I did not reuse the repaired 2024 result later as if it were still an untouched validation year.

## Fresh 2025: the problem moved

The 2025 check showed a different pattern. The main remaining error was no longer primarily lateral shape. Longitudinal amplitude and dilution were now the clearer weakness.

That finding led to an amplitude-residual layer rather than another wholesale change to receptor geometry.

## 2022: architecture exam, not final proof

A pooled residual architecture was frozen and tested on 2022. It improved 119 of 128 cases and reduced overall field error by about 19.7%.

That was enough to support the direction, but not enough to call the problem solved. After the result was opened, 2022 joined the development set of evidence.

## Several plausible ideas did not survive

Regime-specific residual experts, low-dimensional residual predictors and direct lateral corrections were all tried. They did not improve robustly enough under the frozen development gates to justify replacing the simpler design.

The surviving model used a strongly bounded local residual correction. That became Phase2H.
## 2019 and 2018: same frozen model, two one-shot tests

Phase2H was then taken into 2019 and 2018 without retraining. Whole-field error improved by 23.77% and 24.72% respectively relative to the frozen baseline, while amplitude error improved by roughly 34–37%.

The weather-state audit showed that the two years were not repeating the same hourly sequence, although they remain part of the same broad climatology.

The global maxima were still wrong in magnitude and location. That is the main reason I treat this as a useful research milestone rather than a finished surrogate engine.

## Why the project paused here

At this point, another small round of tuning on the same source and climate would add less scientific value than expanding one boundary cleanly. The next serious tests should address the extreme tail, a different site/climate and variable source physics.

The public repository was opened only after this point. Its creation date is therefore later than much of the work described above.