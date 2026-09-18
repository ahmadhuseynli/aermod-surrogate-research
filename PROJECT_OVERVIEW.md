# Project overview

## The idea

AERMOD can calculate hourly concentration fields from source, meteorological and receptor inputs. That is exactly what makes it useful, but it also means that large scenario libraries and repeated sensitivity work can become computationally heavy.

The question behind this project is whether a separate surrogate can learn that response well enough to reproduce the hourly field quickly **inside a clearly validated domain**.

The goal is not to make a black-box replacement for AERMOD. The more useful long-term architecture is:

**AERMOD as teacher and verification engine -> surrogate for fast in-domain prediction -> AERMOD again whenever the case is uncertain or outside the validated support**

That could make repeated environmental modelling much faster while keeping the reference physics model in control of the evidence.

## What the surrogate learns

I did not train the model only on annual maxima or a few summary statistics. The main target is the hourly receptor field itself.

In shorthand:

**source + meteorological state + plume-relative receptor geometry -> surrogate -> hourly concentration field**

For the first prototype, concentration is normalised by emission rate where that proportionality is physically valid, so the learner can focus on dispersion behaviour rather than relearning a simple linear scaling.

## Why the first case is small

The first prototype uses one fixed elevated point source, SO2, flat terrain and no downwash, chemistry or deposition. That is obviously much smaller than the full AERMOD problem. It is deliberate.

With the source physics fixed, a bad result is easier to diagnose. I can ask whether the problem came from the meteorology, the target, receptor geometry, spatial sampling or the learner itself instead of mixing all of those with terrain and source-type effects.

That choice paid off. One of the biggest problems turned out not to be machine-learning capacity at all; it was the spatial resolution of the teacher field.

## What changed during development

**Plume-relative geometry.** A flat homogeneous plume should rotate with the wind. The representation therefore moved away from unnecessary absolute compass direction and toward downwind/crosswind coordinates.

**Teacher resolution.** The early angular receptor layout looked adequate until narrow stable plumes were examined closely. It could miss the plume core, which meant the surrogate was being asked to learn information that was not represented properly in the teacher sampling.

**Fresh-year diagnostics.** Independent yearly checks did not simply confirm the model. They exposed new weaknesses: first crosswind resolution, then longitudinal amplitude and dilution. Once those tests were used to change the design, they became development evidence rather than being recycled as untouched validation.

**A bounded residual layer.** Several more complicated successor ideas were tested and rejected. The version that survived used a strongly constrained local residual correction on top of the main field prediction. That became the Phase2H prototype reported here.

## What the present evidence supports

The same frozen surrogate was evaluated on 2019 and 2018 after the prediction package and scoring rules had been fixed.

Whole-field normalised L1 was 0.13125 and 0.12725 respectively. Written as **1 - normalised L1**, that is about **86.9-87.3% whole-field agreement on this internal metric**.

Relative to the frozen baseline surrogate, field error improved by 23.77% and 24.72%, while amplitude error improved by about 34-37%.

That is useful evidence of temporal transfer inside the same broad site/climate domain. It is not yet evidence for a new climate, a new source family, complex terrain or building downwash.

The extreme tail is also still weak. The largest modelled peaks and their locations were not reproduced reliably in the two final year tests.

## What this could grow into

If the next validation stages succeed, the same core idea could support much larger environmental-modelling workflows.

The most useful extensions would be:

- a controlled range of stack heights, diameters, exit velocities and temperatures;
- different meteorological regimes and sites;
- terrain and building downwash;
- multiple sources and broader receptor fields;
- active-learning loops that ask AERMOD for new simulations where the surrogate is weak;
- a formal applicability layer that separates high-confidence predictions from cases that need verification.

Only after those scientific boundaries are demonstrated would it make sense to build faster operational tools around the model.

The immediate asset is still the dispersion engine itself: a reproducible mapping from physical inputs to hourly AERMOD-type concentration response.
