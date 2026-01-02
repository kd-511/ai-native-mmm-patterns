# Common Pitfalls and Failure Modes of MMM Systems

MMM loses trust in predictable ways. Most failures happen in operations, not modeling: unstable refreshes, silent drift, false certainty, confusing reporting, and weak activation.

This doc is a practical map of how MMM programs fail in production and the design patterns that prevent instability, drift, and loss of trust.

## Contents
- [Failure mode: instability across refreshes](#failure-mode-instability-across-refreshes)
- [Failure mode: silent data and pipeline drift](#failure-mode-silent-data-and-pipeline-drift)
- [Failure mode: identifiability and false certainty](#failure-mode-identifiability-and-false-certainty)
- [Failure mode: reporting that confuses rather than clarifies](#failure-mode-reporting-that-confuses-rather-than-clarifies)
- [Failure mode: activation gaps (insights do not translate to decisions)](#failure-mode-activation-gaps-insights-do-not-translate-to-decisions)
- [Failure mode: governance gaps (no gates, no accountability)](#failure-mode-governance-gaps-no-gates-no-accountability)
- [Patterns that prevent failure](#patterns-that-prevent-failure)
- [Practical checks and artifacts (what to implement)](#practical-checks-and-artifacts-what-to-implement)

---

## Failure mode: instability across refreshes

MMM collapses when refreshes move and no one can explain why.

What it looks like:
- channel contribution and ROI swing materially between refreshes
- rank order flips without a clear explanation path
- stakeholders delay action until “next refresh”
- teams start saying “MMM changes every time”

Why it happens:
- backfills and restatements make refreshes non-comparable
- taxonomy, mappings, or definitions change (sometimes silently)
- model configuration changes are untracked or inconsistent
- no stability thresholds or escalation path

Patterns that prevent it:
- treat refreshes like releases: gates + signoffs + standard pack
- make comparability explicit every cycle (is this comparable to last time?)
- ship a required “what changed and why” memo
- maintain versioned inputs/configs/outputs so swings are diagnosable

---

## Failure mode: silent data and pipeline drift

Drift is inevitable. Silent drift is optional.

What it looks like:
- slow degradation, then sudden “mystery swings”
- spend or exposure series quietly change meaning over time
- different teams report different “truth” for the same channel

Why it happens:
- schema changes, vendor definition changes, taxonomy changes
- ETL changes without versioning or diffable transforms
- missingness, coverage, and distribution shifts go unmonitored
- no single owner for mapping tables and key joins

Patterns that prevent it:
- data contracts for critical inputs (schema, ranges, coverage, freshness)
- lineage and versioning (inputs, transforms, outputs)
- data observability that ships with every refresh
- explicit change management for mappings and definitions

---

## Failure mode: identifiability and false certainty

MMM can produce clean numbers even when the signal is ambiguous. This is where trust dies.

What it looks like:
- point estimates are treated as truth
- people over-index on rank order
- decisions get made on fragile attribution, then reversed later
- “confidence” is implied even when channels co-move

Why it happens:
- collinearity and limited independent variation
- too many degrees of freedom relative to signal
- constraints and priors hide uncertainty rather than communicate it
- no explicit “do not infer” boundaries

Patterns that prevent it:
- uncertainty-first reporting (intervals and downside risk are primary)
- identifiability disclosure (where attribution is ambiguous, say so)
- decision robustness: prefer actions that remain good across plausible ranges
- triggers for experiments or additional evidence when identifiability is low

---

## Failure mode: reporting that confuses rather than clarifies

If reporting creates debate instead of decisions, the product is broken.

What it looks like:
- meetings turn into dashboard tours
- stakeholders interpret charts differently
- leaders ask “so what should we do?” and the answer is unclear
- surprises are broadcast without context

Why it happens:
- inconsistent outputs across cycles
- point estimates without uncertainty and caveats
- insight, recommendation, and decision are blended together
- too much internal modeling detail for broad audiences

Patterns that prevent it:
- standard report template that ships every refresh
- clear labeling: Safe to act on / Needs review / Do not infer
- “what changed” narrative is mandatory
- keep the broad audience on standardized outputs, not modeling internals

---

## Failure mode: activation gaps (insights do not translate to decisions)

MMM is not valuable when it is “interesting.” It is valuable when it changes plans.

What it looks like:
- insights are presented, but spend and strategy do not change
- MMM becomes a quarterly report, not a planning input
- no one can point to decisions MMM influenced

Why it happens:
- no decision owner accountable for action
- scenarios are missing or not tied to controllable levers
- outputs do not land on the planning calendar
- no decision log, no follow-up evaluation

Patterns that prevent it:
- decision cadence: monthly monitoring, quarterly planning pack
- scenario-first outputs tied to real levers
- short decision memo and decision log entry every cycle
- closed-loop review on outcomes vs expected ranges

---

## Failure mode: governance gaps (no gates, no accountability)

Without gates, MMM becomes political and fragile.

What it looks like:
- results ship broadly with no release readiness check
- upstream changes happen without review
- when something swings, ownership is unclear

Why it happens:
- no Block / Warn / Info release framework
- no signoffs for data changes and model changes
- no audit trail and no reproducibility guarantees
- too many reviewers, or none, and no stable council

Patterns that prevent it:
- explicit gates with clear criteria (Block/Warn/Info)
- small, stable review council with named owners
- reproducibility and auditability (versioned inputs/configs/outputs)
- decision owner approves business action, not the model owner

---

## Patterns that prevent failure

If you do nothing else, implement these:

1) Run MMM on a decision cadence, not a data cadence.  
2) Treat refreshes like releases: standard outputs, gates, signoffs.  
3) Make comparability explicit every cycle.  
4) Make uncertainty the product, not a footnote.  
5) Instrument the system: data health + model health.  
6) Close the loop: decisions logged, outcomes reviewed, playbook updated.

---

## Practical checks and artifacts (what to implement)

### A) Gate checklist (Block / Warn / Info)

Block (cannot publish):
- broken data contract or missing critical inputs
- major taxonomy change without mapping/versioning
- run not reproducible from versioned inputs/config
- severe drift beyond threshold with no explanation path

Warn (limited publish + review required):
- swings beyond threshold with plausible cause
- backfills/restatements that impact comparability
- model/config updates expected to move outputs

Info (publish broadly):
- within stability thresholds
- changes documented and diffed
- diagnostics clean

### B) “What changed since last refresh” memo (required)
Include:
- data changes (sources, definitions, mappings, backfills)
- model/config changes
- key deltas and whether they are explainable
- what is safe to act on vs needs review vs do not infer

### C) Drift checks (data + model)

Data drift:
- missingness and coverage shifts
- distribution shifts and outliers
- freshness/latency
- taxonomy/mapping diffs

Model drift:
- contribution/ROI deltas vs prior refresh
- uncertainty width changes
- stability thresholds and incidents
- identifiability flags

### D) Identifiability checklist (minimum)
- co-movement risk flagged by channel pair/group
- sensitivity checks captured (how conclusions change)
- “do not infer” boundaries stated explicitly
- experiment triggers when MMM evidence is insufficient

### E) Decision log template (minimum fields)
- decision, owner, date
- scenario selected
- expected impact range + assumptions
- constraints/risks
- follow-up date + outcome later

If you implement gates, drift checks, uncertainty-first reporting, and closed-loop decisioning, MMM stops being “a model people argue about” and becomes “a system people trust enough to use.”
