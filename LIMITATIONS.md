# Limitations

This page is here because the boundaries matter as much as the headline result.

## What the current evidence actually covers

The reported prototype is limited to:

- one fixed elevated point source;
- SO2 treated as a passive pollutant for this experiment;
- flat/rural terrain;
- no building downwash;
- no chemistry or deposition;
- one broad site climatology;
- controlled plume-relative receptor geometry.

That is the domain in which the current evidence should be read.

## What has not been demonstrated

I have not yet shown that the surrogate transfers reliably to a different site or climate, a broad range of stack conditions, complex terrain, building downwash, multiple interacting sources, other source types, or reactive/deposition cases.

Those are future experiments, not implied capabilities of the current model.

## The peak problem

The largest remaining technical concern is the extreme tail. Whole-field error improves, but the highest concentration can still be substantially wrong and can occur at the wrong receptor.

For an operational or regulatory application that is a serious limitation. If the controlling tail cannot be trusted, AERMOD still has to be used for the decision.

## Applicability is not a guarantee

The project includes a support-distance measure that checks whether a query resembles the development data. It is useful, but it is not a promise of small error. Some difficult cases remain in parts of the input space that look well supported.

I therefore treat applicability as one layer of evidence rather than an automatic pass/fail accuracy certificate.

## About the reported percentages

There are two different percentages in the public summary.

The approximately **87% whole-field agreement** is simply **1 - the final normalised-L1 error** in the two untouched year-level tests. It is an intuitive restatement of that internal field metric.

The **23.77% and 24.72%** figures are the relative reductions in that error compared with the earlier frozen baseline surrogate.

Neither is a universal "model accuracy" claim. They do not measure agreement with real ambient monitoring data, and strong field-average performance does not remove the known peak problem.

## Regulatory position

The surrogate is not an approved replacement for AERMOD. Formal regulatory work should continue to use the required approved model, inputs and procedures.

This is an independent research project and is not affiliated with, sponsored by or endorsed by the U.S. EPA.
