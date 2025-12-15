# The Core Failure Modes of MMM Systems

This document outlines the most common ways Marketing Mix Modeling (MMM) systems fail at scale — not academically, but operationally — and the design patterns that prevent those failures.

This is intentionally tool-, vendor-, and company-agnostic.

---

## 1. Instability Across Refreshes

**What it looks like**
- Large swings in channel ROI between runs
- Coefficient sign flips without clear business explanation
- Results that change more than underlying inputs

**Why it happens**
- Weak regularization or poorly specified priors
- Over-sensitive functional forms
- Data definition drift across refreshes
- No longitudinal diagnostics across model versions

**What to design instead**
- A formal stability layer with:
  - parameter drift metrics
  - prediction drift on fixed holdout data
  - uncertainty comparison across runs
- Explicit guardrails (e.g., no sign flips without review)
- Separation of data issues vs model behavior vs real-world change

---

## 2. Silent Data Pipeline Drift

**What it looks like**
- “Nothing changed” but results suddenly look wrong
- Inconsistent inclusion/exclusion of data
- Late discovery of upstream data issues

**Why it happens**
- No data contracts
- No distribution monitoring
- Poor lineage and versioning

**What to design instead**
- Data contracts defining expected schemas and ranges
- Automated distribution shift checks
- Versioned transformations with diffable changes

---

## 3. Architectures That Don’t Scale Horizontally

**What it looks like**
- A model that works for one brand, region, or use case
- Fragile extensions when new dimensions are added
- Increasing manual work per additional model

**Why it happens**
- Hard-coded assumptions
- Tight coupling between data prep and modeling
- No abstraction around “unit of modeling”

**What to design instead**
- Metadata-driven configuration
- Clear separation of ingestion, features, modeling, and reporting
- Design for N>1 entities from day one

---

## 4. Black-Box Outputs Without Trust

**What it looks like**
- ROI numbers without explanation
- Stakeholders questioning credibility
- Analysts unable to justify results beyond intuition

**Why it happens**
- No standardized model reports
- Inconsistent diagnostics
- Tribal knowledge instead of documentation

**What to design instead**
- A consistent model report including:
  - assumptions and constraints
  - uncertainty ranges
  - stability indicators
  - explicit caveats

---

## 5. No Feedback Loop to Decisions

**What it looks like**
- MMM outputs influence spend
- No measurement of whether those decisions worked
- Same mistakes repeated each cycle

**Why it happens**
- MMM treated as a one-way analytics exercise
- No tagging of decisions
- No post-decision evaluation

**What to design instead**
- Explicit tagging of model-informed decisions
- Feedback loops comparing predicted vs realized outcomes
- Periodic recalibration informed by decision performance

---

## Summary

MMM failures are rarely about math alone.  
They are system design failures.

Stable, trustworthy MMM requires:
- a stability layer
- a data contract layer
- scalable architecture
- interpretability by default
- a closed-loop decision system
