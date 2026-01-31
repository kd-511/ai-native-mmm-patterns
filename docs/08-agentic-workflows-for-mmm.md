Paste this **exact Markdown** into `docs/08-agentic-workflows-for-mmm.md`. It’s formatted to render like your screenshot: title, two short intro paragraphs, **Contents** with linked bullets, then the first section starts and uses the same “What it is / What it does / Outputs” style.

```md
# Agentic Workflows for MMM

Agents can make MMM operations dramatically faster. They can also destroy trust faster than any model bug if they generate confident narratives, silently change assumptions, or act without auditability.

This doc defines how to introduce agentic workflows into MMM safely: the agent roles that are useful, the guardrails that are non-negotiable, how approvals and audit trails should work, how to evaluate agents, and what should never be allowed.

## Contents
- [Agent roles (QA, diagnostics, narrative, triage)](#agent-roles-qa-diagnostics-narrative-triage)
- [Guardrails (read-only default, scoped actions)](#guardrails-read-only-default-scoped-actions)
- [Approvals and audit trails](#approvals-and-audit-trails)
- [Evaluation of agents (precision/recall, hallucination controls)](#evaluation-of-agents-precisionrecall-hallucination-controls)
- [“Never allow” list](#never-allow-list)

---

## Agent roles (QA, diagnostics, narrative, triage)

Start with agent roles that are high leverage and low risk. The best early wins are operational, not decision-making.

### QA agent (data + pipeline)

Purpose: detect issues early and package evidence for humans.

What it does:
- runs contract checks and drift checks
- flags missingness, coverage shifts, outliers, taxonomy diffs
- produces a short “what changed” summary with links to the evidence

Outputs (artifacts):
- QA report (pass/fail + warnings)
- drift summary (top deltas and likely causes)
- gate recommendation (Info/Warn/Block) with evidence

### Diagnostics agent (model health + stability)

Purpose: assemble the standard diagnostics pack every refresh.

What it does:
- computes refresh-to-refresh deltas and stability metrics
- highlights rank-order flips and uncertainty width shifts
- surfaces identifiability warnings and “do not infer” zones

Outputs (artifacts):
- diagnostics pack (standard template)
- stability deltas and comparability label
- “needs review” checklist for the review council

### Narrative agent (refresh memo drafts)

Purpose: draft the refresh memo and executive summary using only computed artifacts.

What it does:
- summarizes changes since last refresh
- drafts “safe to act on” vs “needs review” vs “do not infer”
- drafts scenario narratives with expected ranges and downside risks

Outputs (artifacts):
- refresh memo draft (structured, decision-grade)
- executive summary draft (one page)
- scenario summary draft (assumptions clearly stated)

Important: narratives must cite the artifacts they are derived from. No free-form storytelling.

### Triage agent (ops + routing)

Purpose: reduce human toil in incident response.

What it does:
- classifies alerts (data vs mapping vs pipeline vs model)
- routes issues to the correct owner
- pulls the right runbook steps and pre-fills tickets

Outputs (artifacts):
- incident classification + owner routing
- pre-filled ticket with evidence links
- runbook checklist with progress tracking

Start here. Do not start with “agent recommends budget moves.”

---

## Guardrails (read-only default, scoped actions)

Agents should earn privileges. Default posture: read-only and evidence-producing.

Non-negotiable guardrails:
- read-only by default (no writes to data, configs, mappings)
- scoped tools only (least privilege, time-bound access)
- no silent changes (every action logged and reviewable)
- evidence-bound outputs (every claim traces to an artifact)
- deterministic packaging (agents assemble and summarize, humans decide)

Allowed actions (safe defaults):
- run checks, compute metrics, generate diff reports
- assemble standard report packs and refresh memos
- draft text with citations to computed results
- create tickets, route incidents, propose gate status

Restricted actions (require explicit approval):
- changing thresholds or gate criteria
- updating mapping tables or taxonomies
- modifying model config or priors/constraints
- publishing outputs broadly

Tool design guidance:
- prefer idempotent tools (repeatable without side effects)
- require diffable output for any proposed change
- make actions reversible (rollback is defined)
- log everything by default

---

## Approvals and audit trails

If an agent touches decision-grade outputs, auditability is mandatory.

Approval ladder (recommended):
- Level 0: read-only + evidence + draft generation (no approvals needed)
- Level 1: propose changes (requires human approval)
- Level 2: execute in sandbox (approval + diff review)
- Level 3: execute in production (rare, senior approval)

What must be logged (audit trail):
- run ID, timestamp, agent version
- inputs referenced (dataset versions, mapping versions, config versions)
- tools invoked and parameters
- artifacts generated (reports, diffs, memos)
- decisions suggested (gates, flags, recommended follow-ups)
- approvals (who approved what, when)
- diffs for any change (before/after)

Publishing policy:
- agents should not publish broadly by default
- agent drafts, humans review, humans publish
- gate status must be visible in the output pack

Audit trails protect trust and protect you politically.

---

## Evaluation of agents (precision/recall, hallucination controls)

If you don’t evaluate agents, you are shipping automation without accountability.

### Evaluate alerts (QA + diagnostics agents)

Metrics:
- precision: how many alerts were real issues
- recall: how many real issues were caught
- time-to-detection: how early issues are flagged
- severity calibration: are Block vs Warn recommendations appropriate

How to evaluate:
- label a set of historical incidents and clean runs
- run the agent on the same inputs
- compare agent outputs to labels
- tune thresholds to reduce alert spam while catching major issues

### Evaluate narratives (narrative agent)

The main risk is confident nonsense.

Metrics:
- citation coverage: percent of claims that cite an artifact
- hallucination rate: claims not supported by artifacts
- contradiction rate: claims that conflict with computed outputs
- usefulness: reviewer rating (time saved, clarity improved)

Controls:
- constrain generation to structured templates
- enforce “no claim without citation”
- automated checks for numerical consistency
- require human review for any recommendation language

### Evaluate actions (triage agent)

Metrics:
- routing accuracy: correct owner assignment
- ticket quality: completeness of evidence and steps
- time-to-resolution impact: does it reduce incident time

Treat agent performance like a product metric with an SLA.

---

## Never allow list

Never allow an agent to:
- change mapping tables, taxonomies, or transforms without approval
- change model configs, priors, or constraints without approval
- publish decision-grade outputs broadly without human signoff
- generate executive narratives without artifact grounding
- explain swings without referencing concrete diffs and diagnostics
- recommend budget moves as an autonomous decision
- override gates (Block/Warn/Info) without human review
- access data beyond its scope (least privilege always)
- operate without an audit trail and reproducible run manifest

Agents should not be the decision maker. They should be operating leverage.

---

If you implement role-scoped agents, read-only defaults, approvals, audit trails, and evaluation, agentic workflows can make MMM faster and safer. Without guardrails, they will make it faster and wrong.
```
