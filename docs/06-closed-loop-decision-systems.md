# Closed-Loop Decision Systems

Marketing Mix Modeling only improves if decisions are tracked and evaluated. Without a closed loop, MMM becomes a recurring argument: new refresh, new debate, same lack of learning.

This doc defines the operating system for turning MMM into a learning system: decision logging, outcome measurement, recalibration cadence, a learning agenda, and stopping rules that prevent endless churn.

## Contents
- [Decision logging (what was decided, when, and why)](#decision-logging-what-was-decided-when-and-why)
- [Linking decisions to outcomes](#linking-decisions-to-outcomes)
- [Recalibration cadence](#recalibration-cadence)
- [Learning agenda](#learning-agenda)
- [Stopping rules and evidence thresholds](#stopping-rules-and-evidence-thresholds)

---

## Decision logging (what was decided, when, and why)

If you cannot point to decisions MMM influenced, you do not have adoption. If you cannot reproduce the decision context later, you cannot learn.

A decision log is the minimum artifact that makes MMM real.

### What a good decision log captures
Minimum fields:
- decision ID
- decision type (budget shift, channel mix, scenario selection, test plan)
- date and planning cycle
- decision owner and approvers
- what was decided (plain language)
- why it was decided (MMM evidence + other evidence)
- scenario selected (baseline and chosen scenario)
- expected impact range (not a point estimate)
- key assumptions and constraints
- what to monitor (leading indicators)
- follow-up date and evaluation owner
- link to the refresh memo and report pack

### Decision log anti-patterns
- logging only the outcome, not the rationale
- logging point estimates without uncertainty
- logging after the fact with no follow-up date
- “we discussed it” instead of “we decided it”

If it is not logged, it did not happen.

---

## Linking decisions to outcomes

The goal is not to prove MMM is perfect. The goal is to learn whether MMM-guided decisions improve outcomes within expected ranges.

### How to link decisions to outcomes (practical)
1) Define the outcome and measurement window
- what outcome matters (revenue, conversions, enrollments, leads)
- what time window you expect to see impact
- what leading indicators you will watch earlier

2) Define the counterfactual expectation
- baseline expectation (status quo scenario)
- expected lift range under the chosen decision
- the downside risk range

3) Track actuals vs expected range
- actual outcome in the window
- compare against expected range, not a single number
- classify: within range, above range, below range

4) Record confounders
- supply constraints, pricing changes, launches, policy changes, macro shifts
- anything that plausibly explains divergence

### The key idea
Evaluation is about whether reality landed inside the forecasted uncertainty, and what changed when it didn’t.

---

## Recalibration cadence

Recalibration is the difference between a system that improves and a system that repeats the same mistakes.

Default cadences:
- Monthly: log review and drift review (operational)
- Quarterly: decision outcome review + model/reporting adjustments (planning)
- Semi-annual: governance and taxonomy review (structural)

### What gets recalibrated
- thresholds and guardrails (what counts as a swing)
- comparability rules (what is treated as non-comparable)
- scenario library (which scenarios are decision-ready)
- reporting patterns (what gets summarized, what gets quarantined)
- data contracts and mappings (what definitions need hardening)

Recalibration is not “tune the model.” It is “improve the operating system.”

---

## Learning agenda

A learning agenda makes MMM strategic instead of reactive.

It is a short list of questions you want to answer over the next 1–2 planning cycles, with an explicit plan for evidence.

### What a good learning agenda includes
For each learning question:
- the decision it will influence
- the hypothesis (what you expect and why)
- the evidence required (MMM only, MMM + experiment, MMM + other)
- the measurement window and success criteria
- the next action if confirmed
- the next action if not confirmed

Examples:
- Is channel X truly incremental at current spend levels, or saturating?
- Does upper funnel spend change downstream conversion rates over 4–8 weeks?
- Are we seeing diminishing returns in a specific geography or segment?

A learning agenda prevents two bad outcomes:
- random “insight chasing”
- political “prove my channel works” requests

---

## Stopping rules and evidence thresholds

Without stopping rules, MMM turns into constant churn: endless refresh debates, endless analysis requests, and no decisions.

Stopping rules define when to act, when to hold, and when to escalate.

### Evidence thresholds (practical)
Define thresholds for:
- action-ready recommendations
- “needs more evidence”
- “do not infer”

Examples of action-ready conditions:
- recommended move remains beneficial across plausible ranges
- downside risk is acceptable and explicitly acknowledged
- results are comparable and diagnostics are clean (Info gate)
- decision owner agrees the decision is reversible or testable

Examples of “needs more evidence” conditions:
- identifiability is low and rank-order is unstable
- outcomes are highly sensitive to assumptions
- data drift or taxonomy changes reduce comparability

Examples of “do not infer” conditions:
- contract failures or major taxonomy changes unmapped (Block gate)
- results are not reproducible
- uncertainty intervals are too wide to support decisioning

### Stopping the debate
A good system has a default path:
- If action-ready: decide and log
- If needs evidence: define the evidence plan and timeline
- If do not infer: quarantine and fix inputs before re-engaging

The win is not perfect attribution. The win is faster, safer decisions with continuous learning.

---

If you implement decision logging, outcome linking, recalibration, a learning agenda, and stopping rules, MMM becomes a decision system that improves over time instead of a recurring argument.
