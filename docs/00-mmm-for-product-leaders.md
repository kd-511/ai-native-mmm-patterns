# MMM Foundations for Product Leaders

A plain-English, product-oriented guide to Marketing Mix Modeling (MMM). This is for leaders who need to use MMM outputs to make decisions, not to build models.

## Contents
- [What MMM is](#what-mmm-is)
- [What MMM is not](#what-mmm-is-not)
- [What questions MMM answers](#what-questions-mmm-answers)
- [Inputs and outputs (plain English)](#inputs-and-outputs-plain-english)
- [Where MMM works well](#where-mmm-works-well)
- [Where MMM breaks down](#where-mmm-breaks-down)
- [How to interpret results (uncertainty, not a single truth)](#how-to-interpret-results-uncertainty-not-a-single-truth)
- [How MMM pairs with experiments](#how-mmm-pairs-with-experiments)
- [The minimum activation checklist](#the-minimum-activation-checklist)

## What MMM is
MMM is a way to estimate how much each marketing channel contributed to an outcome over time, given historical variation in spend and exposure.

In practice, MMM answers questions like:
- How much incremental lift did channel X likely drive last quarter?
- If we shift budget from channel A to channel B, what is the expected impact and the uncertainty range?
- Which channels are consistently high ROI versus volatile or context-dependent?

MMM is most useful when you need a portfolio view across channels and you cannot run experiments for every decision.

## What MMM is not
MMM is not:
- A guaranteed causal truth machine
- A replacement for experiments
- A precise attribution tool at user-level
- A tool that can safely separate effects that always move together
- A justification engine to back into a predetermined decision

If MMM is treated as a single “correct number,” trust and adoption usually collapse.

## What questions MMM answers
MMM is strong at strategy and planning questions:
- Budget allocation: Where should the next $X go?
- Budget protection: What is the downside risk of cutting $X from a channel?
- Scenario planning: What happens if we rebalance upper funnel vs lower funnel?
- Portfolio insight: Which channels perform consistently across periods?

MMM is weaker for:
- Creative-level optimization
- Short time windows with limited variation
- Questions that require user-level causality or targeting outcomes

A useful discipline is to label each MMM output by decision type:
- Planning decision
- Optimization decision
- Governance decision

Then state whether MMM is primary evidence, supporting evidence, or not appropriate.

## Inputs and outputs (plain English)

### Typical inputs
MMM typically needs time series data with consistent definitions:
- Outcome: sales, conversions, enrollments, leads, volume, revenue, or another business KPI
- Marketing activity: spend and or exposure by channel over time
- Controls: seasonality proxies, pricing, distribution, macro factors, competitor signals when available
- Calendar: holidays, events, launches, policy changes, supply constraints

Quality matters more than quantity. Clean definitions beat more columns.

### Typical outputs
MMM generally produces:
- Contribution estimates: how much each channel likely drove
- ROI or marginal ROI: expected return per additional dollar at the margin
- Response curves: diminishing returns patterns
- Uncertainty intervals: credible ranges, not point certainty
- Scenario simulations: expected outcome under budget shifts

What leaders should ask for in every output:
- The decision context
- The uncertainty range
- The main drivers of the recommendation
- What would change the conclusion

## Where MMM works well
MMM tends to work well when:
- You have enough time history and meaningful variation in spend and exposure
- Channels are measured consistently over time
- There are clear planning cycles where MMM can influence decisions
- You define “what good looks like” for stability across refreshes
- The organization accepts uncertainty as part of decision-making

MMM is strongest as a decision support system, not a post-hoc scoreboard.

## Where MMM breaks down
MMM breaks down when:
- Channels are highly correlated and do not vary independently (identifiability problem)
- Inputs change silently (taxonomy shifts, tracking changes, vendor definition drift)
- The outcome is dominated by unobserved or unstable non-marketing factors (supply constraints, policy changes, access changes)
- The time window is short and marketing signals are weak relative to noise
- Stakeholders demand deterministic answers or treat outputs as a ranking without uncertainty
- The operating model is unclear (no cadence, no governance, no ownership)

If MMM is breaking down, the fix is usually system design and governance, not tuning model parameters.

## How to interpret results (uncertainty, not a single truth)
MMM provides a range of plausible effects, not a single effect. Decisions should consider both expected value and downside risk.

Three practical rules:
1) Treat point estimates as a summary, not the truth
2) Prefer decisions that are robust under uncertainty
3) Escalate when conclusions flip across refreshes without a clear explanation

When you see a big swing, ask:
- Did inputs change?
- Did definitions change?
- Did the model change?
- Did the real world change?

## How MMM pairs with experiments
MMM and experiments are complements.

Experiments are best for:
- isolating causal lift for a specific intervention
- validating incremental impact with high confidence

MMM is best for:
- integrating signals across channels and time
- scenario planning when experiments are slow or limited
- providing a portfolio view and informing where to run experiments next

When MMM and experiments disagree, do not pick a winner:
- verify measurement definitions and time windows
- review model assumptions and diagnostics
- decide whether the discrepancy is expected or a red flag

## The minimum activation checklist
Most MMM failures are activation failures. Use this checklist to make MMM usable.

### A) Define the decision system
- [ ] What decisions will MMM influence this quarter? (budget setting, reallocations, planning scenarios)
- [ ] Who is the decision owner? (single accountable owner)
- [ ] What is the decision cadence? (monthly, quarterly)
- [ ] What is the default action when uncertainty is high? (hold, test, or limit change)

### B) Standardize the outputs
- [ ] One standard MMM report template used every refresh
- [ ] Always include uncertainty intervals and key diagnostics
- [ ] Always include “what changed since last refresh” section
- [ ] A single glossary for channel definitions and metrics

### C) Put governance gates in place
- [ ] Data changes require a logged change note
- [ ] Model configuration changes require review
- [ ] Large swings require an investigation workflow before sharing broadly
- [ ] Clear rules for what can be acted on without escalation

### D) Create the feedback loop
- [ ] Decision log exists (what we decided, why, and expected impact)
- [ ] Outcome tracking exists (what happened vs expected)
- [ ] Quarterly recalibration review (what we learned, what we change)

### E) Define adoption success metrics
Pick 3 to start:
- [ ] Decision coverage: percent of major budget decisions informed by MMM
- [ ] Time-to-decision: time from refresh to signed-off plan
- [ ] Recommendation action rate: percent of recommendations that lead to a decision, not necessarily acceptance
- [ ] Trust stability: frequency of unexplained swings above a threshold
- [ ] Repeat usage: returning stakeholders over 2 planning cycles

### Minimal artifacts you should insist on
- A one-page “refresh memo” per cycle: what changed, why, what is safe to act on
- A definitions page: channels, outcomes, and what is included or excluded
- A decision log: decisions, owners, dates, expected impact, follow-up date

If you have these artifacts, MMM becomes a product. If you do not, MMM becomes a debate club.
