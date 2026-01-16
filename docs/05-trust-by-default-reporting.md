# Trust-by-Default Reporting

Marketing Mix Modeling outputs only create value when stakeholders trust them enough to act. Trust is not a vibe. Trust is a reporting system: consistent templates, mandatory diagnostics, uncertainty that is visible, and clear boundaries on what the model can and cannot claim.

This doc defines a standard reporting pack for Marketing Mix Modeling that reduces debate, prevents over-interpretation, and makes every refresh decision-grade for both technical and non-technical audiences.

## Contents
- [Standard model report template](#standard-model-report-template)
- [Diagnostics that ship every time](#diagnostics-that-ship-every-time)
- [Uncertainty display patterns](#uncertainty-display-patterns)
- [What not to claim (and why)](#what-not-to-claim-and-why)
- [Executive summary patterns (for non-technical leaders)](#executive-summary-patterns-for-non-technical-leaders)

---

## Standard model report template

If the format changes every refresh, stakeholders stop trusting the system. A standard template makes MMM outputs comparable and forces the team to ship the same evidence every time.

A good model report answers five questions:
- What changed since last refresh?
- What is safe to act on right now?
- What is uncertain and why?
- What decisions do you recommend (if any)?
- What would change the conclusion?

### Recommended report sections (every refresh)

1) Executive summary (one page)
- decisions enabled (this cycle)
- key changes vs prior refresh
- top insights and recommended moves (if any)
- confidence and downside risk
- what not to conclude

2) Results (uncertainty-first)
- contribution estimates by channel
- ROI or marginal ROI at relevant spend levels
- response curves where applicable
- credible intervals shown as primary, not optional

3) Scenario pack
- baseline scenario (status quo)
- 2–3 action scenarios tied to controllable levers
- expected impact range and downside risk per scenario
- assumptions and constraints

4) Diagnostics and model health
- required diagnostics (see next section)
- stability/comparability checks vs prior refresh
- identifiability warnings and “do not infer” flags

5) Data and change log
- data changes (sources, mappings, backfills)
- model/config changes
- comparability label: Comparable / Partially comparable / Not comparable
- gate status: Info / Warn / Block

6) Appendices (optional)
- deeper technical details, only if needed
- keep the main narrative decision-grade

---

## Diagnostics that ship every time

Diagnostics are not optional. If diagnostics only appear when someone asks, trust collapses.

### Minimum diagnostics checklist (every refresh)

Data health:
- freshness/latency status (met SLA or not)
- completeness and coverage shifts
- distribution shift flags (spend, exposures)
- taxonomy/mapping diffs (new, removed, reassigned)

Comparability:
- refresh-to-refresh delta report (key outputs)
- label: comparable vs not comparable and why
- “what changed” memo included and diffable

Model health:
- contribution stability deltas vs prior refresh
- ROI and marginal ROI rank-order change flags
- uncertainty width changes (intervals widening or collapsing)
- identifiability/co-movement warnings

Scenario readiness:
- scenarios available for the decisions on the calendar
- scenario assumptions documented
- scenarios labeled safe vs needs review

Gate status:
- Info / Warn / Block with owner and timestamp

Rule: if the diagnostic is important enough to reference, it is important enough to ship every time.

---

## Uncertainty display patterns

Uncertainty is not a footnote. It is the decision context.

The biggest reporting failure is presenting point estimates as truth. The fix is standard uncertainty patterns that make misinterpretation harder.

### Patterns that work

1) Ranges, not single numbers
- show credible intervals by default
- highlight downside risk, not just expected value

2) Separate signal from confidence
- present “impact estimate” and “confidence level” as distinct fields
- never imply confidence from a clean chart

3) Use decision-oriented language
- “expected range” and “downside risk”
- “safe to act on” vs “needs review”
- “do not infer” where identifiability is weak

4) Rank stability, not just rank order
- show when rank order is unstable across refreshes
- avoid forcing stakeholders into a false ranking battle

5) Make uncertainty comparable across time
- show whether intervals widened or narrowed vs last refresh
- treat big interval changes as a diagnostic, not a footnote

### Anti-patterns to avoid
- hiding uncertainty in an appendix
- showing only a point estimate in the headline
- collapsing uncertainty into a single “confidence” word with no evidence

---

## What not to claim (and why)

Most trust collapses happen because the model is asked to make claims it cannot support.

What not to claim:
- channel X caused Y as a deterministic statement
- precise incremental lift when identifiability is weak
- “this ranking is definitive”
- “we proved this campaign worked” without proper context
- user-level or creative-level attribution from aggregate MMM

Why:
- MMM is a system-level estimator with uncertainty
- channels often co-move, making attribution ambiguous
- inputs and definitions can shift over time
- the model can be directionally useful even when not precise

How to state claims safely:
- use ranges and conditions
- label “directional vs validated”
- state assumptions and constraints
- include “what would change the conclusion”

If you avoid over-claiming, you protect the program’s credibility.

---

## Executive summary patterns (for non-technical leaders)

Executives want decisions, not diagnostics. Your job is to translate complexity into decision-grade clarity without hiding uncertainty.

### A one-page executive summary should include:

1) What changed
- top 3 changes vs prior refresh
- whether changes are comparable or affected by data/mapping updates

2) Decisions enabled
- what decisions this refresh supports (budget shifts, scenario choices)
- what decisions are explicitly out of scope

3) Recommended moves (if any)
- 1–3 recommendations, each with:
  - expected impact range
  - downside risk / constraints
  - confidence level and key caveats
  - owner and next step

4) What not to conclude
- 2–3 “do not infer” bullets that prevent misinterpretation

5) Release readiness
- gate status: Info / Warn / Block
- any items requiring review before broad distribution

### Executive summary language patterns that work
- “Here is what is safe to act on”
- “Here is what changed and why”
- “Here is the expected range and downside risk”
- “Here is what we should not conclude”
- “Here is what would change this recommendation”

If leadership can read one page and know what to do next, the reporting system is doing its job.
