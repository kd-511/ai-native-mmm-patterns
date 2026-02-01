# Privacy-First Measurement

The measurement landscape is fracturing. Cookies are dying. Device graphs are thinning. Regulators are circling. The techniques that powered digital measurement for two decades are becoming unreliable or unavailable.

This doc defines how to build measurement systems that work within privacy constraints: what's actually changing, which approaches still work, how to evaluate clean rooms, and why MMM is having a renaissance.

## Contents

- [The identity crisis](#the-identity-crisis)
- [What's actually changing](#whats-actually-changing)
- [Clean rooms: promise vs reality](#clean-rooms-promise-vs-reality)
- [Aggregated reporting constraints](#aggregated-reporting-constraints)
- [Privacy-preserving techniques](#privacy-preserving-techniques)
- [Why MMM wins in a privacy-constrained world](#why-mmm-wins-in-a-privacy-constrained-world)
- [Building privacy-first measurement products](#building-privacy-first-measurement-products)
- [Checklist](#checklist)

---

## The identity crisis

Digital measurement was built on the assumption that you could track individuals across touchpoints. That assumption is breaking.

**What's under pressure:**

| Identity mechanism | Status | Timeline |
|-------------------|--------|----------|
| Third-party cookies | Deprecated in Safari/Firefox, declining in Chrome | Now |
| IDFA (iOS) | Opt-in only since iOS 14.5 | Now |
| GAID (Android) | Privacy Sandbox rolling out | 2024-2025 |
| Device graphs | Accuracy declining as signals thin | Ongoing |
| Email-based identity | Works but coverage limited | Stable |
| First-party data | Growing importance | Stable |

**What this means for measurement:**

- Cross-site attribution becoming unreliable
- View-through tracking severely limited
- Audience targeting less precise
- Frequency capping harder
- Multi-touch attribution losing signal

The teams that adapted early are fine. The teams that kept hoping cookies would survive are scrambling.

---

## What's actually changing

Not everything is broken. Precision matters here.

### What still works

**First-party data:** If users interact directly with your properties, you can still measure that. Logged-in users, app users, direct site visitors. This data is getting more valuable.

**Platform-reported conversions:** Platforms can still see conversions within their walls. Meta knows what happened on Meta. Google knows what happened on Google. The data exists. It just doesn't leave.

**Aggregate patterns:** You can still see that 10,000 people converted after seeing your campaign. You just can't see which 10,000 or trace their individual paths.

**Modeled conversions:** Platforms increasingly report modeled data, filling gaps with statistical inference. Directionally useful. Precision varies.

### What's degraded

**Cross-platform tracking:** Following a user from Instagram to your site to purchase is increasingly gated. Safari and Firefox block it. Chrome's restrictions tightening.

**View-through attribution:** Users who saw but didn't click are hardest to track. View-through windows are shortening or disappearing in some contexts.

**Multi-touch paths:** The full journey across touchpoints is becoming opaque. Last-touch is often all that's measurable with confidence.

**Lookalike audiences:** Built on behavioral data that's thinning. Quality declining. Reach narrowing.

### What's new

**Privacy Sandbox (Chrome):** Topics API, Attribution Reporting API, Protected Audiences. Google's replacement for third-party cookies. Still evolving. Adoption uncertain.

**SKAdNetwork (iOS):** Apple's privacy-preserving attribution. Limited data. Delayed reporting. Aggregated by design.

**Aggregated reporting APIs:** Platforms offering privacy-safe aggregated data. Useful but constrained.

---

## Clean rooms: promise vs reality

Clean rooms are the industry's answer to "how do we collaborate on data without sharing raw data?" The reality is more complicated.

### What clean rooms actually do

Purpose: enable data collaboration while keeping raw data isolated.

How it works:

- Each party uploads data to a secure environment
- Data is matched on common identifiers (hashed)
- Queries run inside the room, only aggregated outputs leave
- Raw data never moves between parties

Major players:

| Provider | Strengths | Limitations |
|----------|-----------|-------------|
| AWS Clean Rooms | Flexible, infrastructure-level | Requires technical lift |
| Google Ads Data Hub | Deep Google integration | Google ecosystem only |
| Meta Advanced Analytics | Meta data access | Meta ecosystem only |
| LiveRamp | Cross-platform identity | Match rates vary |
| Snowflake | Data warehouse native | Analytics-focused |
| InfoSum | No data movement model | Newer, smaller scale |

### Use cases that work

**Audience overlap analysis:** How many of my customers are in your audience? Works well when both parties have sufficient scale.

**Reach and frequency:** Deduplicated reach across platforms. Valuable for media planning.

**Conversion matching:** Match your conversions to platform exposures. Useful when direct tracking degraded.

**Lookalike seeding:** Share first-party segments as seed audiences. Privacy-safe alternative to pixel-based lookalikes.

### Use cases that are overhyped

**Real-time optimization:** Clean rooms are batch-oriented. Don't expect real-time bidding signals.

**Full-funnel attribution:** You get aggregate matches, not user journeys. Multi-touch paths remain opaque.

**Small advertiser solution:** Setup cost and minimum scale requirements exclude most small advertisers.

**Universal identity replacement:** Clean rooms don't solve identity. They work with whatever identity you bring.

### Build vs buy considerations

**Build (use infrastructure like AWS/Snowflake):**

- More flexibility
- Lower per-query costs at scale
- Requires data engineering investment
- You own the methodology

**Buy (use platform-specific solutions):**

- Faster to deploy
- Pre-built integrations
- Platform-specific limitations
- Methodology is a black box

**Hybrid approach:**

- Use platform clean rooms for platform-specific analysis
- Build own infrastructure for cross-platform work
- Most mature orgs land here

### Clean room evaluation checklist

Before investing in a clean room solution:

- [ ] Do you have sufficient first-party data scale?
- [ ] What's the match rate with target partners?
- [ ] What queries will you actually run?
- [ ] Who will operate it? (requires technical resources)
- [ ] What's the total cost? (setup + ongoing + queries)
- [ ] Does it integrate with your existing stack?
- [ ] What privacy thresholds apply?

---

## Aggregated reporting constraints

Privacy-preserving systems use aggregation to protect individuals. This creates measurement constraints.

### Privacy thresholds

Most aggregated systems have minimum thresholds. If a cohort is too small, data is suppressed or noised.

**Common threshold patterns:**

- k-anonymity: at least k users must share any reported attribute
- Minimum conversion counts: won't report if conversions below threshold
- Noise injection: random noise added to small counts
- Delayed reporting: data held until thresholds met

**Impact on measurement:**

- Long-tail segments invisible
- New campaigns slow to show signal
- Granular breakdowns unavailable
- Small tests harder to read

### Differential privacy basics for PMs

Differential privacy adds mathematical noise to protect individuals while preserving aggregate patterns.

**What you need to know:**

- Epsilon (ε): privacy budget. Lower = more privacy, more noise
- Queries consume budget. Unlimited queries = unlimited information leak
- Noise is calibrated to sensitivity of query
- Repeated queries on same data can compound information

**Practical implications:**

- Can't slice data infinitely (budget runs out)
- Small differences may be noise, not signal
- Need to plan queries in advance
- Exploratory analysis is constrained

### Designing for minimum viable granularity

Accept that some granularity is gone. Design around it.

**Questions to ask:**

- What's the minimum segment size we can reliably measure?
- Which breakdowns are essential vs nice-to-have?
- Can we use modeled data to fill gaps?
- How do we communicate increased uncertainty?

**Practical adjustments:**

- Aggregate small channels into categories
- Use longer time windows to accumulate signal
- Pre-register important breakdowns
- Accept wider confidence intervals

---

## Privacy-preserving techniques

Beyond clean rooms, several techniques enable measurement under privacy constraints.

### Cohort-based approaches

Purpose: group users into privacy-safe cohorts rather than tracking individuals.

How it works:

- Users assigned to cohorts based on behavior
- Targeting and measurement happen at cohort level
- Individual identity not exposed

Examples:

- Google Topics API (interest-based cohorts)
- FLoC (deprecated, but concept lives on)
- Publisher-defined audiences

Limitations:

- Coarser targeting than individual-level
- Cohort definitions may not match your needs
- Cross-site cohorts still contested

### On-device measurement

Purpose: keep raw data on user's device, send only aggregates.

How it works:

- Conversion tracking happens locally
- Device aggregates across events
- Only aggregate reports sent to servers

Examples:

- SKAdNetwork (iOS)
- Attribution Reporting API (Chrome)
- Private Click Measurement (Safari)

Limitations:

- Significant reporting delays
- Limited conversion data (few bits)
- No real-time optimization
- Platform-specific implementations

### Secure multi-party computation (MPC)

Purpose: compute on combined data without any party seeing the other's raw data.

How it works:

- Data split into encrypted shares
- Computation happens on shares
- Results reconstructed without revealing inputs

Limitations:

- Computationally expensive
- Requires coordination between parties
- Limited query types supported
- Still emerging for ads measurement

### What's production-ready vs experimental

| Technique | Status | When to use |
|-----------|--------|-------------|
| Clean rooms | Production | Cross-party analysis at scale |
| SKAdNetwork | Production | iOS app measurement |
| Google Attribution API | Rolling out | Chrome web attribution |
| On-device aggregation | Production | Platform-specific contexts |
| MPC for measurement | Experimental | R&D, not production |
| Federated learning | Experimental | Model training, not reporting |

---

## Why MMM wins in a privacy-constrained world

MMM was designed for a world without user-level tracking. That world is returning.

### MMM doesn't need user-level data

MMM works with aggregate inputs:

- Total spend by channel by time period
- Total conversions by time period
- Market-level variables (pricing, seasonality, competition)

No cookies required. No device graphs. No identity resolution.

### MMM handles signal loss gracefully

When user-level attribution loses signal, it breaks. Conversions don't match. Paths are incomplete. Data has holes.

MMM doesn't have this problem. It never relied on user paths. It models aggregate relationships. If aggregate patterns are stable, MMM still works.

### MMM provides cross-channel view

Platform attribution only sees its own walls. MMM sees the full media mix. In a world of walled gardens, this matters more, not less.

### The MMM renaissance

Open source options (Robyn, Meridian, PyMC Marketing) lowered the barrier. Bayesian methods improved uncertainty quantification. Faster refresh cycles made MMM more actionable.

Privacy constraints provided the push. MMM was ready.

---

## Building privacy-first measurement products

If you're building measurement capabilities, design for privacy from the start.

### Requirements gathering with privacy constraints

**Questions to ask upfront:**

- What user-level data do we actually need vs want?
- Which signals are degraded or unavailable?
- What's our first-party data foundation?
- Which platforms are we dependent on?
- What privacy regulations apply?

**Design principles:**

- Aggregate by default, user-level only when essential
- Build for data minimization (collect only what's needed)
- Assume signals will continue degrading
- Create fallback approaches for each critical metric

### Working with legal and privacy teams

Privacy teams are not blockers. They're risk managers. Work with them early.

**What to bring to the conversation:**

- What data you need and why
- How it will be stored and processed
- Who has access
- Retention period
- User consent status

**What to ask them:**

- What regulations apply?
- What's our risk tolerance?
- What approvals are needed?
- What documentation is required?

### Documentation and compliance

Privacy-first measurement requires clear documentation.

**Maintain documentation for:**

- Data sources and consent basis
- Processing purposes and legal basis
- Data flows and storage locations
- Retention policies
- Access controls
- Privacy impact assessments (where required)

---

## Checklist

Before launching any measurement system, confirm:

- [ ] User-level data is minimized to what's essential
- [ ] Aggregate approaches used where possible
- [ ] Privacy thresholds understood and designed around
- [ ] Clean room use cases validated (not assumed)
- [ ] First-party data strategy defined
- [ ] Platform-specific constraints documented
- [ ] Legal/privacy review completed
- [ ] Fallback approaches defined for signal loss scenarios
- [ ] MMM or aggregate modeling in place as foundation
- [ ] Team trained on privacy constraints and implications
