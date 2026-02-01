# Build vs Buy: Meridian, Robyn, or Custom MMM?

The MMM landscape changed fast. Five years ago, your options were expensive vendors or build from scratch. Now you have Google and Meta giving away open-source frameworks. Vendors are scrambling to differentiate. Internal teams are wondering what to build.

This doc defines how to evaluate MMM build vs buy: the current landscape, what each option actually offers, tradeoffs that matter, and a decision framework for choosing.

## Contents

- [The current landscape](#the-current-landscape)
- [Open source options](#open-source-options)
- [Vendor solutions](#vendor-solutions)
- [Custom builds](#custom-builds)
- [Decision framework](#decision-framework)
- [Migration considerations](#migration-considerations)
- [What I'd recommend](#what-id-recommend)
- [Checklist](#checklist)

---

## The current landscape

MMM is having a moment. Privacy constraints made user-level attribution unreliable. Platforms responded by investing in aggregate measurement. Open-source options emerged. The barrier to entry dropped.

### What changed in 2023-2025

| Before | Now |
|--------|-----|
| MMM = expensive consultants | Open-source options available |
| Black-box vendor models | Transparent methodologies |
| Quarterly refreshes | Weekly/monthly possible |
| Custom builds = 6+ months | Frameworks accelerate to weeks |
| Bayesian was niche | Bayesian is mainstream |

### The major categories

**Open source frameworks:**
- Meridian (Google)
- Robyn (Meta)
- LightweightMMM (Google/DeepMind)
- PyMC Marketing

**Full-service vendors:**
- Measured
- Rockerbox
- Analytic Partners
- Marketing Evolution
- Neustar (TransUnion)
- Nielsen

**Consultancies/agencies:**
- Bespoke builds
- Framework customization
- Managed services

**Internal custom:**
- Built from scratch
- Full control
- Significant investment

---

## Open source options

Open source lowered the barrier. It didn't eliminate the work.

### Meridian (Google)

**What it is:**
Google's open-source Bayesian MMM framework. Built on JAX. Designed for scale.

**Architecture:**
- Hierarchical Bayesian model
- Adstock and saturation built-in
- Geo-level modeling support
- GPU acceleration via JAX

**Strengths:**
- Google's engineering quality
- Bayesian uncertainty quantification
- Scales well to large datasets
- Active development
- Integrates with Google ecosystem

**Limitations:**
- Newer (less community than Robyn)
- JAX learning curve
- Documentation still maturing
- Assumptions may favor Google channels (unproven, but watch for it)

**Best fit:**
- Teams with Python/JAX experience
- Large-scale advertisers
- Organizations comfortable with Bayesian methods
- Those wanting Google ecosystem alignment

**What to watch for:**
- Prior specification matters a lot (defaults may not fit your business)
- Need to validate against non-Google incrementality
- Requires data science investment to operate

### Robyn (Meta)

**What it is:**
Meta's open-source MMM package. Built in R. Widely adopted.

**Architecture:**
- Frequentist with some Bayesian elements
- Ridge regression base
- Nevergrad for optimization
- Built-in visualizations

**Strengths:**
- Mature and battle-tested
- Large community
- Good documentation
- Fast to get started
- Built-in calibration support

**Limitations:**
- R-based (some teams prefer Python)
- Less rigorous uncertainty quantification than full Bayesian
- Optimization can find local minima
- Meta-centric assumptions in defaults

**Best fit:**
- Teams with R experience
- Getting started with MMM quickly
- Mid-size advertisers
- Those wanting community support

**What to watch for:**
- Multiple "good" solutions possible (optimizer sensitivity)
- Calibration with experiments strongly recommended
- May need customization for non-standard media

### LightweightMMM (Google/DeepMind)

**What it is:**
Earlier Google open-source MMM. Bayesian. NumPyro-based.

**Architecture:**
- Bayesian hierarchical model
- Simpler than Meridian
- NumPyro/JAX foundation

**Strengths:**
- Solid Bayesian foundation
- Relatively simple to understand
- Good for learning Bayesian MMM
- Can be starting point for custom

**Limitations:**
- Less actively developed (Meridian is the focus now)
- Fewer features than Meridian
- Smaller community
- Documentation limited

**Best fit:**
- Learning Bayesian MMM
- Simple use cases
- Starting point for customization

**What to watch for:**
- May not scale as well as Meridian
- Less ongoing investment from Google

### PyMC Marketing

**What it is:**
Bayesian MMM built on PyMC. Part of broader PyMC ecosystem.

**Architecture:**
- Full Bayesian via PyMC
- Flexible model specification
- Part of established Bayesian Python ecosystem

**Strengths:**
- Full Bayesian flexibility
- Strong ecosystem (PyMC, ArviZ)
- Active Bayesian community
- Can customize deeply
- Good uncertainty quantification

**Limitations:**
- Requires Bayesian expertise
- Less plug-and-play than Robyn
- Smaller MMM-specific community
- Need to specify more yourself

**Best fit:**
- Teams with Bayesian experience
- Those wanting maximum flexibility
- Custom model requirements
- Organizations already using PyMC

**What to watch for:**
- More expertise required to avoid mistakes
- Less MMM-specific documentation
- Need to build more infrastructure yourself

### Open source comparison

| Factor | Meridian | Robyn | LightweightMMM | PyMC Marketing |
|--------|----------|-------|----------------|----------------|
| Language | Python/JAX | R | Python/JAX | Python/PyMC |
| Approach | Bayesian | Freq + Bayesian | Bayesian | Bayesian |
| Maturity | Newer | Mature | Older | Growing |
| Community | Growing | Large | Small | Medium |
| Flexibility | Medium | Medium | Low | High |
| Learning curve | Medium | Low | Low | High |
| Uncertainty | Strong | Moderate | Strong | Strong |
| Scale | High | Medium | Medium | Medium |
| Active dev | High | Medium | Low | Medium |

---

## Vendor solutions

Vendors provide more than software. They provide implementation, support, and sometimes credibility.

### When to consider vendors

**Good reasons:**
- No internal data science capacity
- Need fast time-to-value
- Want external credibility with stakeholders
- Complex data integration needs
- Prefer managed service to internal build

**Bad reasons:**
- "Everyone uses them" (not a strategy)
- Avoiding internal capability building
- Assuming vendor = automatically better
- Checkbox for leadership

### What you get with vendors

**Typically included:**
- Data ingestion and cleaning
- Model building and maintenance
- Visualization/dashboard
- Refresh cadence management
- Stakeholder presentations
- Methodology documentation

**Sometimes included:**
- Custom model development
- Integration with planning tools
- Scenario simulation
- Calibration study support

**Rarely included:**
- Full methodology transparency
- Ability to audit model internals
- Ownership of the model
- Portability to another solution

### Evaluation criteria

| Criteria | Questions to ask |
|----------|------------------|
| Methodology | Is it Bayesian? What assumptions? Can you see the model? |
| Transparency | Can you audit results? Understand priors? |
| Data requirements | What data do they need? What if you don't have it? |
| Refresh cadence | How often can you update? What's the lag? |
| Calibration | Do they support incrementality integration? |
| Customization | Can you adjust model for your business? |
| Portability | What happens if you leave? Do you keep anything? |
| Support | Who's your contact? What's response time? |
| Total cost | License + implementation + ongoing + overage |

### The black box problem

Most vendors won't show you the model. You get inputs and outputs. The middle is proprietary.

**Problems this creates:**
- Can't validate methodology
- Can't explain results at technical level
- Can't customize for your business
- Vendor dependency for any change
- Hard to debug unexpected results

**Questions to ask:**
- Can we see the model specification?
- Can we audit the priors?
- Can we run our own validation?
- What happens if we disagree with results?

### Contract considerations

**Watch for:**
- Data usage rights (can they use your data for other clients?)
- Termination terms (how hard to leave?)
- Price escalation (what happens at renewal?)
- Scope creep pricing (what's included vs extra?)
- Deliverable ownership (do you own the methodology?)

---

## Custom builds

Building from scratch is an option. It's more option than most teams need.

### When custom makes sense

**Good reasons:**
- Unique business model that frameworks don't fit
- Deep internal data science expertise
- Long-term strategic investment in measurement
- Need for deep integration with internal systems
- Regulatory or compliance requirements for transparency

**Bad reasons:**
- "We can do it better" (usually wrong)
- Not invented here syndrome
- Underestimating maintenance burden
- Avoiding learning existing tools

### What custom requires

**Team:**
- Senior data scientist with Bayesian experience (minimum)
- Data engineer for pipeline work
- PM to manage requirements and stakeholders
- Ongoing maintenance capacity

**Timeline:**
- Initial build: 3-6 months (realistic)
- Production-ready: 6-12 months
- Ongoing maintenance: 20-40% of initial build effort annually

**Skills:**
- Bayesian statistics (not just awareness, actual expertise)
- Time series modeling
- Marketing domain knowledge
- Production ML engineering
- Stakeholder communication

### The maintenance burden

Custom builds are never done. They require:

- Data pipeline maintenance
- Model monitoring and drift detection
- Periodic retraining and recalibration
- Bug fixes and edge cases
- Documentation updates
- Knowledge transfer when people leave
- Stakeholder support and education

Underestimating maintenance is the #1 custom build failure.

### The hybrid path

Most successful organizations don't build from scratch. They:

1. Start with open source framework
2. Customize where needed
3. Build proprietary layers on top
4. Maintain core framework alignment for updates

This gives you:
- Faster start
- Community support
- Framework updates
- Custom fit where it matters

---

## Decision framework

### Questions to answer first

Before evaluating options, clarify:

1. **What's your timeline?**
   - Need something in weeks: Robyn or vendor
   - Have 3-6 months: Meridian, PyMC, or custom on framework
   - Have 6+ months: Any option including full custom

2. **What's your internal capability?**
   - No data science: Vendor
   - Some data science: Open source with support
   - Strong data science: Open source or custom

3. **What's your budget?**
   - Minimal: Open source
   - Moderate: Open source + consulting support
   - Significant: Vendor or well-staffed internal

4. **What's your scale?**
   - Small/mid advertiser: Robyn, vendor
   - Large advertiser: Meridian, vendor, or custom
   - Enterprise: Meridian, custom, or enterprise vendor

5. **What's your stakeholder environment?**
   - Need external credibility: Vendor or big-name open source
   - Technical stakeholders: Open source fine
   - Non-technical stakeholders: Need polished output regardless of backend

### Decision matrix

| Situation | Recommendation |
|-----------|---------------|
| No data science, need it now | Vendor |
| Some data science, need it fast | Robyn |
| Strong data science, strategic investment | Meridian or PyMC |
| Unique requirements, strong team | Custom on framework |
| Large enterprise, complex needs | Meridian + internal team or enterprise vendor |
| Learning/experimenting | Robyn or LightweightMMM |
| Maximum flexibility needed | PyMC Marketing or custom |

### Red flags by option

**Open source red flags:**
- No one internal can maintain it
- Expecting plug-and-play (it's not)
- No plan for calibration
- Underestimating stakeholder education needs

**Vendor red flags:**
- Can't explain methodology at all
- Won't allow any validation
- Long-term lock-in with no portability
- Costs escalate unpredictably
- Refresh cadence doesn't fit your needs

**Custom red flags:**
- Team has never done Bayesian modeling
- Timeline is "a few months" (it's always longer)
- No maintenance plan
- Single person dependency
- Building to prove a point, not solve a problem

---

## Migration considerations

If you have an existing solution, migration is its own project.

### Migrating from vendor to open source

**Why teams do it:**
- Cost reduction
- More control
- Transparency needs
- Vendor relationship issues

**Challenges:**
- Methodology may differ (results won't match exactly)
- Stakeholders anchored on old numbers
- Knowledge gap if team relied on vendor
- Data pipeline work

**Approach:**
- Run in parallel for 2+ quarters
- Explain methodology differences upfront
- Recalibrate with incrementality
- Don't promise identical results

### Migrating between open source frameworks

**Common moves:**
- Robyn to Meridian (R to Python, frequentist to Bayesian)
- LightweightMMM to Meridian (within Google ecosystem)

**Challenges:**
- Different defaults and assumptions
- Results will differ
- Learning curve on new framework

**Approach:**
- Document current methodology clearly
- Understand what's driving differences
- Parallel run for validation
- Stakeholder communication on change

### Migrating from custom to framework

**Why teams do it:**
- Maintenance burden
- Key person left
- Framework caught up to custom features
- Want community support

**Challenges:**
- Custom features may not exist in framework
- Attached to "our" methodology
- Migration requires understanding both

**Approach:**
- Inventory what custom model does
- Map to framework capabilities
- Accept some differences
- Plan for custom extensions where needed

---

## What I'd recommend

Based on common situations:

### Small/mid advertiser, limited data science

**Recommendation:** Robyn with consulting support for setup

Why: Fast to start, large community, consulting help available, lower barrier.

### Mid/large advertiser, some data science

**Recommendation:** Meridian with internal ownership

Why: Bayesian rigor, scales well, active development, builds internal capability.

### Enterprise, strong data science, strategic investment

**Recommendation:** Meridian or PyMC Marketing, heavily customized

Why: Maximum control, internal capability, long-term investment payoff.

### No internal capability, need credibility

**Recommendation:** Vendor with transparent methodology

Why: Managed service, external credibility, faster time-to-value.

### Learning and experimenting

**Recommendation:** Robyn first, then Meridian

Why: Robyn has lower barrier, then graduate to Bayesian rigor.

### General principle

Start with the simplest option that meets your needs. You can always graduate to more complex solutions. You can't easily recover from over-building too early.

---

## Checklist

Before committing to an MMM solution, confirm:

- [ ] Timeline is realistic for chosen approach
- [ ] Internal capability matches requirements
- [ ] Budget covers full lifecycle (not just initial build)
- [ ] Maintenance plan exists
- [ ] Stakeholder education planned
- [ ] Calibration with incrementality on roadmap
- [ ] Methodology transparency sufficient for your needs
- [ ] Exit plan exists (especially for vendors)
- [ ] Single-person dependency avoided
- [ ] Documentation requirements defined
- [ ] Success criteria defined (how will you know it's working?)
