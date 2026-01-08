# Stability Layer

MMM becomes useful when results are stable enough to act on. Stability does not mean “no change.” It means refresh-to-refresh movement is explainable, comparable, and governed.

This doc defines what stability means in MMM platforms and the practical checks, guardrails, and escalation paths that keep trust intact when things move.

## Contents
- [What “stability” means in MMM platforms](#what-stability-means-in-mmm-platforms)
- [Drift metrics (data + model)](#drift-metrics-data--model)
- [Refresh comparability](#refresh-comparability)
- [Guardrails and thresholds](#guardrails-and-thresholds)
- [Holdout/backtesting expectations](#holdoutbacktesting-expectations)
- [Escalation playbook when things swing](#escalation-playbook-when-things-swing)

---

## What “stability” means in MMM platforms

Stability is a product requirement: stakeholders should be able to rely on outputs without re-litigating the model every refresh.

Stability means:
- refresh-to-refresh movement has an explainable cause
- results are comparable across time and across releases
- uncertainty is visible (so people do not overreact)
- there is a clear policy for what can ship and what requires review

Stability does not mean:
- identical results every refresh
- removing uncertainty from the story
- hiding swings to avoid questions

---

## Drift metrics (data + model)

Drift is inevitable. The goal is to detect it early and classify it correctly.

Data drift (inputs):
- missingness and coverage shifts
- distribution shifts and outliers (spend, exposures, reach)
- taxonomy/mapping diffs (new categories, reassignment rates)
- freshness and latency (late arriving data, restatements)

Model drift (outputs):
- contribution deltas vs prior refresh (absolute and %)
- ROI and marginal ROI rank-order changes
- uncertainty width changes (intervals expanding or collapsing)
- fit/backtest deltas where applicable

A good drift panel answers:
- what moved?
- is it explainable?
- is it comparable?
- is it safe to publish?

---

## Refresh comparability

Comparability is the difference between “movement we can trust” and “movement we must quarantine.”

Refreshes become non-comparable when:
- historical inputs are restated/backfilled
- channel definitions or mappings change
- model configuration changes materially
- time windows shift in a way that changes interpretation

Patterns that enforce comparability:
- versioned inputs/configs/outputs (every run is reproducible)
- diffable transforms (mapping tables and ETL are auditable)
- a required “what changed and why” memo every refresh
- explicit comparability labels: Comparable / Partially comparable / Not comparable

Minimum comparability artifacts:
- a change log (data, mappings, config)
- a delta report (prior vs current for key outputs)
- a gate status (Block/Warn/Info)

---

## Guardrails and thresholds

Guardrails define what level of movement triggers review and how distribution happens.

Typical guardrails:
- contribution swing threshold by channel
- ROI rank-order flip threshold (top N changes)
- uncertainty collapse threshold (suspiciously tight intervals)
- data contract breach threshold (coverage, missingness, freshness)

Guardrails should map to actions:
- Info: publish broadly
- Warn: limited publish + review required
- Block: cannot publish

The point is not the exact numbers. The point is having explicit policy so stability is not negotiated every refresh.

---

## Holdout/backtesting expectations

Backtesting is not a scoreboard. It is a sanity check that protects against false certainty.

Expectations to set:
- what “good enough” means for your use cases
- which metrics are monitored every refresh vs periodically
- how backtest results affect gates (Info/Warn/Block)
- what changes require re-baselining expectations (taxonomy or major data shifts)

What to avoid:
- treating backtest as proof of causal truth
- optimizing to backtest at the expense of decision usability
- hiding uncertainty because fit looks “good”

---

## Escalation playbook when things swing

When outputs swing, you need a repeatable path that prevents panic and preserves credibility.

Step 1: classify the swing
- data change?
- mapping/taxonomy change?
- config/model change?
- real-world change?

Step 2: run the comparability checklist
- comparable vs not comparable
- what must be quarantined vs safe to publish

Step 3: apply gates
- Block / Warn / Info decision with named owner and timestamp

Step 4: communicate with a standard memo
- what changed
- why it changed (best-known cause)
- what is safe to act on
- what is under review
- expected timeline for resolution

Step 5: update the playbook
- new thresholds?
- new data contract?
- new monitoring?
- new escalation owner?

If you treat swings like incidents, stability becomes a system property, not a personality trait.
