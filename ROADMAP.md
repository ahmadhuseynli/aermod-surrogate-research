# Research roadmap

The current prototype is paused at a natural boundary. The next work should expand the science, not just add another small model tweak.

## Near term

### 1. Peak and tail behaviour

Understand why the highest concentrations are still poorly reproduced. The goal is not to force the current model to match a few known maxima, but to identify a representation or modelling approach that transfers to unseen extremes.

### 2. New independent site or climate

The 2018 and 2019 tests show temporal transfer inside the same broad climatology. A different site would test a much stronger form of generalisation.

### 3. Variable source physics

Move from one fixed stack to a bounded range of release height, diameter, exit velocity and temperature. This is necessary before the surrogate can be described as a source-general engine.

## Later

- complex terrain;
- building downwash;
- multiple point sources;
- other source types;
- additional pollutants where the AERMOD treatment is appropriate;
- adaptive AERMOD simulation design focused on weak or uncertain regions;
- stronger uncertainty and out-of-domain calibration.

## Long-term architecture

The intended end state is a governed simulation factory:

1. generate physically valid scenarios;
2. run AERMOD as the reference model;
3. preserve inputs, outputs and provenance;
4. train a surrogate on hourly fields;
5. identify high-error or poorly supported regions;
6. generate targeted new teacher cases;
7. repeat until the validated domain is broad enough for the intended use.

AERMOD would remain the fallback and regulatory engine even if the surrogate becomes accurate enough for routine operational prediction.
