# AI-Native MMM Patterns

The operating manual for building Marketing Mix Models that people actually trust and use.

This repo is for product managers, data scientists, and measurement leads who are tired of MMM programs that produce beautiful models and zero decisions. It covers what works, what breaks, and the patterns that keep measurement systems stable at scale.

**Author:** [Karan Dhir](https://www.linkedin.com/in/karandhir/) · Building decision-grade AI systems · Previously Amazon, Walmart
**Writing:** [Decision-Grade AI on Substack](https://substack.com/@karandhir)

---

## TL;DR

MMM estimates the incremental impact of marketing channels and helps allocate budget. Modern MMM is Bayesian, refreshable, and designed to work as a product with governance, monitoring, and clear activation paths.

Most MMM programs fail in activation, not modeling. This repo focuses on the operational layer that turns models into decisions.

---

## Start Here (By Role)

### Product Managers
You own the system. Start with these:

| Doc | What you'll learn |
|-----|-------------------|
| [00 - MMM for Product Leaders](docs/00-mmm-for-product-leaders.md) | What MMM is, where it works, where it doesn't |
| [01 - Activation and Governance](docs/01-activation-and-governance.md) | Planning cadence, signoffs, decision workflows |
| [11 - Stakeholder Communication](docs/11-stakeholder-communication-guide.md) | How to present results without losing the room |
| [13 - Build vs Buy](docs/13-build-vs-buy-mmm.md) | Meridian vs Robyn vs vendors vs custom |

### Data Scientists
You build the models. Start with these:

| Doc | What you'll learn |
|-----|-------------------|
| [02 - Failure Modes](docs/02-failure-modes-of-mmm.md) | Why MMM programs fail and how to prevent it |
| [03 - Stability Layer](docs/03-stability-layer.md) | Drift metrics, guardrails, refresh governance |
| [09 - Calibration and Incrementality](docs/09-calibration-and-incrementality.md) | How to validate MMM with experiments |
| [04 - Data Contracts and Lineage](docs/04-data-contracts-and-lineage.md) | Contracts, monitoring, versioned transforms |

### Measurement / Analytics Leads
You bridge technical and business. Start with these:

| Doc | What you'll learn |
|-----|-------------------|
| [05 - Trust-by-Default Reporting](docs/05-trust-by-default-reporting.md) | Standard reports, diagnostics, uncertainty display |
| [12 - Cross-Channel Measurement](docs/12-cross-channel-measurement.md) | Why numbers don't add up and what to do about it |
| [10 - Privacy-First Measurement](docs/10-privacy-first-measurement.md) | What works when cookies die |
| [06 - Closed-Loop Decision Systems](docs/06-closed-loop-decision-systems.md) | Decision logging, outcome evaluation |

### Engineering / MLOps
You keep it running. Start with these:

| Doc | What you'll learn |
|-----|-------------------|
| [07 - MLOps Onboarding](docs/07-mlops-onboarding-for-mmm.md) | Certification, release gates, observability, runbooks |
| [08 - Agentic Workflows](docs/08-agentic-workflows-for-mmm.md) | Agent roles, guardrails, approvals, audit trails |
| [04 - Data Contracts and Lineage](docs/04-data-contracts-and-lineage.md) | Contracts, monitoring, versioned transforms |

---

## What This Repo Covers

### Core Operating Model
How to run MMM as a product, not a project.

- [00 - MMM for Product Leaders](docs/00-mmm-for-product-leaders.md) - Concepts, use cases, limitations
- [01 - Activation and Governance](docs/01-activation-and-governance.md) - Planning cadence, signoffs, decision workflows
- [02 - Failure Modes](docs/02-failure-modes-of-mmm.md) - Instability, drift, trust breaks, decision disconnects
- [06 - Closed-Loop Decision Systems](docs/06-closed-loop-decision-systems.md) - Decision logging, outcome evaluation, recalibration

### Stability and Trust
How to keep the system trustworthy over time.

- [03 - Stability Layer](docs/03-stability-layer.md) - Drift metrics, guardrails, refresh governance
- [05 - Trust-by-Default Reporting](docs/05-trust-by-default-reporting.md) - Standard reports, diagnostics, uncertainty display
- [09 - Calibration and Incrementality](docs/09-calibration-and-incrementality.md) - Validating MMM with experiments, geo tests, lift studies
- [11 - Stakeholder Communication](docs/11-stakeholder-communication-guide.md) - What to claim, handling objections, executive summaries

### Technical Foundations
How to build and maintain the infrastructure.

- [04 - Data Contracts and Lineage](docs/04-data-contracts-and-lineage.md) - Contracts, monitoring, diffable transforms
- [07 - MLOps Onboarding](docs/07-mlops-onboarding-for-mmm.md) - Certification, release gates, observability, runbooks
- [08 - Agentic Workflows](docs/08-agentic-workflows-for-mmm.md) - Agent roles, guardrails, approvals, audit trails

### Ecosystem and Landscape
How MMM fits into the broader measurement world.

- [10 - Privacy-First Measurement](docs/10-privacy-first-measurement.md) - Post-cookie measurement, clean rooms, what still works
- [12 - Cross-Channel Measurement](docs/12-cross-channel-measurement.md) - Double-counting, walled gardens, MMM as arbiter
- [13 - Build vs Buy](docs/13-build-vs-buy-mmm.md) - Meridian, Robyn, PyMC, vendors, decision framework

---

## Why This Exists

MMM is having a renaissance. Privacy changes made user-level attribution unreliable. Open-source frameworks (Robyn, Meridian) lowered the barrier. Bayesian methods improved uncertainty quantification.

But most MMM programs still fail. Not because the models are bad. Because:

- Numbers swing between refreshes and stakeholders lose trust
- Nobody knows who owns the system or what to do when it breaks
- Results are presented without uncertainty and then miss
- There's no connection between model outputs and actual decisions
- The model sits in a notebook while planning happens in spreadsheets

This repo is the operational layer that prevents those failures.

---

## What MMM Actually Is

MMM answers: "Given what we spent across channels over time, how much did each channel contribute?"

**Most useful when:**
- Experiments are limited or too slow for every question
- You need a portfolio view across channels
- You want scenario planning, not just reporting

**Not useful when:**
- You need real-time optimization (MMM is strategic, not tactical)
- You have no historical data
- Spend doesn't vary enough to learn from

**MMM is not:**
- A perfect causal truth machine
- A replacement for experiments
- A tool that can safely answer questions your data cannot support

---

## Why Bayesian

Modern MMM is Bayesian because:

- **Uncertainty is explicit.** You get ranges, not false precision.
- **Priors encode knowledge.** You can incorporate calibration from experiments.
- **Stability is a feature.** Regularization prevents overfitting to noise.
- **Refresh behavior is predictable.** Small data changes don't cause wild swings.

If your MMM doesn't report uncertainty, it's lying to you politely.

---

## Common Failure Modes

| Failure | What happens | What prevents it |
|---------|--------------|------------------|
| Refresh volatility | Numbers swing, leaders stop believing | Stability layer, guardrails, governance |
| No calibration | Model is confident but wrong | Incrementality tests, lift studies |
| Reporting confusion | Outputs aren't comparable, caveats buried | Standard reports, consistent diagnostics |
| Activation failure | Insights exist, decisions don't change | Decision workflows, closed-loop evaluation |
| Stakeholder distrust | "The model must be wrong" | Communication patterns, uncertainty display |
| Data drift | Upstream changes break outputs | Data contracts, monitoring, lineage |

Each of these has a doc that addresses it in detail.

---

## Principles

This repo is:

- **Tool-agnostic.** Patterns apply whether you use Robyn, Meridian, PyMC, or a vendor.
- **Operationally focused.** More about running systems than building models.
- **Written for practitioners.** By someone who's shipped this, not theorized about it.
- **Safe to share.** No proprietary data or internal systems.

This repo is not:

- An MMM math tutorial
- A recommendation for a specific stack
- A way to automate decisions without accountability

---

## Full Doc Index

| # | Doc | Focus |
|---|-----|-------|
| 00 | [MMM for Product Leaders](docs/00-mmm-for-product-leaders.md) | Foundations, use cases, limitations |
| 01 | [Activation and Governance](docs/01-activation-and-governance.md) | Planning cadence, signoffs, workflows |
| 02 | [Failure Modes](docs/02-failure-modes-of-mmm.md) | What breaks and why |
| 03 | [Stability Layer](docs/03-stability-layer.md) | Drift, guardrails, refresh governance |
| 04 | [Data Contracts and Lineage](docs/04-data-contracts-and-lineage.md) | Contracts, monitoring, transforms |
| 05 | [Trust-by-Default Reporting](docs/05-trust-by-default-reporting.md) | Standard reports, diagnostics |
| 06 | [Closed-Loop Decision Systems](docs/06-closed-loop-decision-systems.md) | Decision logging, outcome evaluation |
| 07 | [MLOps Onboarding](docs/07-mlops-onboarding-for-mmm.md) | Certification, release gates, runbooks |
| 08 | [Agentic Workflows](docs/08-agentic-workflows-for-mmm.md) | Agent roles, guardrails, approvals |
| 09 | [Calibration and Incrementality](docs/09-calibration-and-incrementality.md) | Validation, experiments, lift studies |
| 10 | [Privacy-First Measurement](docs/10-privacy-first-measurement.md) | Post-cookie, clean rooms, privacy |
| 11 | [Stakeholder Communication](docs/11-stakeholder-communication-guide.md) | Presenting results, handling objections |
| 12 | [Cross-Channel Measurement](docs/12-cross-channel-measurement.md) | Double-counting, walled gardens |
| 13 | [Build vs Buy](docs/13-build-vs-buy-mmm.md) | Meridian, Robyn, vendors, decisions |

---

## Related Writing

This repo is the technical reference. For the narrative version, see the [Decision-Grade AI series on Substack](https://substack.com/@karandhir):

- What I Learned Shipping AI Systems That Can't Be Wrong
- How to Build Evaluation Gates for AI Decision Systems
- When to Kill an AI Roadmap
- Beyond the Prompt: Why Bayesian Thinking Is the Missing Layer for Agentic AI
- Why "Human-in-the-Loop" Is Not a Safety Strategy
- The Stability Problem in AI Decision Systems
- Your Model Isn't Drunk, It Just Looks That Way
- Governance Is Not a Dirty Word (But Most of It Is Useless)
- The Decision-Grade Stack: A Framework

---

## Contributing

PRs and issues welcome. If you have a production story, include:

- What happened
- How it was detected (or missed)
- The pattern that would have prevented it
- The artifact you recommend (metric, gate, checklist, report section, runbook step)

---

## License

MIT. Use it, adapt it, make it better.
