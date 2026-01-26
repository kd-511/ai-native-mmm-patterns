# MLOps Onboarding for MMM

MMM breaks when it is treated like an analysis instead of a production system. The fastest way to lose trust is to ship refreshes that are not reproducible, not monitored, and not governed.

This doc is a practical onboarding guide for operating MMM like production ML: certification before shipping, release gates, reproducibility by default, monitoring across data and model health, and runbooks for when things break.

## Contents
- [Certification checklist (pre-ship)](#certification-checklist-pre-ship)
- [Release gates (block / warn / info)](#release-gates-block--warn--info)
- [Reproducibility (versioned inputs, configs, outputs)](#reproducibility-versioned-inputs-configs-outputs)
- [Monitoring (data health + model health)](#monitoring-data-health--model-health)
- [Runbooks (what to do when things break)](#runbooks-what-to-do-when-things-break)

---

## Certification checklist (pre-ship)

Certification means: this MMM refresh is safe to publish and safe to use for decisions.

A certification checklist should be fast, repeatable, and enforced. It is not a one-time document.

### A) Data readiness (must pass)
- [ ] all critical inputs present (outcome, spend/exposure, mappings, controls)
- [ ] data contracts validated (schema, keys, required fields)
- [ ] freshness SLA met (or exception logged)
- [ ] coverage within thresholds (no silent drops)
- [ ] mapping/taxonomy version confirmed and diff reviewed
- [ ] backfills/restatements identified and comparability impact assessed

### B) Run readiness (must pass)
- [ ] run is reproducible from versioned inputs and versioned config
- [ ] run artifacts generated (report pack, diagnostics, change log)
- [ ] compute environment/version is recorded (so reruns match)

### C) Model readiness (must pass)
- [ ] required diagnostics generated (not optional)
- [ ] identifiability warnings reviewed and “do not infer” zones labeled
- [ ] uncertainty outputs present (intervals, downside risk)
- [ ] stability deltas vs last refresh assessed (within thresholds or explained)

### D) Decision readiness (must pass for planning releases)
- [ ] scenarios generated for decisions on the calendar
- [ ] recommended moves include expected range + downside risk
- [ ] executive summary drafted (one page, decision-grade)
- [ ] gate status assigned (Info/Warn/Block) with owner and timestamp

Certification should take minutes, not days. The point is discipline, not bureaucracy.

---

## Release gates (block / warn / info)

Treat MMM refreshes like releases. Gates prevent “shipping surprises.”

### Block (cannot publish)
Use Block when the release is not trustworthy or not reproducible:
- broken data contract or missing critical inputs
- major taxonomy/mapping change without versioning and review
- run not reproducible from versioned inputs/configs
- severe drift beyond threshold with no explanation path
- monitoring indicates systemic pipeline instability

### Warn (limited publish + review required)
Use Warn when the release is usable but not broadly safe:
- significant swings beyond threshold with a plausible explanation
- backfills/restatements affect comparability (partial comparability)
- model/config changes expected to shift outputs
- coverage shifts beyond threshold but not catastrophic

Warn means:
- publish to the review council and decision owner first
- ship the “what changed and why” memo
- explicitly label what is safe vs what needs review

### Info (publish broadly)
Use Info when:
- within stability thresholds
- changes documented and diffed
- diagnostics clean
- comparability confirmed

Gates are only useful if they are enforced.

---

## Reproducibility (versioned inputs, configs, outputs)

If you can’t reproduce last month’s run, you can’t defend last month’s decisions.

Minimum reproducibility requirements:
- versioned input snapshots (or immutable dataset references)
- versioned mapping tables (taxonomy, rollups, join keys)
- versioned transforms (diffable code or artifact IDs)
- versioned model configuration (parameters, priors/constraints, feature switches)
- run ID + timestamp + environment metadata
- stored output artifacts (report pack, diagnostics, change log)

### Recommended run artifacts (every refresh)
- run manifest (inputs, versions, config hash, environment)
- report pack (standard template)
- diagnostics pack (standard checks)
- “what changed” diff (data + mappings + config)
- gate decision (Info/Warn/Block) with owner

Reproducibility turns MMM from “trust me” into “verify me.”

---

## Monitoring (data health + model health)

Monitoring is the early warning system that prevents drift from becoming a leadership incident.

### Data health monitoring
Track:
- freshness/latency and SLA breaches
- completeness and coverage shifts
- distribution drift (spend, exposures, reach)
- taxonomy/mapping diffs (new/removed/reassigned)
- join integrity (match rates, row explosions, dropped rows)

Alerting guidance:
- page/block for contract failures and severe coverage loss
- warn for drift beyond threshold
- info for minor expected movement

### Model health monitoring
Track:
- refresh stability deltas (contribution and ROI changes)
- rank-order stability (top changes and flips)
- uncertainty width changes (intervals widening/collapsing)
- identifiability flags (co-movement risk)
- backtest/holdout trend metrics where applicable

The objective is not “no movement.” The objective is explainable movement with clear escalation.

---

## Runbooks (what to do when things break)

When outputs swing or pipelines break, teams fail when they improvise. A runbook prevents panic and politics.

### Runbook: data contract failure (Block)
1) identify the failing dataset and contract rule
2) confirm whether it is upstream change vs pipeline regression
3) quarantine the release (Block) and notify the review council
4) apply the smallest safe fix (prefer upstream correction over downstream hacks)
5) re-run contract checks and document the change
6) re-run the MMM refresh with a new run ID and updated manifest
7) ship a short memo: what broke, what changed, what is safe now

### Runbook: major swing in outputs (Warn or Block)
1) classify: data change? mapping change? config change? real-world change?
2) run comparability checks and label comparable vs not comparable
3) review drift dashboard (data + model)
4) decide gate: Warn (limited publish) vs Block (quarantine)
5) publish “what changed and why” memo with safe-to-act labels
6) schedule a follow-up review and update guardrails if needed

### Runbook: taxonomy/mapping change
1) diff mapping table (new/removed/reassigned categories)
2) version bump and change note required
3) assess comparability impact on historical series
4) if impact is material, treat as Warn by default
5) update documentation and notify consumers of definition change

### Runbook: monitoring alerts
1) acknowledge alert and classify severity (Info/Warn/Block)
2) identify owner (data vs model vs pipeline)
3) apply runbook for the class of issue
4) log incident and postmortem action items (contracts, thresholds, tests)

Runbooks are the difference between a mature platform and a fragile one.

---

If you implement certification, release gates, reproducibility, monitoring, and runbooks, MMM becomes operable at scale. Without them, every refresh is a trust reset.
