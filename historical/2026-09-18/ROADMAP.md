# Research roadmap

The current prototype is at a point where another small tuning cycle on the same setup would not tell me much. The next work should test a new scientific boundary.

## 1. Fix the tail before widening the claims

The biggest unresolved issue is the extreme concentration tail. The next step is to understand why the controlling maxima remain unstable without tuning directly to known validation peaks.

A useful improvement here would have to transfer to unseen extremes, not just reduce error on the cases already inspected.

## 2. Move outside the current climatology

The 2018 and 2019 results show temporal transfer inside one broad local climate. A new site or genuinely different meteorological regime would be a much stronger test.

That experiment should be preregistered and kept untouched until the next model is frozen.

## 3. Let the source physics vary

The current source is fixed. A broader engine needs a controlled range of release height, diameter, exit velocity and temperature.

I would rather add those variables deliberately and validate them one at a time than jump immediately to a very wide source space and lose track of where errors come from.

## Later extensions

Only after the three items above are stable would I move into more complicated AERMOD behaviour: terrain, building downwash, multiple sources, other source types, and additional pollutants where the AERMOD treatment is appropriate.
## Longer-term direction

The longer-term idea is a governed simulation loop rather than one permanently fixed training set:

1. generate physically valid scenarios;
2. run AERMOD as the reference model;
3. preserve the physical inputs, outputs and provenance;
4. train the surrogate on hourly fields;
5. identify poorly supported or high-error parts of the state space;
6. run targeted new AERMOD cases there;
7. retrain and repeat.

AERMOD would still remain the verification and regulatory engine. The point of the surrogate is fast prediction inside a domain that has actually been demonstrated, not removing the reference model from the workflow.