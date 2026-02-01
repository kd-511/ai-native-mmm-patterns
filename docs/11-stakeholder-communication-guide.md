
# Stakeholder Communication Guide

Your model can be perfectly calibrated and still fail if nobody understands or trusts the outputs. Communication is not a soft skill bolted on at the end. It is a core product capability that determines whether measurement influences decisions or becomes expensive background noise.

This doc defines how to communicate MMM outputs to non-technical stakeholders: what to claim vs avoid, how to present uncertainty, how to handle objections, and templates for standard deliverables.

## Contents

- [Know your audience](#know-your-audience)
- [What to claim vs what not to claim](#what-to-claim-vs-what-not-to-claim)
- [Presenting uncertainty](#presenting-uncertainty)
- [Handling counterintuitive results](#handling-counterintuitive-results)
- [Handling objections](#handling-objections)
- [Executive summary templates](#executive-summary-templates)
- [Visual communication](#visual-communication)
- [Sales partnership](#sales-partnership)
- [Checklist](#checklist)

---

## Know your audience

Different stakeholders need different depths and framings. One deck does not fit all.

### Audience mapping

| Audience | What they care about | Depth needed | Key question they ask |
|----------|---------------------|--------------|----------------------|
| CMO/Exec | Business impact, strategic direction | High-level | "What should we do differently?" |
| Marketing Director | Channel performance, budget allocation | Medium | "Is my channel working?" |
| Media Planner | Tactical optimization, efficiency | Detailed | "Where do I shift spend?" |
| Finance | ROI, budget justification | Medium | "Is this spend justified?" |
| Sales (internal) | Client-ready insights | Simple | "What do I tell the advertiser?" |
| Data Science | Methodology, uncertainty | Deep | "How confident are we?" |

### Tailoring your communication

**For executives:**

- Lead with decisions, not methodology
- One page max before appendix
- Clear recommendation with rationale
- Acknowledge uncertainty without drowning in it

**For marketing directors:**

- Channel-level detail
- Comparison to previous period
- Actionable insights for their scope
- Anticipate their questions

**For media planners:**

- Granular enough to act on
- Clear optimization direction
- Practical constraints acknowledged
- Follow-up path for questions

**For finance:**

- ROI framing
- Confidence intervals on returns
- Comparison to alternatives
- Investment language, not media jargon

---

## What to claim vs what not to claim

Overclaiming destroys trust faster than being wrong. Be precise about what the model does and doesn't tell you.

### Safe claims

These are defensible with appropriate caveats:

**Relative performance:**
- "Channel A appears more efficient than Channel B based on historical patterns"
- "Increasing spend in Channel A has historically been associated with stronger returns than Channel B"

**Directional guidance:**
- "The data suggests reallocating from X to Y would improve overall efficiency"
- "Diminishing returns appear to set in above $X spend level for this channel"

**Uncertainty-acknowledged estimates:**
- "Our estimate is $X with a range of $Y to $Z"
- "We're reasonably confident the true value is within this range"

**Conditional recommendations:**
- "If the goal is to maximize short-term conversions, the model suggests..."
- "Under current market conditions, the data indicates..."

### Dangerous claims

These will backfire. Avoid them:

**False precision:**
- "ROI is exactly 2.47x" (implies certainty that doesn't exist)
- "Optimal spend is $4,237,891" (spurious precision)

**Causal certainty from observational data:**
- "This channel caused X conversions" (MMM shows association, not proof)
- "If you spend $X, you will get Y" (prediction, not guarantee)

**Ignoring uncertainty:**
- "The model says X" without ranges (hides uncertainty)
- "This is what the data shows" (implies objectivity that obscures assumptions)

**Extrapolation as fact:**
- "Double the spend and you'll double the returns" (ignores diminishing returns)
- "This will work in Q4" (model trained on different conditions)

### The language of appropriate confidence

| Instead of... | Say... |
|---------------|--------|
| "The model says" | "The model suggests" or "The data indicates" |
| "ROI is 2.5x" | "ROI is estimated at 2.5x (range: 2.0-3.0x)" |
| "This channel drove X" | "This channel is associated with X" |
| "You should spend $X" | "The model suggests $X would optimize for [goal]" |
| "This is the answer" | "This is our best estimate given available data" |

---

## Presenting uncertainty

Uncertainty is a feature, not a bug. Present it as valuable information.

### Why uncertainty matters to stakeholders

Stakeholders make bets. They need to know:

- How much confidence to put in this recommendation
- What's the downside if the estimate is wrong
- Whether to wait for more data or act now
- How to hedge their decisions

Hiding uncertainty doesn't help them. It sets them up to be surprised.

### Uncertainty display patterns

**Ranges, not just points:**

Bad: "Channel A ROI: 2.5x"
Good: "Channel A ROI: 2.5x (likely range: 2.0x - 3.1x)"

**Confidence tiers:**

High confidence: "Strong signal, consistent across time periods, narrow range"
Medium confidence: "Reasonable signal, some variation, moderate range"
Low confidence: "Weak signal, high variation, wide range or limited data"

**Decision-relevant framing:**

Instead of: "95% CI is 1.8 to 3.2"
Try: "Even in pessimistic scenarios, this channel breaks even. In optimistic scenarios, it's our best performer."

**Visual indicators:**

- Color coding for confidence levels
- Error bars on charts (where appropriate for audience)
- Explicit "high/medium/low confidence" labels

### What not to do

- Don't bury uncertainty in footnotes nobody reads
- Don't show 47 decimal places of false precision
- Don't use statistical jargon without translation
- Don't hide wide intervals behind point estimates

---

## Handling counterintuitive results

Sometimes the model says something stakeholders don't want to hear. This is when trust is built or broken.

### Why results seem counterintuitive

**Model is right, intuition is wrong:**
- Intuition based on incomplete information
- Confusing correlation with causation
- Anchoring on platform-reported metrics
- Not accounting for diminishing returns

**Model is wrong, intuition is right:**
- Data quality issues
- Model specification problems
- Important variables omitted
- Context the model can't see

**Both are partially right:**
- Different time horizons
- Different definitions of success
- Different segments behaving differently
- Uncertainty overlaps

### Before presenting counterintuitive results

Do your homework first:

1. **Pressure test the finding**
   - Is the data clean?
   - Is the model well-specified?
   - Does the result persist across specifications?
   - What's the uncertainty around it?

2. **Understand the stakeholder's prior**
   - What do they believe today?
   - What's that belief based on?
   - What would change their mind?

3. **Prepare the narrative**
   - Why might this be true?
   - What evidence supports it?
   - What would we expect to see if it's wrong?

### Presenting counterintuitive results

**Lead with curiosity, not certainty:**
- "The model is showing something interesting that I want to walk through"
- "This challenges some of our assumptions, and I want to explore it together"

**Acknowledge their perspective:**
- "I know this is different from what platform reporting shows"
- "This surprised us too, so we dug deeper"

**Show your work:**
- "Here's why the model might be seeing this"
- "Here's what we checked to validate"
- "Here's what we're still uncertain about"

**Propose a path forward:**
- "We could run an incrementality test to validate"
- "Let's watch this metric over the next quarter"
- "Here's what would change our conclusion"

### When to hold back results

Sometimes discretion matters:

- Finding is within noise range (don't present noise as signal)
- Data quality issues unresolved (fix first, then share)
- Context is missing (get the full picture)
- Timing is wrong (major decision already made, wait for next cycle)

Holding back is not hiding. It's responsible communication.

---

## Handling objections

Objections are buying signals. They mean stakeholders are engaged. Handle them well.

### "This doesn't match what we see in platform"

**Why they say it:** Platform metrics are their daily dashboard. MMM disagrees with their reality.

**How to respond:**

"That's expected, and here's why. Platform reporting counts everyone who saw or clicked an ad before converting. MMM tries to estimate what would have happened without the ad. Platform gives you credit. MMM tries to isolate incremental impact. Both are valid for different questions."

**Follow-up:** Offer to walk through specific differences. Show where MMM and platform agree vs diverge.

### "Last quarter you said something different"

**Why they say it:** They remember a previous number. Credibility at stake.

**How to respond:**

"You're right, and here's what changed. [New data / methodology update / market shift]. I should have flagged the update more clearly. Here's how we'll communicate changes going forward."

**Follow-up:** Commit to clearer versioning and change communication.

### "Can you just give me one number?"

**Why they say it:** Ranges feel like hedging. They want clarity.

**How to respond:**

"I can give you our best estimate: X. But I'd be doing you a disservice if I didn't tell you the realistic range is Y to Z. If you're making a $5M decision, knowing it could be 20% higher or lower matters."

**Follow-up:** Offer to frame the range in decision-relevant terms.

### "Why should I trust a model over my intuition?"

**Why they say it:** They've been in market for years. Model is a black box.

**How to respond:**

"You shouldn't trust it blindly. Your intuition catches things the model can't see. But the model processes more data than any human can and doesn't have the biases we all have. Best results come from combining both. Where does your intuition differ? Let's dig in."

**Follow-up:** Treat it as a collaborative investigation, not a debate.

### "The model must be wrong"

**Why they say it:** Results challenge their worldview or political position.

**How to respond:**

"It might be. Let's check. What specifically seems off? If we can identify what the model might be missing, we can investigate. If we can't find an issue, maybe the data is telling us something worth considering."

**Follow-up:** Propose specific validation steps. Offer calibration study if warranted.

---

## Executive summary templates

Standard formats reduce friction and build familiarity.

### Monthly refresh summary (one page)

```
# MMM Refresh Summary: [Month Year]

## Key Findings
[3-5 bullet points. Lead with most important.]

## Channel Performance Summary
[Table: Channel | ROI Estimate | Range | vs Last Month | Confidence]

## Recommended Actions
[2-3 specific, actionable recommendations]

## What Changed
[Brief note on any methodology updates or data changes]

## Confidence Notes
[Which estimates are high/medium/low confidence and why]

## Next Steps
[Calibration plans, follow-up analyses, decision timeline]
```

### Quarterly business review format

```
# Quarterly Measurement Review: [Quarter Year]

## Executive Summary
[One paragraph: key takeaway, main recommendation, confidence level]

## Performance Overview
[Channel-level performance with trends]

## Strategic Insights
[2-3 deeper insights with implications]

## Model Health
[Calibration status, stability metrics, data quality notes]

## Recommendations
[Prioritized list with rationale]

## Q&A Prep
[Anticipated questions with prepared responses]

## Appendix
[Methodology notes, detailed tables, technical details]
```

### Ad-hoc analysis template

```
# Analysis: [Specific Question]

## Question
[What we were asked to investigate]

## Approach
[How we investigated, briefly]

## Findings
[What we found, with uncertainty noted]

## Implications
[What this means for decisions]

## Caveats
[Limitations, assumptions, what we don't know]

## Recommendation
[Suggested action, if applicable]
```

---

## Visual communication

Charts can clarify or confuse. Design for clarity.

### Charts that work

**Bar charts for comparison:**
- Channel performance side by side
- Clear labels, sorted meaningfully
- Include confidence indicators where appropriate

**Line charts for trends:**
- Performance over time
- Clear axis labels
- Annotate key events

**Waterfall charts for decomposition:**
- What drove the change
- Base to final with contributions
- Intuitive flow

### Charts that confuse

**Pie charts:** Hard to compare. Use bar charts instead.

**Dual-axis charts:** Misleading scales. Separate into two charts.

**3D anything:** Distorts perception. Use 2D.

**Too many series:** More than 5-6 lines becomes noise. Aggregate or separate.

### Showing uncertainty visually

**Error bars:** Work for technical audiences. Overwhelming for execs.

**Ranges in tables:** "(2.0 - 3.0)" alongside point estimate. Accessible.

**Confidence shading:** Light shading around trend lines. Intuitive.

**Traffic light indicators:** Green/yellow/red for confidence level. Simple.

### The "so what" test

Before including any chart, ask:

- What decision does this inform?
- What action should someone take after seeing this?
- If the answer is "none," cut the chart.

---

## Sales partnership

If your measurement influences advertiser conversations, sales teams are key stakeholders.

### What sales needs vs what they ask for

**They ask for:** "Give me a deck I can show the client"

**They need:**
- Simple talking points (not methodology)
- Answers to likely client questions
- What to say when numbers look bad
- What NOT to promise

### Arming sales teams

**Create:**
- One-pagers by client segment
- FAQ documents for common questions
- Objection handling guides
- Clear escalation path for technical questions

**Train on:**
- What the model does and doesn't do
- How to explain uncertainty simply
- What claims are safe to make
- When to bring in measurement experts

### Feedback loops

Sales hears things you don't. Create channels for:

- Client reactions to measurement
- Questions they can't answer
- Competitive intelligence
- Feature requests from the field

---

## Checklist

Before any stakeholder communication, confirm:

- [ ] Audience identified and communication tailored
- [ ] Claims are appropriately hedged
- [ ] Uncertainty is visible, not hidden
- [ ] Counterintuitive results pressure-tested
- [ ] Prepared for likely objections
- [ ] Executive summary is one page
- [ ] Charts pass the "so what" test
- [ ] Sales has what they need (if applicable)
- [ ] Follow-up path clear
