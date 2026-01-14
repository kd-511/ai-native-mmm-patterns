# Data Contracts and Lineage

Marketing Mix Modeling is only as trustworthy as its inputs. Most “model issues” are actually data definition issues: silent schema changes, shifting taxonomies, backfills, and transforms that no one can audit.

This doc defines the minimum data contracts and lineage patterns required to operate Marketing Mix Modeling as a governed system: what must be true, what breaks a release, how to version changes, and how to handle emergencies safely.

## Contents
- [Schema contracts (what must be true)](#schema-contracts-what-must-be-true)
- [Data quality checks (what blocks vs warns)](#data-quality-checks-what-blocks-vs-warns)
- [Lineage and versioning](#lineage-and-versioning)
- [Diffable transforms](#diffable-transforms)
- [“Break glass” process (how to handle emergency changes safely)](#break-glass-process-how-to-handle-emergency-changes-safely)

---

## Schema contracts (what must be true)

Schema contracts define the minimum shape and meaning of MMM inputs. Without contracts, “the same dataset” becomes different over time and refreshes stop being comparable.

A schema contract should define:
- required tables and required columns
- datatypes and allowed value formats
- primary keys and join keys
- allowed null behavior (where nulls are acceptable vs not)
- units and definitions (spend currency, timezone, windowing rules)
- taxonomy rules (channel names, rollups, mapping ownership)

Minimum recommendation:
- one contract per critical input dataset (outcome, spend, exposures, mappings, controls)
- one owner per contract
- contract changes require a version bump and a change note

---

## Data quality checks (what blocks vs warns)

Data checks are not “nice to have.” They are release gates.

### Block checks (cannot ship)
Examples:
- missing critical columns or failed schema validation
- join key integrity breaks (row explosions, dropped coverage beyond threshold)
- freshness breach (data not updated within SLA)
- outcome series missing or materially incomplete
- mapping table missing or incompatible version

### Warn checks (limited publish + review required)
Examples:
- coverage shifts beyond threshold (publisher/channel coverage drop)
- distribution shift (spend/exposure spikes or collapses)
- late backfills/restatements that affect comparability
- new categories appearing in taxonomy without confirmed mapping

### Info checks (ship broadly)
Examples:
- within expected ranges and coverage thresholds
- changes are documented and diffed
- no contract breaches

Recommended check categories:
- freshness/latency
- completeness and coverage
- schema integrity
- range and outlier detection
- distribution shifts (drift)
- join integrity (row count and key match rates)
- taxonomy/mapping diffs

---

## Lineage and versioning

Lineage is how you answer: “Where did this number come from?” Versioning is how you ensure you can reproduce it.

Minimum lineage requirement:
- every refresh output links to:
  - input dataset versions (or snapshot identifiers)
  - mapping table version
  - transform version (commit hash or artifact ID)
  - model config version
  - run ID and timestamp

Version what matters:
- mapping tables (channel taxonomy, publisher mappings, rollups)
- transforms (ETL logic, aggregation rules, attribution rules)
- input snapshots (especially if backfills occur)
- outputs (so past decisions remain auditable)

If you can’t recreate last month’s output, you can’t defend last month’s decision.

---

## Diffable transforms

Transforms are where truth silently changes.

Make every transform diffable:
- mapping diffs: new categories, removed categories, reassigned categories
- aggregation diffs: changes in windowing, timezones, filters
- join diffs: key coverage changes, row retention changes
- metric diffs: definition changes (what is included/excluded)

Recommended patterns:
- store transforms as code (not manual steps)
- produce a “diff report” artifact on every change
- require review for transform changes that affect historical series

Minimum “what changed” artifacts:
- mapping diff (before/after)
- row counts and coverage diff
- top contributors to delta (which channels/publishers moved and why)
- explicit statement: comparable / partially comparable / not comparable

---

## “Break glass” process (how to handle emergency changes safely)

Sometimes you must ship an emergency fix: a broken upstream feed, a critical mapping issue, or a late restatement. “Break glass” is how you do it without destroying trust.

A break-glass policy should define:
- who can declare break glass (named owners)
- what qualifies (severity criteria)
- what gets frozen vs what can change
- what must be logged (mandatory audit trail)
- how you communicate (standard memo)
- how you reconcile later (post-incident correction plan)

Minimum break-glass checklist:
- [ ] identify severity and impacted outputs
- [ ] capture the exact input and transform versions
- [ ] implement the smallest safe change
- [ ] run contract checks and drift checks
- [ ] label comparability and gate the release (Warn or Block, usually)
- [ ] publish a change memo: what changed, why, what is safe to act on
- [ ] schedule a post-incident review and permanent fix

Break-glass is not a shortcut. It is controlled change under pressure.

---

If you implement contracts, block/warn gates, lineage/versioning, and diffable transforms, Marketing Mix Modeling becomes reproducible and governable. Without them, every refresh is a trust reset.
