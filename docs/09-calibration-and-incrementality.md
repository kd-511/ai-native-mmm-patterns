# Calibration and Incrementality

Your MMM can converge beautifully and still be wrong. Calibration is how you find out before your stakeholders do. Without it, you're shipping confident recommendations based on patterns that may not reflect reality.

This doc defines how to validate MMM outputs against real-world experiments: which calibration methods to use, how to design studies that actually work, what to do when MMM and lift disagree, and how often to recalibrate.

## Contents

- [Why calibration matters](#why-calibration-matters)
- [Incrementality as ground truth](#incrementality-as-ground-truth)
- [Types of calibration experiments](#types-of-calibration-experiments)
- [Designing calibration studies](#designing-calibration-studies)
- [When MMM and lift disagree](#when-mmm-and-lift-disagree)
- [Calibration cadence](#calibration-cadence)
- [Documentation and decision records](#documentation-and-decision-records)

---

## Why calibration matters

MMM estimates relationships from observational data. It finds patterns. It does not prove causation. A model can fit historical data perfectly and still misattribute effects.

**Common failure modes without calibration:**

- Overestimating channels with consistent spend (no variation to learn from)
- Underestimating channels with delayed effects (attribution window too short)
- Confusing correlation with causation (brand spend tracks with seasonality)
- Absorbing effects from unmeasured variables into measured channels

**What calibration provides:**

- Ground truth comparison for key channels
- Confidence bounds on model estimates
- Evidence for stakeholder conversations
- Triggers for model revision

Calibration is not optional. It is the difference between "the model says" and "we know."

---

## Incrementality as ground truth

Incrementality experiments measure the causal effect of marketing by comparing outcomes with and without exposure. They answer: "What would have happened if we hadn't spent?"

**Why incrementality is the gold standard:**

- Establishes causation, not just correlation
- Controls for confounders MMM cannot observe
- Provides point estimates with confidence intervals
- Creates defensible evidence for stakeholders

**What incrementality measures vs what MMM measures:**

| Incrementality | MMM |
|----------------|-----|
| Causal effect of a specific intervention | Average marginal effect over historical period |
| Short-term response (typically) | Short and long-term response (with adstock) |
| Specific context (time, audience, creative) | Generalized across contexts |
| High internal validity | High external validity |

Neither is "right." They measure different things. Calibration uses incrementality to anchor MMM estimates in causal reality.

---

## Types of calibration experiments

Start with the method that fits your constraints. Perfect is the enemy of calibrated.

### Geo experiments

Purpose: measure incrementality by varying spend across geographic regions.

What it does:

- Randomly assigns regions to test (increased/decreased spend) and control (baseline)
- Measures outcome differences between test and control
- Controls for regional variation through matching or randomization

When to use:

- Channel has sufficient regional variation possible
- Outcomes are measurable at geo level
- Enough regions for statistical power

Limitations:

- Spillover between regions (national campaigns, travel)
- Regional heterogeneity in response
- Requires 4-8 weeks minimum for most channels
- Cannot isolate user-level effects

Outputs:

- Incremental lift estimate with confidence interval
- Cost per incremental outcome
- Comparison point for MMM channel estimate

### User-level holdouts

Purpose: measure incrementality by withholding exposure from a random user sample.

What it does:

- Randomly assigns users to exposed vs holdout groups
- Measures conversion differences between groups
- Controls for user-level confounders through randomization

When to use:

- Platform supports user-level targeting and holdouts
- Sufficient conversion volume for power
- Short consideration cycle (results in days/weeks)

Limitations:

- Platform-dependent (not all support true holdouts)
- Cannot measure cross-device or offline effects
- Contamination from other touchpoints
- Often limited to single platform

Outputs:

- Incremental lift percentage
- Confidence interval
- Platform-specific calibration point

### Matched market tests

Purpose: measure incrementality using similar markets as synthetic control.

What it does:

- Identifies market pairs with similar historical patterns
- Applies treatment to one market, holds other constant
- Measures divergence from expected parallel trend

When to use:

- Geo experiments not feasible (too few regions)
- Need longer measurement window
- Historical data available for matching

Limitations:

- Matching quality affects validity
- Parallel trends assumption may not hold
- Single pair = no confidence interval without bootstrapping
- External shocks can invalidate

Outputs:

- Estimated incremental effect
- Match quality diagnostics
- Sensitivity analysis on assumptions

### Synthetic control methods

Purpose: construct a weighted combination of control units to match treated unit's pre-period.

What it does:

- Uses optimization to find control weights
- Projects counterfactual for treatment period
- Measures gap between actual and synthetic control

When to use:

- Single treated unit (market, region)
- Rich pre-period data available
- Multiple potential control units

Limitations:

- Requires good pre-period fit
- Sensitive to donor pool selection
- Inference requires permutation tests
- Assumes no spillover to control units

Outputs:

- Point estimate of treatment effect
- Placebo tests for inference
- Pre-period fit diagnostics

### Platform lift studies

Purpose: use platform-provided measurement tools for incrementality.

What it does:

- Leverages platform's randomization infrastructure
- Typically ghost ads or PSA holdouts
- Measures conversion lift within platform

When to use:

- Quick directional read needed
- Platform is significant spend
- Internal resources for experiments limited

Limitations:

- Platform marks its own homework
- Methodology often opaque
- May not match your conversion definition
- Cross-platform effects invisible

Outputs:

- Platform-reported lift metrics
- Confidence intervals (if provided)
- Directional calibration input

---

## Designing calibration studies

Bad experiments waste money and create false confidence. Design matters.

### Statistical power

Before running any experiment, calculate required sample size.

What to specify:

- Minimum detectable effect (MDE): smallest lift worth detecting
- Baseline conversion rate: expected rate in control
- Significance level (alpha): typically 0.05
- Power (1-beta): typically 0.80

Rule of thumb: if you need to detect a 5% lift, you need far more samples than if you're looking for 20% lift. Be realistic about what effect size matters for decisions.

**Power calculation outputs:**

- Required sample size per group
- Required duration given traffic
- Feasibility assessment (is this experiment worth running?)

### Duration

Most experiments run too short.

**Minimum duration considerations:**

- Full weekly cycle (capture day-of-week effects)
- Consideration cycle for product (days for impulse, weeks for considered)
- Adstock decay period (if measuring lagged effects)
- Enough conversions for statistical power

**Typical durations:**

| Channel type | Minimum duration |
|--------------|------------------|
| Paid search (branded) | 2 weeks |
| Paid search (non-brand) | 3-4 weeks |
| Paid social | 3-4 weeks |
| Display/programmatic | 4-6 weeks |
| TV/streaming | 6-8 weeks |
| Brand campaigns | 8-12 weeks |

### Avoiding contamination

Contamination kills experiments. Plan for it.

**Common contamination sources:**

- Cross-device exposure (user in holdout exposed on another device)
- Organic spillover (word of mouth from exposed users)
- Geographic spillover (travel, national media)
- Concurrent campaigns (other channels running during test)
- Seasonality shifts (test period not representative)

**Mitigation strategies:**

- Use geographic boundaries that limit spillover
- Exclude border regions from analysis
- Document concurrent marketing activity
- Run during "typical" periods when possible
- Use intent-to-treat analysis to handle contamination

### Cost and feasibility

Every experiment has a cost. Make it explicit.

**Direct costs:**

- Lost revenue from holdout (no exposure = fewer conversions)
- Media waste in over-spend conditions
- Operational cost of setup and monitoring

**Feasibility checklist:**

- [ ] Platform supports required targeting
- [ ] Sufficient volume for statistical power
- [ ] Duration fits business calendar
- [ ] Stakeholder buy-in for holdout
- [ ] Measurement infrastructure ready
- [ ] Resources for analysis and interpretation

If an experiment isn't feasible, don't run a underpowered version. Use a different method or accept wider uncertainty bounds.

---

## When MMM and lift disagree

They will disagree. This is not a bug. It's information.

### Common causes of disagreement

**MMM overestimates, lift is lower:**

- MMM absorbing effects from correlated unmeasured variables
- Insufficient variation in historical spend (MMM extrapolating)
- Adstock specification too long (attributing delayed unrelated conversions)
- Reverse causality (spend follows demand, not drives it)

**MMM underestimates, lift is higher:**

- Lift study captured short-term only, MMM includes long-term
- Lift context was unusually favorable (new creative, promo period)
- MMM data quality issues dampening signal
- Priors too skeptical for channel

**Inconclusive or wide intervals:**

- Experiment underpowered
- High variance in outcomes
- Contamination in experiment
- MMM has wide posteriors (also uncertain)

### Investigation protocol

When disagreement surfaces, follow this sequence:

1. **Check the experiment first**
   - Was it adequately powered?
   - Was there contamination?
   - Was the period representative?
   - Were there concurrent factors?

2. **Check the MMM second**
   - What's the MMM uncertainty for this channel?
   - Is there enough spend variation in training data?
   - Are priors reasonable for this channel?
   - Any data quality issues?

3. **Compare apples to apples**
   - Is lift measuring same outcome as MMM?
   - Is time period comparable?
   - Is channel definition identical?
   - Are there lag differences?

4. **Document and decide**
   - Record findings in calibration log
   - Decide whether to update MMM priors
   - Decide whether to rerun experiment
   - Communicate uncertainty to stakeholders

### Updating MMM with calibration data

When lift provides credible new information, incorporate it.

**Options for incorporating lift:**

- **Informative priors:** Use lift estimate to set prior mean and variance for channel coefficient
- **Calibration targets:** Add soft constraint that posterior should be consistent with lift
- **Hierarchical structure:** Pool lift estimates across similar channels/markets
- **Posterior validation:** Compare posterior to lift as diagnostic, don't force agreement

**When NOT to force agreement:**

- Lift study was underpowered or compromised
- Lift context was non-representative
- MMM has strong evidence from other sources
- Disagreement is within overlapping uncertainty bounds

---

## Calibration cadence

Calibration is not a one-time event. Markets change. Channels evolve. Models drift.

### Recommended cadence

| Calibration type | Frequency | Trigger |
|------------------|-----------|---------|
| Major channel lift study | Annually | Planned roadmap item |
| Quick platform studies | Quarterly | Directional checks |
| Ad-hoc validation | As needed | Major model changes, stakeholder questions |
| Full recalibration | 18-24 months | Model rebuild or major market shift |

### Triggers for unscheduled calibration

Run calibration outside normal cadence when:

- Model estimates diverge significantly from prior version
- Stakeholder challenges specific channel estimate
- Major market change (new competitor, economic shift)
- Channel strategy changes significantly (new creative, new audience)
- Platform changes measurement methodology

### Building calibration into the roadmap

Calibration competes with features for resources. Protect it.

**Roadmap strategies:**

- Allocate fixed percentage of measurement budget to calibration
- Tie major model releases to calibration requirements
- Build lift studies into campaign planning (not afterthought)
- Create calibration SLA (e.g., each major channel calibrated every 18 months)

---

## Documentation and decision records

Calibration is worthless if findings aren't captured and used.

### Calibration study log

Maintain a running log of all calibration activities.

**Required fields:**

| Field | Description |
|-------|-------------|
| Study ID | Unique identifier |
| Channel | Channel calibrated |
| Method | Geo, holdout, platform, etc. |
| Date range | Test period |
| Lift estimate | Point estimate |
| Confidence interval | 80% or 95% CI |
| MMM estimate | Comparable MMM output |
| Agreement | Yes/No/Partial |
| Action taken | Prior update, none, further investigation |
| Owner | Who ran it |
| Notes | Context, caveats, limitations |

### Decision record template

When calibration leads to a decision, document it.

```
## Calibration Decision Record

**Date:** [Date]
**Channel:** [Channel]
**Study:** [Study ID or description]

### Findings
[What did calibration show?]

### Comparison to MMM
[How did it compare? Agreement or disagreement?]

### Investigation
[What did you check? What did you find?]

### Decision
[What action was taken? Why?]

### Stakeholder communication
[Who was informed? What was the message?]

### Follow-up
[Any planned next steps?]
```

### Stakeholder communication

Calibration builds trust when communicated well.

**What to share:**

- We run ongoing validation (shows rigor)
- Results were consistent / inconsistent with model (transparency)
- Here's what we did about it (accountability)
- Here's our confidence level now (appropriate uncertainty)

**What not to share:**

- Every minor discrepancy (creates noise, not trust)
- Technical details without context (confuses more than clarifies)
- Unresolved disagreements without a plan (opens can of worms)

---

## Checklist

Before shipping any MMM to stakeholders, confirm:

- [ ] At least one major channel has been calibrated with incrementality
- [ ] Calibration results are documented in study log
- [ ] Disagreements have been investigated and resolved or explained
- [ ] Priors reflect calibration where appropriate
- [ ] Calibration cadence is on the roadmap
- [ ] Stakeholders know calibration exists and what it means
