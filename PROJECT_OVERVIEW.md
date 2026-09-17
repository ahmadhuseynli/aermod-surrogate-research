# Project overview

## The question

AERMOD can produce detailed hourly concentration fields, but repeated model execution becomes expensive when the number of meteorological states, receptors or scenarios grows. This project asks whether a separate surrogate can learn the reference model's response well enough to make fast predictions inside a known and validated domain.

The goal is not to train on annual maxima or a few summary statistics. The target is the hourly concentration field itself.

In simple form:

**source + meteorology + receptor geometry -> surrogate -> hourly concentration field**

AERMOD is used as the teacher and remains the reference for verification and regulatory work.

## Why the first scope is deliberately small

The project started with one elevated point source, SO2, flat terrain and no downwash, chemistry or deposition. Keeping the source physics fixed made it possible to separate one question from many others: can the atmospheric and spatial response be learned at all?

That small scope also made failures easier to diagnose. A poor result could be traced to meteorology, geometry, target design, spatial resolution or the learner instead of being mixed together with terrain, multiple source types and other complications.

## Main research themes

### 1. Teacher data

AERMOD is treated as a physics-response generator. Teacher runs preserve the link between environmental state, receptor geometry and the resulting hourly concentration.

### 2. Plume-relative geometry

A homogeneous flat-terrain plume should rotate with the wind. The project therefore moved away from absolute compass direction and toward plume-relative downwind and crosswind coordinates.

### 3. Spatial resolution

An important early result was that a coarse angular receptor grid could not resolve narrow stable plumes. This was a teacher-representation problem, not simply a machine-learning problem. The project moved to a denser Cartesian plume-relative representation as a result.

### 4. Field structure

Instead of treating every receptor independently, the project explored a factorised view of the plume: the atmospheric state controls a compact field structure, while spatial geometry determines how that structure is sampled.

### 5. Residual error

Later fresh-year tests showed that much of the remaining error came from longitudinal amplitude and dilution. The current prototype therefore uses a base field model with a bounded residual correction rather than relying on a single unconstrained learner.

### 6. Fresh validation

Years used to design the model are not reused as fresh evidence. The current frozen prototype was evaluated on 2019 and then 2018 only after the model and evaluation rules had been fixed.

## What the project has shown so far

The present evidence supports a narrow statement: within the same broad site and source domain, the frozen surrogate improved the full AERMOD concentration field by roughly 24% relative to its frozen baseline on two untouched meteorological years.

The project has not shown that the model transfers to a different climate, different source family, complex terrain, building downwash or regulatory peak prediction.
