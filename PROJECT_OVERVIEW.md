# Project overview

## What I was trying to find out

The project started with a fairly practical question. AERMOD can generate an hourly concentration field, but running large numbers of cases repeatedly is slow. Could a separate surrogate learn the AERMOD response well enough to reproduce that field quickly for new cases inside a known domain?

I did not want to train on annual maxima or a handful of summary statistics. The main target from the start was the hourly receptor field itself.

In shorthand:

**source + meteorological state + plume-relative receptor geometry → surrogate → hourly concentration field**

AERMOD is the teacher in this work. It remains the verification model and, where formal regulatory modelling is required, the regulatory model.

## Why I kept the first case small

The first prototype uses one fixed elevated point source, SO2, flat terrain and no downwash, chemistry or deposition. That is obviously much smaller than the full AERMOD problem. It was deliberate.

With the source physics fixed, a bad result is easier to diagnose. I can ask whether the problem came from the meteorology, the target, receptor geometry, spatial sampling or the learner itself instead of mixing all of those with terrain and source-type effects.

That choice paid off quite early. One of the biggest problems turned out not to be machine-learning capacity at all; it was the spatial resolution of the teacher field.
## The main things that changed the project

**Plume-relative geometry.** A flat homogeneous plume should rotate with the wind. I therefore moved away from absolute compass direction and toward downwind/crosswind coordinates.

**Teacher resolution.** The early 10-degree angular receptor layout looked adequate until narrow stable plumes were examined closely. It was not. The grid could miss the plume core, which meant the surrogate was being asked to learn information that was not represented properly in the teacher sampling.

**Fresh-year diagnostics.** Later tests on 2024 and 2025 did not simply confirm the model. They exposed new weaknesses: first crosswind resolution, then longitudinal amplitude and dilution. Those years were subsequently treated as development evidence rather than reused as untouched validation.

**A bounded residual layer.** After several successor ideas failed, the model that survived used a strongly constrained local residual correction on top of the main field prediction. That became the Phase2H prototype reported here.

## What the present evidence supports

The same frozen surrogate was evaluated on 2019 and 2018 after the prediction package and scoring rules had been fixed. Relative to the frozen baseline, whole-field normalised L1 improved by 23.77% in 2019 and 24.72% in 2018.

That is useful evidence of temporal transfer inside the same broad site/climate domain. It is not yet evidence for a new climate, a new source family, complex terrain or building downwash.

The extreme tail is also still weak. The largest modelled peaks and their locations were not reproduced reliably in the two final year tests.

## About the dates in this repository

The research began in the private lab on 14 August 2026. This public repository was opened on 17 September 2026 after the first cycle had been frozen and documented. The public commit history therefore starts later than the research history. [`DEVELOPMENT_RECORD.md`](DEVELOPMENT_RECORD.md) gives the dated trail from the underlying project record.