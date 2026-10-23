# Atmospheric Dispersion Surrogate Research

[![Archived research DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.22819727.svg)](https://doi.org/10.5281/zenodo.22819727)

Research status, 23 October 2026: **closed as a practical no-go for the proposed generic AERMOD surrogate product**.

I started this project to find out whether a separately trained model could reproduce AERMOD's hourly concentration fields quickly enough, and reliably enough, to become useful for repeated dispersion calculations. I wanted the computational engine itself to be the useful product. AERMOD would remain the reference for scientific verification and for any formal regulatory application.

The work went well beyond the first model. It included controlled source-physics experiments, meteorological and receptor representations, frozen year-level tests, independent-applicability work, Gen2 physical-domain extensions, Gen3 regulatory-style routing studies, a sequence of predictive challenges through V16, and a final October 2026 review of the remaining failure mechanisms. The conclusion is now that the current approach has not delivered the generalization, trustworthy controlling concentrations, useful coverage or demonstrated end-to-end speed required for the intended product. The project is not being presented as an active route to commercial deployment.

The complete explanation, including the negative experiments, the results that genuinely held up, and the final stop decision, is in [Closing the atmospheric dispersion surrogate research programme](RESEARCH_CLOSURE_2026-10-23.md). The corresponding public account is on the [research website](https://ahmadhuseynli.github.io/aermod-surrogate-research/).

## Why the early work was encouraging

The first controlled problem used one elevated point source, passive sulfur dioxide, flat terrain and a defined receptor geometry. The model learned the hourly concentration response normalized by emissions where that was physically appropriate. Early experiments showed that brute-force increases in learner capacity could not fix defects in the spatial information presented to it. An angular receptor grid missed some narrow stable plume cores. Moving to plume-relative coordinates, better spatial sampling and a tightly bounded amplitude correction improved the field predictions.

The frozen Phase2H model subsequently gave whole-field normalized L1 of 0.1272474 in 2018 and 0.1312534 in 2019. Those were 24.72% and 23.77% reductions against the frozen baseline surrogate, with accompanying amplitude-error reductions of 37.14% and 34.22%. Earlier public pages described roughly 87% whole-field agreement because they expressed the particular normalized-L1 statistic as one minus L1. That was never a universal accuracy measure or a comparison with real ambient measurements. In both years the largest peak was materially overpredicted and occurred at the wrong case or receptor. The earlier numbers remain valid as restricted-domain research results, but they do not imply a reliable engineering product.

## What prevented the result becoming a usable engine

Subsequent governed work expanded the scientific questions rather than quietly modifying the frozen Phase2H model. Gen2 Stage24C closed with a bounded research capability, not with a demonstrated generic replacement product. Gen3 then asked whether an actual complete scenario could be safely assigned to a surrogate rather than sent back to AERMOD.

The E04 five-year evaluation did not finish and remained paused. The E04S one-year applicability screen identified substantial out-of-domain routing for the tested sources, so no teacher-truth accuracy result was claimed. In E04A, a day-level design accepted zero, two or 132 of 1,460 scenario-days depending on the frozen scope. The planned hybrid result would have been dominated by AERMOD fallback and the branch closed before the reserved concentration truth was opened. These were important feasibility failures, not interchangeable prediction-error tests.

The later V8–V16 experiments challenged field representations and inference models on already-spent research populations. Several truth-assisted reconstructions showed that the field could be described well if its amplitude, width or peaks were already known. That did not mean those quantities could be predicted from the inputs available when a new case arrived. The trained factor models continued to fail difficult weather regimes and tail checks.

In the terminal V16 direct neural-field test, the model passed ten of ten frozen criteria on a blocked 2019 holdout but only two of ten on the selected 2025 transfer cases. Its transfer relative whole-field L1 was 0.525702 and its low-wind relative field L1 was 3.228091. The severe-error fraction was 70.31% across those 64 selected cases, with plus 50.65% aggregate bias. The selected 2025 set was already-spent development evidence, not a random annual sample or a new untouched confirmation set.

The October review found a real neural input problem: the training observations used 10-metre wind-reference height while the transfer observations used 7.9 metres, and the learned model had never trained the weight direction for that feature. A controlled height-column diagnostic cut the overall relative field L1 to 0.243881 but still passed only six of ten gates. This partial repair did not create a validated model and could not explain earlier tree-model failures. The same review found that V16 still encoded fixed stack settings rather than the variable source physics needed for the original generic objective. A narrow fixed-stack rescue was considered but left unqualified because untouched confirmation, meteorological independence, geometry alignment and available resources were not established.

## What this result means

The science did yield useful findings about teacher-grid resolution, stable plume reconstruction, amplitude and dilution, the difference between oracle representation and predictive learnability, year-to-year feature support, applicability fallback and the proper handling of spent validation truth. Those lessons are worth retaining, particularly because many attractive intermediate scores could otherwise be mistaken for completion.

They do not amount to evidence that a commercially viable and independently validated generic surrogate exists. Nor do the failures prove that no surrogate could ever reproduce AERMOD over any possible restricted problem. The defensible conclusion is narrower: the approach tested here has reached a practical stop for the product it was meant to deliver. No V17 architecture search or further tuning under the same closed formulation is authorized.

The older [development record](DEVELOPMENT_RECORD.md), [historical results](RESULTS.md), [research history](RESEARCH_HISTORY.md), [methodology](METHODOLOGY.md) and [provenance record](EVIDENCE_AND_PROVENANCE.md) are retained so readers can examine the earlier stages without pretending that the later negative evidence never happened. The [October 2026 closure](RESEARCH_CLOSURE_2026-10-23.md) supplies the current interpretation. Frozen Gen1 and Gen2 model assets and the private governed experiment record remain untouched.

The [Zenodo project record](https://doi.org/10.5281/zenodo.22819727) and [original technical note](https://ahmadhuseynli.github.io/aermod-surrogate-research/assets/AERMOD_SURROGATE_TECHNICAL_NOTE_v0.1.pdf) document an earlier release of this ongoing-at-the-time research. They should be read together with this dated closure, not as statements of the project's present status.

This independent research is not affiliated with or endorsed by the United States Environmental Protection Agency. No tested surrogate is claimed to be approved for regulatory use. Where formal procedures require AERMOD, AERMOD remains the reference model.
