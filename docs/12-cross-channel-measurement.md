# Cross-Channel Measurement

Every ad platform will tell you they drove your conversions. Add up what they all claim and you'll exceed your total conversions by 2-3x. This is not fraud. It's a feature of how attribution works. And it's your problem to solve.

This doc defines how to think about cross-channel measurement: why the numbers don't add up, how different approaches handle the problem, where MMM fits, and what to tell stakeholders who are confused by conflicting reports.

## Contents

- [The double-counting problem](#the-double-counting-problem)
- [Walled gardens and data silos](#walled-gardens-and-data-silos)
- [Cross-channel measurement approaches](#cross-channel-measurement-approaches)
- [MMM as the arbiter](#mmm-as-the-arbiter)
- [Channel-specific considerations](#channel-specific-considerations)
- [Building cross-channel reporting products](#building-cross-channel-reporting-products)
- [What to tell stakeholders](#what-to-tell-stakeholders)
- [Checklist](#checklist)

---

## The double-counting problem

Attribution systems give credit. They give it generously. Multiple systems giving credit for the same conversion is not a bug. It's how they work.

### Why it happens

**Overlapping attribution windows:**

User sees Meta ad Monday. Clicks Google ad Wednesday. Converts Friday.

- Meta claims the conversion (7-day view-through)
- Google claims the conversion (last click)
- Both are "right" by their own rules

**View-through vs click-through:**

View-through attribution credits conversions to ad impressions even without clicks. Every platform someone was exposed to claims view-through credit.

User sees ads on Meta, YouTube, display network. Converts via direct navigation.

- Meta claims view-through
- YouTube claims view-through
- Display network claims view-through
- Total claimed: 3 conversions. Actual: 1.

**Cross-device paths:**

User researches on mobile. Converts on desktop.

- Mobile channels claim credit (they started the journey)
- Desktop channels claim credit (they closed)
- Same user, different devices, multiple claims

### The math problem

| Channel | Reported Conversions |
|---------|---------------------|
| Paid Search | 10,000 |
| Meta | 8,000 |
| YouTube | 4,000 |
| Display | 3,000 |
| Affiliate | 2,000 |
| **Total Claimed** | **27,000** |
| **Actual Conversions** | **12,000** |

This is a real pattern. The sum of channel-reported conversions routinely exceeds actual conversions by 100-200%.

### Why platforms don't fix this

Incentive alignment:

- Platforms want to show they drive value
- Conservative attribution means showing less value
- Less value means less ad spend
- Nobody voluntarily makes themselves look worse

This is not conspiracy. It's rational behavior. Your job is to see through it.

---

## Walled gardens and data silos

The major platforms are walled gardens. They see everything inside their walls. They see almost nothing outside.

### What each platform sees

| Platform | Sees clearly | Can't see |
|----------|-------------|-----------|
| Google Ads | Search, YouTube, GDN, site with GA4 | Meta, TikTok, offline, competitors |
| Meta | Facebook, Instagram, Audience Network | Google, TikTok, Amazon, offline |
| Amazon Ads | Amazon search, DSP, retail data | External sites, non-Amazon conversions |
| TikTok | TikTok app, TikTok pixel sites | Everything else |
| The Trade Desk | Programmatic display/CTV inventory | Walled garden inventory |

### The incentive problem

Each platform:

- Reports their own contribution favorably
- Cannot measure what happens outside their walls
- Has no incentive to help you compare across platforms

This creates a measurement vacuum. Someone needs to fill it. That someone is you.

### "Unified measurement" is mostly fantasy

Vendors promise unified measurement. Most deliver:

- Data from multiple platforms in one dashboard
- Still double-counted (same numbers, prettier format)
- No actual deduplication at user level
- No incremental contribution estimation

True cross-channel measurement requires either:

- User-level identity across platforms (increasingly impossible)
- Aggregate modeling that doesn't rely on user matching (MMM)

---

## Cross-channel measurement approaches

Different approaches make different tradeoffs. None are perfect.

### Last-touch attribution

How it works: Credit goes to the last touchpoint before conversion.

Pros:
- Simple
- No double counting
- Easy to implement

Cons:
- Ignores upper-funnel contributions
- Biased toward channels that close (search, brand)
- Punishes channels that assist (display, awareness)

When to use: Quick directional reads, simple businesses, when you need one number.

### Multi-touch attribution (MTA)

How it works: Credit distributed across touchpoints based on position, time decay, or modeled weights.

Pros:
- Acknowledges full funnel
- More nuanced than last-touch
- Can customize rules

Cons:
- Requires user-level tracking (increasingly broken)
- Rules are arbitrary (why 40% to first touch?)
- Doesn't prove causation
- Privacy constraints killing it

When to use: Where user-level paths still trackable, with caveats acknowledged.

### Incrementality testing

How it works: Randomized experiments measuring lift from exposure vs holdout.

Pros:
- Actually measures causation
- Gold standard for validation
- Platform-agnostic when designed well

Cons:
- Expensive (holdout = lost revenue)
- Slow (need statistical power)
- Point-in-time (doesn't cover full mix continuously)
- Can't run on everything at once

When to use: Calibration of key channels, validating big investments, settling debates.

### Marketing mix modeling (MMM)

How it works: Regression on aggregate data estimating contribution of each channel.

Pros:
- No user-level tracking required
- Covers full channel mix
- Handles cross-channel holistically
- Privacy-proof

Cons:
- Requires sufficient data history
- Cannot do real-time optimization
- Needs calibration with incrementality
- Aggregate (no user-level insights)

When to use: Strategic planning, budget allocation, cross-channel view.

### Hybrid approaches

Most mature organizations combine:

| Use case | Approach |
|----------|----------|
| Strategic planning | MMM |
| Tactical optimization | Platform signals (with skepticism) |
| Validation | Incrementality testing |
| Reconciliation | MMM as arbiter |

No single approach solves everything. Portfolio of methods is the answer.

---

## MMM as the arbiter

MMM has a unique role in cross-channel measurement. It's the only approach that sees everything at once without relying on user-level tracking.

### Why MMM can arbitrate

**Holistic view:**
MMM models total outcomes as a function of all inputs. It naturally forces contributions to sum to 100% (or close). The double-counting problem doesn't exist because you're not adding up channel reports.

**Aggregate by design:**
MMM doesn't need to match users across platforms. It works with total spend and total outcomes. Walled gardens become irrelevant at the aggregate level.

**Accounts for interaction:**
MMM can model channel interactions. TV lifts paid search. Brand lifts performance. These effects are captured in a holistic model, not double-counted.

### How to position MMM vs platform reporting

**MMM is for allocation. Platform reports are for optimization.**

| Question | Use |
|----------|-----|
| How should I split budget across channels? | MMM |
| Is this Meta campaign better than that one? | Platform reporting |
| What's the true incremental value of TV? | MMM (calibrated with lift) |
| Should I pause this keyword? | Platform reporting |
| How much did each channel contribute to Q4? | MMM |

### When to trust platform vs MMM

Trust platform reporting when:
- Optimizing within a platform
- Making tactical creative/targeting decisions
- Directional read on campaign performance
- Same-platform comparisons

Trust MMM when:
- Allocating across platforms
- Evaluating channel incremental value
- Strategic planning
- Reconciling conflicting reports

### Explaining the difference to stakeholders

**Simple framing:**

"Platform reports tell you how many people touched your ads before converting. That's useful for understanding reach. MMM tries to estimate how many additional conversions happened because of your ads. That's the incremental value. Both are valid. They answer different questions."

**Why they differ:**

"If Meta says they drove 10,000 conversions, they're saying 10,000 people saw Meta ads and converted. MMM might say 6,000 of those conversions were incremental. The other 4,000 would have converted anyway. That's why MMM is lower. It's not disagreeing. It's measuring something different."

---

## Channel-specific considerations

Different channels have different measurement quirks. Know them.

### Paid search

**What's unique:**
- High intent (users are searching)
- Keyword-level granularity
- Brand vs non-brand behave differently
- Strong last-touch performance

**Measurement challenges:**
- Brand search is often capturing existing demand, not creating it
- Non-brand harder to separate from brand halo
- Platform reporting doesn't separate incrementality

**MMM considerations:**
- May need to separate brand/non-brand
- Diminishing returns curve often steep
- Watch for organic cannibalization

### Paid social (Meta, TikTok, etc.)

**What's unique:**
- Interruption-based (users not searching)
- Heavy view-through attribution
- Strong targeting capabilities
- Creative-dependent performance

**Measurement challenges:**
- View-through is where double-counting lives
- Attribution windows vary by platform
- iOS privacy changes hit hard
- Cross-device paths common

**MMM considerations:**
- Adstock effects matter (delayed response)
- May need longer lag structures
- Platform-reported conversions are inflated

### Video/streaming (YouTube, CTV)

**What's unique:**
- Awareness-oriented
- Longer consideration cycles
- Harder to track direct response
- Growing share of mix

**Measurement challenges:**
- View-through is majority of attribution
- Cross-device measurement weak
- Incrementality testing expensive
- Brand effects hard to isolate

**MMM considerations:**
- Longer adstock decay
- May need brand metrics as outcomes
- Calibration especially important

### Programmatic display

**What's unique:**
- Retargeting heavy
- Lower funnel attribution
- Fraud and viewability concerns
- Complex supply chain

**Measurement challenges:**
- Retargeting claims credit for already-likely converters
- Viewability varies wildly
- Fraud can inflate metrics
- Impression counting inconsistent

**MMM considerations:**
- Often overattributed in platform reports
- May need fraud/viewability adjustments
- Separate prospecting vs retargeting if possible

### TV and offline

**What's unique:**
- Broad reach
- No user-level tracking
- Longer response curves
- Brand building role

**Measurement challenges:**
- No click-through
- Delayed response (days/weeks)
- Hard to isolate from other media
- Expensive to test

**MMM considerations:**
- MMM is primary measurement method
- Adstock modeling critical
- Calibration with matched market tests
- Baseline effects matter

### Retail media

**What's unique:**
- Close to purchase
- Closed-loop measurement (for that retailer)
- Growing channel
- Retailer controls data

**Measurement challenges:**
- Walled garden within walled gardens
- Only see conversions on that retailer
- May cannibalize organic sales on retailer
- Limited view of full funnel

**MMM considerations:**
- Need retailer data share or estimates
- May overattribute (capturing existing demand)
- Consider retailer sales as separate outcome

---

## Building cross-channel reporting products

If you're building reporting that spans channels, design with cross-channel challenges in mind.

### Data ingestion challenges

**Consistency problems:**

- Different attribution windows by platform
- Different conversion definitions
- Different time zones and reporting delays
- Different granularity levels

**Normalization needs:**

- Standardize attribution windows for comparison
- Align conversion definitions
- Convert to common time zone
- Define minimum granularity

### Deduplication approaches

**Option 1: Don't deduplicate, just show**
Show platform-reported alongside MMM-estimated. Let users see the gap.

**Option 2: Use MMM as truth**
Show MMM contribution as the "real" number. Platform numbers in detail view only.

**Option 3: Adjust with factors**
Apply adjustment factors based on historical MMM vs platform gaps.

**Recommendation:** Option 2 for strategic views. Option 1 for operational views with clear labeling.

### Reporting hierarchy design

```
Level 1: Total Marketing
  - MMM-estimated total contribution
  
Level 2: Channel Category
  - Paid Search, Paid Social, Video, Display, etc.
  - MMM-estimated contribution per category
  
Level 3: Platform
  - Google, Meta, TikTok, etc.
  - Platform-reported metrics
  - MMM estimate where available
  
Level 4: Campaign/Tactic
  - Platform-reported only (MMM doesn't go this deep)
  - Clear labeling that this is platform-reported
```

### The "single source of truth" trap

There is no single source of truth in cross-channel measurement. Anyone who tells you otherwise is selling something.

**What to aim for instead:**

- Clear hierarchy of metrics for different decisions
- Transparency about what each metric does and doesn't measure
- Consistent methodology over time
- Explicit uncertainty where it exists

---

## What to tell stakeholders

Cross-channel confusion is a stakeholder management problem as much as a technical one.

### Setting expectations upfront

"Our platform reports will always add up to more than our actual conversions. That's how attribution works. We use MMM to estimate the true incremental contribution of each channel. Those two numbers serve different purposes."

### Why numbers differ

| Source | What it measures | When to use |
|--------|------------------|-------------|
| Platform reports | Touchpoints before conversion | Optimizing within platform |
| MMM | Estimated incremental contribution | Allocating across platforms |
| Incrementality tests | Causal impact of specific intervention | Validating key channels |

### The 100% conversation

Stakeholders want contributions to sum to 100%. Platform reports won't. MMM can.

"If you need a view where everything adds to 100%, that's MMM. If you need to optimize a Meta campaign, use Meta reporting. Different tools for different jobs."

### When stakeholders push back

**"But Meta says they drove 10,000 conversions"**

"They're saying 10,000 people saw Meta ads and converted. Some of those people would have converted anyway. MMM estimates how many additional conversions happened because of Meta. Both numbers are real. They measure different things."

**"I don't trust models, I trust data"**

"The platform data is also modeled. They're estimating which conversions to credit to which ads. They're just not showing you the model. At least with MMM, you can see the methodology."

---

## Checklist

Before launching cross-channel reporting, confirm:

- [ ] Double-counting dynamics documented and explained to stakeholders
- [ ] Platform reporting limitations acknowledged
- [ ] MMM or aggregate approach in place for allocation decisions
- [ ] Hierarchy clear: what to use for what decision
- [ ] Attribution windows normalized or differences flagged
- [ ] Channel-specific quirks accounted for
- [ ] Stakeholder education complete
- [ ] "Numbers don't add up" conversation had proactively
- [ ] Incrementality tests planned for key channel calibration
- [ ] Reporting hierarchy designed with decision levels in mind
