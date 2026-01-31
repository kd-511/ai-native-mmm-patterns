```md
# Agentic Workflows for MMM

Agents can make MMM operations dramatically faster. They can also destroy trust faster than any model bug if they generate confident narratives, silently change assumptions, or act without auditability.

This doc describes how to introduce agentic workflows into MMM safely: which roles agents should play, what guardrails are non-negotiable, how approvals and audit trails should work, how to evaluate agents, and what should never be allowed.

## Contents
- [Agent roles (QA, diagnostics, narrative, triage)](#agent-roles-qa-diagnostics-narrative-triage)
- [Guardrails (read-only default, scoped actions)](#guardrails-read-only-default-scoped-actions)
- [Approvals and audit trails](#approvals-and-audit-trails)
- [Evaluation of agents (precision/recall, hallucination controls)](#evaluation-of-agents-precisionrecall-hallucination-controls)
- [“Never allow” list](#never-allow-list)

---

## Agent roles (QA, diagnostics, narrative, triage)

Start with agent roles that are high leverage and low risk. The best early wins are operational, not decision-making.

### 1) QA agent (data + pipeline)
Purpose: detect issues early and package evidence for humans.
What it does:
- runs contract checks and drift checks
- flags missingness, coverage shifts, outliers, taxonomy diffs
- produces a short “what changed” summary with links to the evidence

Outputs (artifacts):
- QA report (pass/fail + warnings)
- drift summary (top deltas and likely causes)
- gate recommendation (Info/Warn/Block) with evidence

### 2) Diagnostics agent (model health + stability)
Purpose: assemble the standard diagnostics pack every refresh.
What it does:
- computes refresh-to-refresh deltas and stability metrics
- highlights rank-order flips and uncertainty width shifts
- surfaces identifiability warnings and “do not infer” zones

Outputs:
- diagnostics pack (standard template)
- stability deltas and comparability label
- “needs review” checklist for the review council

### 3) Narrative agent (refresh memo drafts)
Purpose: draft the refresh memo and executive summary using only computed artifacts.
What it does:
- summarizes changes since last refresh
- drafts “safe to act on” vs “needs review” vs “do not infer”
- drafts scenario narratives with expected ranges and downside risks

Outputs:
- refresh memo draft (structured, decision-grade)
- executive summary draft (one page)
- scenario summary draft (assumptions clearly stated)

Important: narratives must cite the artifacts they are derived from. No free-form storytelling.

### 4) Triage agent (ops + routing)
Purpose: reduce human toil in incident response.
What it does:
- classifies alerts (data vs mapping vs pipeline vs model)
- routes issues to the correct owner
- pulls the right runbook steps and pre-fills tickets

Outputs:
- incident classification + owner routing
- pre-filled ticket with evidence links
- runbook checklist with progress tracking

Start here. Do not start with “agent recommends budget moves.”

---

## Guardrails (read-only default, scoped actions)

Agents should earn privileges. Default posture: read-only and evidence-producing.

### Non-negotiable guardrails
- Read-only by default (no writes to data, configs, mappings)
- Scoped tools only (least privilege, time-bound tokens)
- No silent changes (every action logged and reviewable)
- Evidence-bound outputs (every claim traces to an artifact)
- Deterministic packaging (agents assemble and summarize, humans decide)

### Allowed actions (safe defaults)
- run checks, compute metrics, generate diff reports
- assemble standard report packs and memos
- draft text with citations to computed results
- create tickets, route incidents, propose gate status

### Restricted actions (require explicit approval)
- changing thresholds or gate criteria
- updating mapping tables or taxonomies
- modifying model config or priors/constraints
- publishing outputs broadly

### Tool design guidance
Prefer tools that are:
- idempotent (repeatable without side effects)
- diffable (before/after visible)
- reversible (easy rollback)
- logged (who/what/when)

Agents should accelerate operations, not create new failure modes.

---

## Approvals and audit trails

If an agent touches decision-grade outputs, auditability is mandatory.

### Approval model (recommended)
Use a simple ladder:
- Level 0: read-only, evidence + draft generation (no approvals needed)
- Level 1: propose changes (requires human approval)
- Level 2: execute changes in a sandbox (requires approval + diff review)
- Level 3: execute changes in production (rare, requires senior approval)

### What must be logged (audit trail)
For every agent run:
- run ID, timestamp, agent version
- inputs referenced (dataset versions, mapping versions, config versions)
- tools invoked and parameters
- artifacts generated (reports, diffs, memos)
- decisions suggested (gate recommendation, flags)
- approvals (who approved what, when)
- diffs for any change (before/after)

### Publishing policy
Agents should not publish to broad audiences automatically.
Default: agent drafts, humans review, humans publish.

Audit trails protect trust and protect you politically.

---

## Evaluation of agents (precision/recall, hallucination controls)

If you don’t evaluate agents, you are shipping automation without accountability.

### 1) Evaluate alerts (QA + diagnostics agents)
Metrics:
- precision: how many alerts were real issues
- recall: how many real issues were caught
- time-to-detection: how early issues are flagged
- severity calibration: are Block vs Warn recommendations appropriate

Methods:
- label a set of historical incidents
- run the agent and compare outputs to ground truth labels
- tune thresholds to optimize for “catch big problems, avoid alert spam”

### 2) Evaluate narratives (narrative agent)
The main risk is confident nonsense.

Metrics:
- citation coverage: % of claims that cite an artifact
- hallucination rate: claims not supported by artifacts
- contradiction rate: claims that conflict with computed outputs
- usefulness: reviewer rating (does it reduce time to publish?)

Controls:
- constrain generation to structured templates
- enforce “no claim without citation” policies
- automated checks for numerical consistency
- require a human review for any “recommendation” language

### 3) Evaluate actions (triage agent)
Metrics:
- routing accuracy: correct owner assignment
- ticket quality: completeness of evidence and steps
- time-to-resolution impact: does it reduce incident time

Evaluation is a product requirement. Treat agents like a feature with SLAs, not a novelty.

---

## “Never allow” list

If you want to keep MMM trusted, prohibit these behaviors outright.

Never allow an agent to:
- change mapping tables, taxonomies, or transforms without approval
- change model configs, priors, or constraints without approval
- publish decision-grade outputs broadly without human signoff
- generate executive narratives without artifact grounding
- “explain” swings without referencing concrete diffs and diagnostics
- recommend budget moves as an autonomous decision
- override gates (Block/Warn/Info) without human review
- access data beyond its scope (least privilege always)
- operate without an audit trail and reproducible run manifest

Agents should not be the decision maker. They should be the operating leverage.

---

If you implement role-scoped agents, read-only defaults, approvals, audit trails, and evaluation, agentic workflows can make MMM faster and safer. Without guardrails, they will make it faster and wrong.
```
