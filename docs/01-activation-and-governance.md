# Activation and Governance

MMM becomes valuable when it changes decisions. Most MMM efforts fail here, not in modeling.

This doc is a practical operating model for turning MMM into a repeatable decision system: clear cadence, clear roles, standard outputs, explicit gates, and measurable adoption.

## Contents
- [Decision calendar](#decision-calendar-monthlyquarterly-rhythm)
- [Stakeholder roles](#stakeholder-roles-who-decides-who-reviews-who-consumes)
- [Standard outputs](#standard-outputs-what-ships-every-refresh)
- [Decision workflow](#decision-workflow-scenarios-recommendations-approvals)
- [Governance gates](#governance-gates-what-requires-signoff)
- [Adoption metrics](#adoption-metrics-usage-decision-coverage-time-to-decision)
- [Templates you can copy](#templates-you-can-copy)

---

## Decision calendar (monthly/quarterly rhythm)

MMM should run on a decision cadence, not a data cadence.

A simple default:
- **Monthly:** operational refresh + monitoring + “what changed” memo  
  Goal: keep the system stable and catch drift early.
- **Quarterly:** planning-grade refresh + scenario packs + sign-offs  
  Goal: inform budget allocation and portfolio moves.

### Monthly rhythm (operational)
Outputs are “safe updates”:
- data + model health checks
- refresh comparability vs prior month
- updated contributions/ROI with uncertainty ranges
- a short “what changed and why” memo
- flagged items requiring review (do not broadcast surprises)

### Quarterly rhythm (planning)
Outputs are “decision-ready”:
- scenario pack (baseline + 3–5 actionable scenarios)
- recommended moves with downside risk framing
- approval workflow and decision log updates
- retrospectives from prior quarter decisions (closed-loop learning)

If the organization only wants quarterly MMM, you still need monthly monitoring. Otherwise you learn about drift when it’s already political.

---

## Stakeholder roles (who decides, who reviews, who consumes)

Activation collapses when “everyone owns it.” Name roles explicitly.

### Decision Owner (single accountable)
- owns the decision outcome (budget moves, planning recommendations)
- decides what is safe to act on
- owns the final call when evidence is mixed

This role is usually a planning lead, channel strategy lead, or a GM-type owner. Not the modeling team.

### MMM Product Owner (accountable for usability and trust)
- owns definitions, standard outputs, activation workflow
- ensures refreshes ship consistently and comparably
- drives adoption metrics and stakeholder enablement

### Model Owner (technical accountability)
- owns model configuration, diagnostics, and methodological choices
- explains changes and uncertainty drivers
- accountable for reproducibility and model health

### Data Owner (input integrity)
- owns data contracts and change management
- responsible for upstream breaks, taxonomy changes, and lineage

### Review Council (small, stable group)
A standing group that reviews release readiness:
- Decision Owner (chair)
- MMM Product Owner
- Model Owner
- Data Owner
- 1–2 key stakeholder reps (not 12)

### Consumers (broad audience)
Most people should consume standardized outputs, not debate modeling internals.
Give them clarity:
- what is safe to act on
- what is uncertain
- what is out of scope

---

## Standard outputs (what ships every refresh)

If outputs change format every cycle, people stop trusting them. Standardization is a product requirement.

### Every refresh should ship:
1) **Executive summary**
- what changed since last refresh
- top insights and recommended moves (if any)
- confidence and downside risk framing
- “do not infer” boundaries

2) **Contribution and ROI view**
- contribution estimates by channel
- ROI or marginal ROI at relevant spend levels
- uncertainty intervals front-and-center

3) **Scenario pack**
At minimum:
- baseline scenario (status quo)
- “increase” scenario for 1–2 scalable channels
- “reallocate” scenario (shift from low-confidence/low-return to higher)
- “protect downside” scenario (if cuts are on the table)

4) **Health panel**
- data health checks and drift flags
- model health checks and stability metrics
- comparability indicators vs prior refresh

5) **Change log**
A short, explicit record:
- data changes (definitions, sources, backfills)
- model/config changes
- known caveats

### What not to ship
- point estimates without uncertainty
- new diagnostics “this one time”
- surprise results without an explanation path

---

## Decision workflow (scenarios, recommendations, approvals)

This is the minimum workflow that turns MMM into action.

### Step 1: Pre-read (async)
Distribute:
- executive summary
- scenario pack
- health panel
- change log

Explicitly label:
- **Safe to act on**
- **Needs review**
- **Do not infer**

### Step 2: Review meeting (30–45 minutes, small group)
Agenda:
1) Any release gate violations? (block/warn)
2) What changed since last refresh?
3) What decisions are on the table this cycle?
4) Scenario review: expected impact + downside risk
5) Recommendation: approve, modify, or defer

If the meeting becomes “teach MMM,” you failed earlier. Education should be separate from decisioning.

### Step 3: Decision memo (same day)
Write a short decision memo:
- decision
- rationale (with uncertainty)
- risks and constraints
- owner + execution date
- follow-up date for evaluation

### Step 4: Decision log update (mandatory)
Log:
- what changed
- what was decided
- expected impact range
- what to watch
- when to review outcomes

### Step 5: Closed-loop review (next cycle)
Ask one question:
- Did the outcome land within the expected range?
If not, investigate inputs, assumptions, or external changes.

---

## Governance gates (what requires signoff)

Without gates, MMM becomes a political object. Gates make it operable.

Use three levels: **Block / Warn / Info**.

### Block (cannot publish)
Examples:
- missing critical inputs or broken data contract
- major taxonomy change without mapping/versioning
- reproducibility failure (cannot recreate last run)
- health panel shows severe drift beyond thresholds with no explanation

### Warn (publish to limited audience + review required)
Examples:
- notable swings beyond threshold but plausible explanation exists
- backfills or restatements that affect comparability
- model config updates with expected movement

### Info (publish broadly)
Examples:
- small expected movement within stability thresholds
- minor input changes documented and diffed
- routine refresh with stable diagnostics

### Signoff responsibilities
- Data changes: Data Owner + MMM Product Owner
- Model changes: Model Owner + MMM Product Owner
- Publish decision-grade recommendations: Decision Owner

Rule: the model owner should never be the final approver of business action. Keep accountability clean.

---

## Adoption metrics (usage, decision coverage, time-to-decision)

If you can’t measure adoption, you’re guessing.

Start with 3 metrics and expand later.

### 1) Decision coverage
- **Definition:** percent of major budget/planning decisions that reference MMM evidence
- **Why it matters:** tells you if MMM is actually used

### 2) Time-to-decision
- **Definition:** time from refresh availability to signed-off decision
- **Why it matters:** shows whether MMM accelerates planning or slows it

### 3) Repeat consumption
- **Definition:** returning stakeholders over 2–3 cycles (not one-time viewers)
- **Why it matters:** durable trust beats one-off curiosity

Optional add-ons:
- Recommendation action rate (accepted, modified, deferred)
- Stability incident rate (unexplained swings above threshold)
- “What changed” SLA (time to explain a swing)
- Closed-loop completion rate (decisions evaluated on schedule)

Adoption is not “dashboard views.” Adoption is decisions.

---

## Templates you can copy

### A) Refresh memo (one page)
**Subject:** MMM Refresh Summary (Month/Quarter)

**What changed since last refresh**
- Data:
- Model:
- External context:

**Key insights**
- Insight 1:
- Insight 2:

**Scenarios reviewed**
- Scenario A:
- Scenario B:
- Scenario C:

**Recommendation**
- Recommended move:
- Expected impact range:
- Downside risk / constraints:

**Release status**
- Gates: Block / Warn / Info
- Notes:

**Owners**
- Decision owner:
- MMM product owner:
- Model owner:
- Data owner:

### B) Decision log entry
- Decision:
- Date:
- Owner:
- MMM evidence used:
- Expected impact range:
- Risks/constraints:
- Follow-up date:
- Outcome (later):

---

If you implement the cadence, roles, standard outputs, gates, and adoption metrics above, MMM stops being “a model people argue about” and becomes “a system that reliably informs decisions.”
