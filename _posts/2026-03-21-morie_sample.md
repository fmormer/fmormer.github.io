---
layout: post
title: Adaptive CPT Investigation Planning with Reinforcement Learning
image: "/img/posts/morie_sample/morie_sample.png"
tags: [Offshore Floating Wind, Geotechnical Engineering, Artificial Intelligence, Reinforcement Learning, CPT, Site Investigation, Subsurface Modeling, Python]
---

# Celtic Sea Floating Offshore Wind – Adaptive CPT Investigation Planning with Reinforcement Learning

## Executive Summary

This study establishes the **adaptive CPT investigation-planning layer** of Morie Analytics by extending the AI-assisted subsurface reconstruction workflow developed in `morie_subsurface` 
toward sequential decision-making.

The central question is simple:

> Once a sparse subsurface reconstruction workflow exists, where should the next CPT be placed?

In `morie_subsurface`, synthetic geological truth fields were generated, sparsely sampled and reconstructed using SchemaGAN.  
In `morie_sample`, the same sparse-to-dense reconstruction concept is used in a 2D vertical-section setting — referred to here as SchemaGAN-2D — and becomes the environment in which an 
adaptive sampling policy is trained.

The workflow combines:

* GeoSyn synthetic truth fields inherited from `morie_subsurface`
* Sparse CPT-style vertical observations
* SchemaGAN-2D sparse-to-dense reconstruction
* Deep Reinforcement Learning for adaptive CPT placement
* RMSE-based reconstruction assessment
* CPT-count-aware reward formulation
* Validation against matched uniform-spacing baselines

The result is a reproducible framework capable of testing whether a learned policy can improve offshore subsurface reconstruction by selecting CPT locations adaptively, rather than relying 
only on fixed-spacing investigation layouts.

In the current synthetic benchmark, the trained policy produces a statistically significant but practically small improvement over the matched uniform-spacing baseline. This makes the study 
most valuable as a **feasibility demonstration of the adaptive sampling loop**, rather than as a final claim of deployment-ready CPT campaign optimization.


This study represents the transition from:

> AI-assisted reconstruction from sparse CPT data

toward:

> Adaptive investigation planning based on what has already been observed.

> Site intelligence → Layout generation → Soil reconstruction → AI subsurface intelligence → **Adaptive CPT planning** → Mooring physics → Anchor verification → Anchor prediction

<div align="center">
  <img src="/img/posts/morie_sample/morie_sample.png"
       alt="Adaptive CPT investigation planning workflow linking morie_subsurface reconstruction with reinforcement-learning-based sampling"
       width="1000">
</div>

*Figure 1 – Integrated adaptive CPT investigation-planning workflow linking `morie_subsurface` reconstruction fields with reinforcement-learning-based sampling decisions.*

## Project Scope

This study focuses on the adaptive investigation-planning layer of the Morie ecosystem.

The scope includes:

* Adaptive CPT placement
* Reinforcement-learning environment for investigation planning
* Coupling between sparse CPT observations and SchemaGAN-2D reconstruction
* RMSE-based reconstruction assessment after each CPT
* CPT-count-aware reward formulation
* Training and validation of a Deep Q-Learning policy
* Validation against uniform-spacing baselines at matched CPT count
* Initial comparison framework for future non-RL adaptive baselines
* Interpretation of adaptive sampling value under controlled synthetic geology

This first version should be understood as a regional investigation-planning prototype.
It is designed to test adaptive CPT-placement logic over the synthetic Celtic Sea benchmark, rather than to define final anchor-cluster-scale investigation spacing.

The study converts:

**Sparse offshore reconstruction capability → adaptive CPT placement strategy**.

## Engineering Context

Early-stage floating offshore wind developments face a fundamental geotechnical challenge:

> How can site investigation campaigns be planned efficiently when each additional CPT has a significant cost?

In real offshore projects:

* CPT campaigns are expensive
* Investigation density is limited
* Spatial variability is not fully known in advance
* Geological complexity can vary across the lease area
* Engineering decisions are often required before complete site characterization is available

The previous `morie_subsurface` study addressed one side of this problem:

> Can sparse CPT-style observations be reconstructed into engineering-ready subsurface fields?

This study addresses the next question:

> If the reconstruction improves when new CPTs are added, where should those CPTs go?

Rather than prescribing a fixed sampling layout in advance, `morie_sample` explores an adaptive strategy where each new CPT location depends on the information obtained from previous CPTs.

This shifts the investigation problem from a static layout question toward a sequential decision-making problem.

## From `morie_subsurface` to `morie_sample`

`morie_sample` is intentionally separated from `morie_subsurface`.

This separation preserves architectural clarity across the Morie ecosystem.

### `morie_subsurface`

Focuses on:

* Synthetic geological truth generation
* Sparse CPT-style sampling
* SchemaGAN-2D reconstruction
* IC-based engineering parameter derivation
* Reconstruction-quality validation

### `morie_sample`

Focuses on:

* Adaptive CPT placement
* Reinforcement learning
* Investigation efficiency
* Reconstruction improvement after each CPT
* Comparison with uniform-spacing baselines

The relationship can be summarized as:

| Study case         | Main question                                                 | Main output                                            |
| ------------------ | ------------------------------------------------------------- | ------------------------------------------------------ |
| `morie_subsurface` | Can sparse CPT data reconstruct offshore subsurface fields?   | Reconstructed Ic and engineering parameter fields      |
| `morie_sample`     | Where should the next CPT be placed?                          | Adaptive CPT placement policy and validation metrics   |

Together, the two study cases form a unified offshore subsurface intelligence framework.

`morie_subsurface` reconstructs what may exist between sparse CPTs.
`morie_sample` learns where an additional CPT may be most useful.

## Inputs and Data Sources

This study builds directly on upstream Morie Analytics outputs.

### From `morie_subsurface`

* GeoSyn truth Ic fields
* GeoSyn sidecar metadata
* SchemaGAN-2D generator
* Sparse Ic and mask convention
* Celtic Sea three-layer sand-state model
* Ic-based geological convention
* Local grid geometry

The inherited truth fields represent IC values over a 2D grid with:

* 500 columns along the horizontal direction
* 80 vertical rows
* 10 m horizontal spacing
* 0.5 m vertical spacing
* Ic values representative of the synthetic Celtic Sea sand-state model

The `morie_sample` repository consumes these artefacts as read-only inputs.
Nothing in `morie_subsurface` is modified by the adaptive sampling workflow.

### Additional Inputs

The adaptive sampling layer adds:

* DQN agent configuration
* CPT action spacing in physical meters
* Reward weighting parameter
* Training and validation realization splits
* All-realization validation sweep
* Validation metrics and plotting routines

All inputs remain aligned with the same cropped Celtic Sea engineering domain used across the Morie portfolio.


## System Flow

The adaptive sampling workflow can be summarized as:

**GeoSyn Truth Field → Initial CPT → Sparse Ic + Mask → SchemaGAN-2D Reconstruction → Reconstruction Assessment → DQN Action → Next CPT Location → Updated Reconstruction → Reward Signal → Policy Update**

The architecture preserves the following aspects throughout the process:

* Geological traceability
* Engineering scale
* Reproducibility
* Compatibility with `morie_subsurface`
* Direct validation against known synthetic truth

### Processing Workflow

1. Load a GeoSyn truth Ic field inherited from `morie_subsurface`
2. Place the first CPT trace
3. Build the sparse Ic and mask tensors
4. Reconstruct the full Ic field using SchemaGAN-2D
5. Compute the reconstruction RMSE against the known synthetic truth
6. Build a six-feature state vector from the observed Ic traces
7. Select the next CPT spacing using the DQN policy
8. Add the new CPT trace to the sparse input
9. Reconstruct the Ic field again
10. Compute reward based on reconstruction quality and CPT count
11. Repeat until the investigated section boundary is reached
12. Compare the adaptive policy against matched sampling baselines

This converts:

**Sparse CPT traces → reconstructed Ic field → adaptive next-sample decision**.

In this first version, the known GeoSyn truth field is used to compute the reward and validation metrics during synthetic training and benchmarking. In a real investigation campaign, the full subsurface truth would not be available. 
Future deployment-oriented versions should therefore replace truth-based reconstruction error with observable proxies such as reconstruction uncertainty, ensemble disagreement, inter-trace dissimilarity or anchor-capacity uncertainty.


## Local Engineering Domain

The workflow inherits the same cropped Celtic Sea local engineering domain used in `morie_subsurface`.

This ensures continuity across:

* Synthetic geological truth generation
* Sparse CPT-style sampling
* SchemaGAN-2D reconstruction
* Engineering interpretation
* Downstream offshore design workflows

The selected domain preserves:

* Offshore engineering scale
* Sand-dominated layered behavior
* Spatial continuity representative of the controlled synthetic benchmark
* Compatibility with the Morie floating wind portfolio sequence

The current implementation is intentionally 2D and section-based.
It works on vertical Ic sections rather than on a full 3D ground model.

This makes it suitable for developing and validating the adaptive sampling logic before extending the approach toward more complex 3D investigation planning.

## Adaptive CPT Investigation Concept

The main concept of `morie_sample` is that the CPT campaign is not fixed in advance.

Instead, the investigation evolves as new information becomes available.
At each step, the agent observes the latest CPT trace together with information from previously sampled traces.
It then chooses the next horizontal step from a discrete action set.

Each valid action places one new CPT.
The number of CPTs per episode is therefore not prescribed directly.
It emerges from the policy.

A policy that always selects long steps exits the section quickly and produces a sparse investigation campaign.
A policy that always selects short steps produces a denser campaign but pays a higher investigation-cost penalty.

The interesting strategies lie between these two extremes.

In this first implementation, an episode ends when the policy reaches the boundary of the investigated section.
Future versions can introduce an explicit stop action, allowing the model to decide not only where to sample next, but also when the campaign is sufficiently informative.

The adaptive policy must learn when additional spatial resolution is useful and when the reconstruction model already has enough information to infer the remaining field.

<div align="center">
  <img src="/img/posts/morie_sample/rollout_r0004_ep0.png"
       alt="Adaptive CPT rollout showing truth IC sparse CPT input SchemaGAN reconstruction and reconstruction error"
       width="900">
</div>

*Figure 2 – Example adaptive CPT rollout for one GeoSyn realization. The DQN policy selects four CPT locations, the sparse IC traces are passed through the SchemaGAN-2D reconstruction model, and the resulting full-field reconstruction is compared against the known synthetic truth.*

## Reinforcement Learning Environment

The adaptive sampling problem is formulated as a reinforcement-learning environment.

The environment contains:

* A known synthetic truth IC field
* A sparse CPT sampling mask
* A SchemaGAN-2D reconstruction model
* A reward function balancing reconstruction error and CPT count
* A discrete action space expressed in physical meters

At each step, the agent receives a compact state representation based only on IC traces.

The agent does not directly observe the full truth field.
The truth field is only used internally to compute reconstruction error during training and validation.

This is important because it mirrors the engineering problem:

> The decision-maker only has access to the CPTs already collected, not to the full subsurface truth.

The full-field truth is available in this synthetic benchmark so that the adaptive policy can be trained and evaluated quantitatively.

## State, Actions and Reward

### State Vector

The agent observes a six-dimensional state derived from the Ic traces.

The state includes:

| Number  | Feature                                                                    |
| ------- | -------------------------------------------------------------------------- |
|    1    | Mean of the Ic trace at the most recent CPT column                         |
|    2    | Standard deviation of that Ic trace                                        |
|    3    | Mean cosine similarity between the latest IC trace and previous CPT traces |
|    4    | Standard deviation of those cosine similarities                            |
|    5    | Normalized x-position of the latest CPT                                    |
|    6    | Fraction of the CPT budget used                                            |

At this stage, the state is intentionally based only on Ic traces.

The engineering quantities derived in `morie_subsurface`, such as relative density, friction angle and submerged unit weight, are not used in the v0 state.
This keeps the first implementation directly comparable with the reinforcement-learning reference study.

A limitation of this v0 state is that it does not fully encode the spatial arrangement of all previous CPTs. It includes the latest position and similarity to previous traces, 
but it does not explicitly describe whether earlier CPTs are well distributed, clustered or leaving large unsampled gaps.

Future versions can extend the state to include engineering parameters, uncertainty metrics or anchor-relevant quantities.

### Action Set

The action set is declared in physical meters and then converted into grid-column strides using the current horizontal spacing of 10 m.

| Action | Horizontal step | Column stride |
| ------ | --------------- | ------------- |
| 1      | 250 m           | 25 columns    |
| 2      | 500 m           | 50 columns    |
| 3      | 1000 m          | 100 columns   |
| 4      | 1500 m          | 150 columns   |

This is an important adaptation within Morie Analytics.
The agent is not operating in abstract pixel space. It is operating in engineering-relevant physical distances.

In this version, the action set should be interpreted as a regional or pre-FEED investigation-planning configuration. It is not yet intended to resolve detailed anchor-cluster-scale ground model 
development, where smaller investigation spacings may be required. Future configurations could introduce finer actions, for example 50–100 m steps around specific anchor clusters.

### Reward Logic

The reinforcement-learning agent is guided by a reward logic that balances two competing objectives:

* Improve the quality of the reconstructed subsurface field
* Avoid adding CPTs that do not provide enough additional value

After each new CPT is selected, the sparse input is updated and the SchemaGAN-2D model reconstructs the full Ic field again. The quality of this reconstruction is then compared against the known synthetic truth.
The reward logic therefore combines two normalized contributions:

* A reconstruction-quality term, based on the current full-field RMSE
* An investigation-effort term, based on the number of CPTs used

In the Tier-L configuration, the balance is controlled by:

`alpha = 0.6`

This means that reconstruction quality carries slightly more weight than investigation effort, while still penalizing unnecessary CPTs.
If the new CPT helps improve the reconstructed field, the action is favoured. If the policy keeps adding CPTs without meaningful improvement, the investigation-effort penalty becomes more important.
This produces an engineering-relevant trade-off:

> Additional CPTs are useful only if they improve the reconstructed subsurface field enough to justify the extra investigation effort.

In practical terms, the agent is not simply trying to use the fewest possible CPTs, nor is it trying to sample as densely as possible. It is learning a compromise between subsurface reconstruction quality and investigation efficiency.

## SchemaGAN Reconstruction During Rollout

The reinforcement-learning loop is coupled directly with the SchemaGAN-2D reconstruction model developed in `morie_subsurface`.

After each CPT is selected:

1. The new Ic trace is added to the sparse input field
2. The CPT mask is updated
3. The sparse Ic and mask tensors are passed through SchemaGAN-2D
4. The full Ic field is reconstructed
5. The reconstruction is compared against the known GeoSyn truth during synthetic benchmarking
6. The resulting reconstruction assessment contributes to the reward

This means that the agent is not learning an abstract sampling rule.
It is learning through the reconstruction consequences of each CPT location. The value of a CPT is therefore measured by how much it helps reconstruct the full subsurface field.

This is the key link between `morie_subsurface` and `morie_sample`:

* `morie_subsurface` provides the reconstruction engine.
* `morie_sample` uses that engine to evaluate adaptive investigation decisions.

## Training Strategy

The adaptive sampling policy is trained using Deep Q-Learning. During training, the agent repeatedly interacts with the synthetic GeoSyn truth fields inherited from `morie_subsurface`. 
At each episode, the agent selects CPT locations, receives feedback based on reconstruction quality and investigation effort to then gradually update its sampling strategy.

The training process includes:

* Experience replay, so the agent can learn from previous sampling decisions
* A target network, used to stabilize the learning process
* Epsilon-greedy exploration, so the agent initially tests different CPT-spacing strategies before becoming more selective
* Greedy validation after training, where the learned policy is evaluated without exploratory actions

The first extended Tier-L run was trained for 75,000 episodes.The first extended large training configuration, designated Tier-L in the repository, was trained for 75,000 episodes.

During training:

* The exploration parameter decayed toward its lower bound
* The moving-average reward progressively improved
* The number of CPTs per episode reduced from denser early exploration toward compact campaigns
* The learned policy converged toward approximately four CPTs per episode

This training behavior is important from an engineering perspective. At the beginning of training, the agent explores many possible CPT-spacing combinations. 
As training progresses, it learns that dense investigation is not always necessary for the controlled synthetic fields used in this benchmark. 
The final policy therefore tends toward compact CPT campaigns while maintaining reconstruction quality.

The final policy therefore tends toward compact CPT campaigns while maintaining reconstruction quality. This should be interpreted in the context of the current smooth synthetic truth fields, 
where the SchemaGAN-2D reconstruction model reaches a low error level with relatively few informative CPT traces.

<div align="center">
  <img src="/img/posts/morie_sample/training_curves.png"
       alt="Training curves for the 75k episode DQN run showing reward RMSE epsilon decay and number of in-situ tests"
       width="950">
</div>

*Figure 3 – Training curves for the 75k-episode Tier-L run. The moving-average reward stabilizes as exploration decays, while the learned policy progressively shifts toward lower CPT counts and converges toward approximately four in-situ tests per episode.*

## Validation Results: 75k-Episode Tier-L Run

The trained DQN policy was evaluated across 120 GeoSyn truth profiles.

For each profile, the adaptive policy was compared against a uniform-spacing Standard baseline at the same CPT count selected by the policy.

This paired comparison is important. The baseline is not allowed to use more CPTs than the adaptive policy.
Both approaches are evaluated under the same investigation-count constraint.

The validation evaluates:

* Full-field Ic RMSE
* Mean Ic bias
* Percentage of pixels within a selected Ic error band
* Paired comparison between DQN and uniform spacing

The 75k run produced the following summary metrics:

| Metric                |             DRL |        Standard |
| --------------------- | --------------: | --------------: |
| RMSE (IC)             | 0.0456 ± 0.0031 | 0.0462 ± 0.0030 |
| Bias (IC)             | 0.0008 ± 0.0045 | 0.0005 ± 0.0047 |
| PIC — abs(err) ≤ 0.05 |  0.798 ± 0.0200 |  0.790 ± 0.0200 |

Here, PIC refers to the proportion of reconstructed cells where the absolute Ic error is lower than or equal to 0.05.

The adaptive policy produces a lower mean RMSE than the matched uniform-spacing baseline, but the effect is small and not universal at the individual-profile level.

Across the 120-profile sweep:

* DRL gives lower RMSE in 78 profiles
* Uniform spacing gives lower RMSE in 42 profiles
* The mean paired delta, DRL minus Standard, is -6.54e-4 Ic
* The 95% bootstrap confidence interval is [-9.67e-4, -3.43e-4]
* The paired Wilcoxon signed-rank test gives p = 1.34e-4
* The paired t-test gives p = 1.03e-4

These checks support a statistically significant but practically small improvement in the current synthetic benchmark.

This is an important distinction. The result should not be interpreted as a large performance gain. 
Instead, it shows that the adaptive sampling loop can be trained, validated and benchmarked against matched sampling strategies, 
while producing a measurable but limited improvement over uniform spacing under the current smooth synthetic truth fields.

<div align="center">
  <img src="/img/posts/morie_sample/metrics_distributions.png"
       alt="Validation distributions comparing DRL and uniform spacing across RMSE bias and PIC metrics"
       width="1100">
</div>

*Figure 4 – Validation of the trained DRL policy against the matched uniform-spacing Standard baseline across 120 GeoSyn profiles. The adaptive policy produces a slightly lower RMSE distribution, near-zero bias, and a marginally higher percentage of pixels within the selected IC error band.*

The RMSE-vs-CPT-count comparison provides a second view of the same validation exercise.
Because the trained policy converges toward approximately four CPTs, the paired comparisons concentrate around the same investigation count.

In addition to the uniform-spacing Standard baseline, the repository now includes a second non-RL comparator: **MaxGap**. 
This strategy places the next CPT at the midpoint of the largest unsampled gap, providing a simple adaptive baseline that does not require reinforcement learning.

This is useful because uniform spacing is only a first benchmark. A stronger validation set should compare DRL not only against fixed spacing, but also against simple adaptive rules that are easier to implement and explain.


## Engineering Interpretation

The main result is that the adaptive investigation-planning loop works end-to-end:

> CPT selection → Sparse input update → SchemaGAN reconstruction → RMSE evaluation → Reward → next CPT decision.

The trained policy produces a statistically significant but practically small improvement in mean Ic reconstruction error relative to the matched uniform-spacing baseline.

This is an important engineering observation. The result shows that the adaptive workflow can be trained, validated and benchmarked against fixed-spacing investigation strategies. However, the absolute RMSE margin remains small 
and the improvement should not be interpreted as a large performance gain.

The synthetic GeoSyn truth fields used in this first implementation are intentionally controlled. They are smooth, structured and relatively predictable compared with real offshore stratigraphy.

The current truth fields are generated from simplified geological patterns with strong spatial continuity. As a result, the SchemaGAN-2D model can reconstruct the Ic field accurately from a small number of CPT traces.

Once approximately four informative CPTs are available, the reconstruction error approaches a performance ceiling. At that point, the specific placement of the four CPTs still matters, 
but there is limited room for any sampling policy to create a large additional RMSE reduction.

This limitation has three consequences:

* First, reduced heterogeneity can make uniformly spaced CPTs highly competitive with adaptive policies.
* Second, smoother truth fields allow the reconstruction error floor to be reached quickly, shrinking the headroom available for large gains.
* Third, a policy trained only on simplified synthetic regularities may not transfer directly to real site variability without recalibration.

This should not be interpreted as evidence that adaptive sampling has limited value. Instead, it indicates that the current benchmark is relatively easy for the reconstruction model.
In real offshore conditions, the subsurface may include:

* Irregular layer boundaries
* Local erosional or depositional features
* Buried channels
* Sand lenses or interbedded materials
* Mixed soil units
* Abrupt lateral transitions
* CPT measurement noise
* Interpretation uncertainty
* Geological features not captured by smooth harmonic patterns

In such conditions, more CPTs would normally be required to interpret the full stratification reliably. 
The value of adaptive sampling is therefore expected to become more significant as geological complexity increases.

A more complex truth-generation stage would create a more demanding benchmark where the policy must decide whether additional CPTs are needed to resolve features that cannot be inferred 
from smooth geological continuity alone.

The current result should therefore be interpreted as:

* A successful validation of the adaptive sampling workflow
* A demonstration that the DQN policy can learn compact CPT strategies
* A first benchmark against uniform spacing
* An indication that the current synthetic truth fields may underestimate the value of adaptive CPT placement
* A motivation to increase geological complexity in future versions

This is useful because the workflow does more than optimize CPT positions. It also helps diagnose where the limiting factor lies:

> Is reconstruction uncertainty controlled by sampling strategy, by the reconstruction model or by the complexity of the geological truth?

In the current version, the answer appears to be:

> The SchemaGAN-2D model is already strong for the controlled synthetic fields, so the remaining RMSE margin available to adaptive placement is limited.


## Outputs Generated

The workflow produces:

* Trained DQN policy checkpoints
* Episode-level reward histories
* Episode-level Ic RMSE histories
* Exploration decay curves
* CPT-count evolution curves
* Adaptive CPT rollout figures
* Sparse input and reconstruction panels
* Full-field reconstruction error maps
* RMSE-vs-CPT-count validation plots
* Metrics-distribution plots
* Paired comparison metrics against uniform-spacing baselines
* Statistical significance reports for paired validation results
* Comparator outputs for uniform spacing and non-RL adaptive baselines such as MaxGap

These outputs are directly usable for evaluating adaptive investigation strategies.


## Engineering Applications

The outputs support:

* Early-stage CPT campaign planning
* Regional and pre-FEED investigation-density screening
* Sensitivity testing of CPT spacing
* Sparse-data uncertainty reduction studies
* AI-assisted geotechnical interpretation
* Floating offshore wind lease-area investigation strategy
* Benchmarking of adaptive sampling policies
* Future integration with anchor and mooring design workflows

The methodology can support questions such as:

* How many CPTs are needed for a given reconstruction objective?
* Where should the next CPT be placed?
* When does additional sampling stop improving the reconstructed field?
* Is uncertainty controlled by sampling density or by geological complexity?
* How does adaptive sampling compare with uniform spacing?
* How should investigation strategy evolve as new data are collected?
* Which areas would benefit from finer investigation spacing before anchor design?

This enables:

**Sparse Offshore Data → AI Reconstruction → Adaptive Sampling → Engineering Decisions**

At this stage, these applications should be interpreted as decision-support and benchmarking capabilities for early investigation planning. 
Future versions will be needed before the workflow can be used as a deployment-ready tool for final offshore CPT campaign design.


## Relationship to Other Morie Study Cases

This study extends the Morie subsurface workflow from reconstruction into adaptive planning.

### Receives from

* **morie_site** → environmental context
* **morie_layout** → floating wind geometry
* **morie_soil** → deterministic soil reconstruction framework
* **morie_subsurface** → GeoSyn truth fields and SchemaGAN-2D reconstruction model

### Feeds into

* **morie_subsurface** → future active-learning and uncertainty-aware reconstruction extensions
* **morie_anchor** → future anchor engineering studies under improved subsurface interpretation
* **morie_atlas** → lease-scale intelligence and uncertainty screening
* **future investigation-planning workflows** → campaign benchmarking, adaptive sampling and CPT-density studies

It provides the transition from:

> Engineering-aware AI reconstruction

toward:

> Adaptive offshore investigation planning.


## Why It Matters Commercially?

Site investigation is one of the earliest, most expensive and most consequential stages of offshore wind development.

Poorly planned campaigns can lead to:

* Unresolved geotechnical uncertainty
* Conservative design assumptions
* Late-stage redesign
* Inefficient anchor selection
* Increased installation risk
* Additional investigation needs
* Higher project development cost

Adaptive sampling provides a way to evaluate where new information is most valuable.

For floating offshore wind, this is particularly relevant because:

* Lease areas are large
* Anchor locations are spatially distributed
* Soil variability affects anchor feasibility
* Mooring layout and anchor design depend on local ground conditions
* Early-stage decisions are often made under sparse information

The commercial value is not simply reducing the number of CPTs.

The value is improving the relationship between:

> Investigation cost, uncertainty reduction and engineering decision quality.

This is where adaptive geotechnical intelligence becomes useful:

* The subsurface model is updated as information arrives
* The next investigation point is selected based on reconstruction value
* Sampling strategies can be compared before field execution
* Engineering teams can test investigation scenarios under controlled assumptions
* The workflow can eventually support campaign planning at lease scale

In its current form, `morie_sample` is best understood as a decision-support and benchmarking workflow for early-stage investigation planning. 
Future deployment-oriented versions should incorporate real CPT data, uncertainty-aware reward logic, finer action spacing and engineering objectives linked to anchor and mooring design.


## Aspects to Improve

This study is an important step, but several extensions are required before the workflow can support real project-level investigation planning.

Potential improvements include:

* Broader validation on more complex geological truth fields
* Synthetic fields with sharper boundaries and non-harmonic structures
* Buried channels, lenses and discontinuous units
* Mixed soil types including clay, sand and weak rock
* Real CPT calibration using offshore site investigation datasets
* Measurement noise and interpretation uncertainty
* 3D adaptive sampling workflows
* Explicit stop action instead of boundary-based episode termination
* Finer action spacing for anchor-cluster-scale investigation, including 50–100 m steps
* Alternative reward functions based on uncertainty reduction
* Engineering-parameter-based reward channels
* Inclusion of relative density, friction angle and submerged unit weight in the state
* Anchor-capacity-informed reward functions
* Depth-weighted rewards focused on anchor embedment zones
* Integration with campaign cost, vessel logistics and weather-window constraints

A natural next step is to increase geological complexity in the truth-generation stage.

More realistic synthetic fields would create a more demanding benchmark where the adaptive policy must decide whether additional CPTs are needed to resolve features that cannot be inferred 
from smooth continuity alone.

This would move the workflow closer to real offshore investigation planning.


## Design Philosophy

This study reflects the Morie Analytics approach:

* **Adaptive**: the next CPT location depends on what has already been observed.
* **Sequential**: investigation planning is treated as a step-by-step decision process, not as a fixed sampling layout.
* **Engineering-scaled**: actions are expressed in physical meters, not abstract pixels.
* **Reconstruction-driven**: every new CPT is evaluated through its impact on full-field Ic reconstruction.
* **Modular**: the workflow consumes `morie_subsurface` outputs without modifying them.
* **Transparent**: the reward explicitly balances reconstruction accuracy and investigation effort.
* **Benchmarkable**: the adaptive policy is compared against matched uniform-spacing baselines.
* **Interpretable**: RMSE, bias and PIC metrics provide direct reconstruction-quality diagnostics.
* **Extensible**: future tiers can introduce engineering parameters, uncertainty, logistics and explicit stopping rules.
* **Engineering-ready**: the workflow is designed to connect eventually with anchor, mooring and lease-scale decision tools.

The methodology does not treat AI as a black-box replacement for geotechnical judgement.
Instead, it creates a controlled environment where investigation strategies can be tested, compared and improved before being applied to real offshore datasets.


## Research Foundations

The reinforcement-learning methodology presented in this study builds upon the adaptive CPT investigation framework introduced by:

* Bruno Zuada Coelho
* Evangelia Smyrniou
* Fabian A. Campos Montero

*Optimizing geotechnical in-situ site investigations using Deep Reinforcement Learning.*

The upstream reference implementation is CPTSuperLearn.

Within Morie Analytics, the concept is adapted toward:

* Offshore floating wind environments
* Celtic Sea synthetic geological truth fields
* Physical-meter-based CPT actions
* SchemaGAN-2D sparse-to-dense reconstruction
* Mask-aware sparse input representation
* Keras 3 / TensorFlow 2.16 reconstruction coupling
* PyTorch-based DQN training and validation
* Downstream compatibility with Morie geotechnical and offshore design workflows

The case-study contribution is not the DQN algorithm itself.

The contribution is the integration of adaptive CPT planning into the Morie offshore engineering ecosystem:

> GeoSyn truth → SchemaGAN reconstruction → Adaptive CPT policy → Validation against matched sampling baselines → Engineering interpretation.

This establishes the first version of an adaptive geotechnical investigation-planning layer for Morie Analytics.
