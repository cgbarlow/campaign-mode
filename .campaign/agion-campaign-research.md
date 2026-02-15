# Campaign Mode × Agion: Adaptation Research & Options

## Executive Summary

This document analyses how Campaign Mode could be adapted to support and accelerate Agion Oy's mission as "The Agentic OS for the Sovereign Enterprise." It identifies deep structural alignments, enterprise adoption barriers, and presents four strategic options ranging from internal tooling to product integration.

The expanded analysis (Parts 8-14) deepens the case by examining Campaign Mode's theoretical grounding in Dr McCallum's Six-Animal Model and Self-Determination Theory, the role of cognitive diversity in preventing the blind spots that plague AI governance at scale, neurodiversity as a lens for seeing gaps in teams and workflows, Conway's Law implications for agent architecture, barriers specific to Agion's market position, and how Campaign Mode could serve as an internal operating system for Agion's own teams.

The DoView Planning analysis (Parts 16-20) introduces Dr Paul Duignan's visual strategy methodology — DoView Planning — grounded in outcomes theory, and explores the deep structural parallels between DoView diagrams, Campaign Mode, Six Animals, and the Agion platform. The analysis identifies DoView as the missing "strategy blueprint" layer in the governance stack and proposes a four-layer convergence thesis: visual outcomes architecture (DoView), cognitive diversity (Six Animals), lifecycle governance (Campaign Mode), and machine-speed enforcement (Agion).

---

## Part 1: Agion Mission Analysis

### What Agion Does
Agion provides a governance platform for enterprise AI agent deployments. Their core thesis: **"AI without control is as useless as no AI at all."** They solve two paradoxes:

1. **Speed vs. Control** — Moving fast with AI risks compliance gaps; moving slow defeats automation's purpose
2. **Scale vs. Oversight** — As agent numbers grow into thousands, human oversight becomes impossible

### AANG Framework (Five Principles)
| Principle | Description |
|-----------|-------------|
| **Mission-as-Code** | KPIs translated into executable agent missions |
| **Governance-as-Code** | Policies become automated, unbreakable rules |
| **Dynamic Trust** | Agent autonomy calibrated via real-time trust scoring |
| **Radical Transparency** | 100% auditable with immutable logging |
| **Human-AI Partnership** | Humans set strategy; agents execute |

### Target Market
Regulated enterprises: public administration, telecommunications, logistics, finance, healthcare, industrial operations. Nordic-founded, EU AI Act compliance built-in.

### Go-to-Market
90-day fixed-fee implementation: Discovery (Day 1) → Deployment (Weeks 1-6) → Go-live (Weeks 7-12).

---

## Part 2: Structural Alignments

Campaign Mode and Agion share surprisingly deep structural parallels:

| Campaign Mode Concept | Agion Equivalent | Alignment |
|----------------------|------------------|-----------|
| **Quest Definition** (success criteria) | **Mission-as-Code** (KPIs as executable missions) | Both define testable completion conditions upfront |
| **Dragon** (adversarial evaluation) | **Dynamic Trust Scoring** (real-time capability assessment) | Both independently evaluate whether agents meet criteria |
| **Guardian** (quality gates) | **Governance-as-Code** (automated policy enforcement) | Both prevent progression without meeting thresholds |
| **Context Isolation** (NPC independence) | **Audit Independence** (immutable logs, separated concerns) | Both enforce objective evaluation through structural separation |
| **Progress Log** (append-only) | **Immutable Audit Trail** | Both maintain transparent, tamper-resistant records |
| **Campaign Modes** (Grow/Ship) | **Trust Tiers** (escalating autonomy) | Both calibrate oversight intensity to context |
| **User as Protagonist** | **Human-AI Partnership** | Both position humans as strategic decision-makers, not passive observers |
| **Gandalf** (mentorship without rescue) | **Human Leverage Ratio** (amplification, not replacement) | Both amplify human capability without removing agency |

These are not surface similarities. The philosophical alignment is structural: both systems solve the same fundamental tension between autonomous execution and human oversight.

---

## Part 3: Enterprise Adoption Barriers

### Barrier 1: Fantasy Framing Creates Credibility Risk
**The problem:** "Quest," "Dragon," "Gandalf," and "Guardian" are evocative and memorable — for developers and creatives. In enterprise procurement conversations with CIOs, compliance officers, and board members in regulated industries, fantasy terminology creates immediate credibility friction.

**Severity: High.** Agion's target customers are public administration (KELA-scale), telcos, and financial institutions. A governance platform that mentions "slaying dragons" in the same breath as EU AI Act compliance will face rejection at the procurement stage, regardless of underlying quality.

**Mitigation path:** Campaign Mode already supports thematic re-skinning via character profiles. The architecture is sound — the naming layer needs an enterprise-neutral option.

### Barrier 2: Single-User Focus vs. Enterprise Team Scale
**The problem:** Campaign Mode is designed for one human protagonist working with AI agents. Agion's customers have teams of 5-50 people orchestrating thousands of AI agents. There's no concept of shared campaigns, role assignment across humans, or team-level progress tracking.

**Severity: High.** Enterprise adoption requires multi-stakeholder workflows. A governance framework that only works for solo practitioners won't survive contact with enterprise team structures.

**Mitigation path:** The animal archetypes (Bear=vision, Cat=risk, Owl=process, etc.) already map to enterprise team functions. The structural pattern could support human team members adopting archetype roles rather than AI agents playing them.

### Barrier 3: No Integration with Enterprise Governance Tooling
**The problem:** Enterprises have existing SDLC pipelines, compliance frameworks (ISO 27001, SOC 2, EU AI Act), change management processes, and audit systems. Campaign Mode operates as a standalone narrative layer with no hooks into these systems.

**Severity: Medium-High.** Agion already provides governance-as-code and audit trails. Campaign Mode would need to emit structured data (not just markdown progress logs) that integrates with enterprise observability and compliance tooling.

**Mitigation path:** The `.campaign/quest.md` state model could be extended to emit machine-readable events (JSON audit records, webhook notifications, JIRA/ServiceNow integration).

### Barrier 4: No Quantifiable ROI Story
**The problem:** Campaign Mode's value is experiential — better decision-making, reduced blind spots, quality gates preventing premature advancement. These are hard to quantify in enterprise business cases.

**Severity: Medium.** Agion already speaks the language of ROI (95% automated decision rate, 10ms policy validation). Campaign Mode needs to generate measurable outputs: cycle time reduction, defect rates at checkpoints, rework frequency after Dragon confrontations.

**Mitigation path:** Instrument the campaign lifecycle to capture metrics. Guardian block rates, Dragon pass/fail ratios, and time-to-checkpoint become KPIs.

### Barrier 5: Perceived Complexity of Onboarding
**The problem:** Campaign Mode has 10 agents, 6 phases, 3 isolation levels, 3 campaign modes, and character profiles. Enterprise teams need to understand the value proposition in under 2 minutes and start using it in under 30 minutes.

**Severity: Medium.** Agion's 90-day program already includes discovery and deployment phases that could absorb Campaign Mode onboarding. But the framework itself needs a "zero-config" enterprise entry point.

**Mitigation path:** Ship mode already streamlines the experience. An enterprise preset could auto-configure profiles, skip character setup, and use neutral terminology throughout.

### Barrier 6: Instruction-Based Isolation is Insufficient for Regulated Industries
**The problem:** Campaign Mode's context isolation between NPCs is enforced by prompt instructions, not architectural boundaries. In regulated industries where audit integrity is a legal requirement, "the AI was told not to share context" is not a defensible isolation guarantee.

**Severity: Medium for current use; High if positioned as governance tooling.** If Campaign Mode claims to provide independent evaluation (Dragon), that independence must be architecturally verifiable, not just instructionally asserted.

**Mitigation path:** This is already acknowledged in the north-star as a post-v1 evolution (API-based agents with hard isolation). Agion's platform architecture could provide the hard boundaries that Campaign Mode's design calls for.

---

## Part 4: Strategic Options

### Option A: Enterprise Skin — "Mission Mode"
**What:** Create an enterprise-neutral thematic layer for Campaign Mode. Same architecture, different vocabulary.

| Campaign Mode | Mission Mode (Enterprise) |
|---------------|--------------------------|
| Quest | Mission / Initiative |
| Gandalf (Mentor) | Advisor / Strategist |
| Dragon (Adversary) | Challenger / Auditor |
| Guardian (Gatekeeper) | Quality Gate / Compliance Gate |
| Campaign Mode | Engagement Mode |
| Grow / Ship | Learn / Deliver |
| Dragon Slain | Criteria Met / Approved |
| Dragon Prevails | Rework Required |
| Character Profiles | Role Configurations |
| Party | Team |

**Effort:** Low-Medium. Leverage existing theming/profile system. Create enterprise preset profiles for all NPCs and animals.

**Value for Agion:** Removes the single biggest barrier to enterprise conversations. Enables Agion to reference Campaign Mode's methodology without the fantasy framing. Could be used internally for Agion's own delivery methodology and externally as a customer-facing framework.

**Risk:** Dilutes the distinctive brand that makes Campaign Mode memorable in the developer community.

**Recommendation:** Implement as an alternative theme, not a replacement. Fantasy and Enterprise themes coexist via the existing profile system.

---

### Option B: 90-Day Implementation Accelerator
**What:** Structure Agion's 90-day customer implementation program as a Campaign Mode campaign.

| 90-Day Phase | Campaign Mapping |
|-------------|-----------------|
| **Discovery** (Day 1) | Phase 1: Quest Definition — Advisor frames the initiative, defines success criteria (governance KPIs, agent deployment targets, compliance requirements) |
| **Deployment** (Weeks 1-6) | Phase 3: Campaign Execution — Team works with animal archetypes mapped to enterprise functions (Bear=Strategy, Cat=Risk/Compliance, Owl=Project Management, Puppy=Change Management, Rabbit=Resources/Procurement, Wolf=Team Alignment) |
| **Milestone Reviews** (Weeks 3, 6, 9) | Phase 4: Guardian Checkpoints — Quality gates at key deployment milestones |
| **Go-Live** (Weeks 7-12) | Phase 5: Challenger Confrontation — Adversarial readiness assessment before production deployment |
| **Handover** | Phase 6: Debrief — Process retrospective, lessons learned, team capability assessment |

**Effort:** Medium. Requires enterprise skin (Option A) plus a pre-built "Agion 90-Day" quest template with standard success criteria, checkpoint definitions, and milestone structures.

**Value for Agion:** Differentiates Agion's implementation methodology from competitors. Provides structured quality gates that prevent premature go-lives (a common enterprise failure mode). Creates a repeatable, auditable implementation framework that customers can reference. The "Challenger confrontation" before go-live is a natural fit — no customer wants to deploy ungoverned AI agents into production without adversarial testing.

**Risk:** Over-structures a process that may need flexibility per customer. Campaign Mode's sequential phase model may not fit all implementation timelines.

**Recommendation:** Build as a configurable template, not a rigid process. Allow phases to overlap and checkpoints to be scheduled flexibly.

---

### Option C: Governance Methodology for Agent Missions
**What:** Adapt Campaign Mode's lifecycle as the human-facing orchestration layer for Agion's agent governance platform. Each "mission" (agent deployment initiative) follows the campaign lifecycle, with NPCs providing structured oversight.

**Conceptual Architecture:**
```
┌─────────────────────────────────────────────────┐
│  Agion Platform (Technical Layer)                │
│  - Governance-as-Code engine                     │
│  - Dynamic Trust Scoring                         │
│  - Immutable Audit Trail                         │
│  - Policy Validation (<10ms)                     │
└────────────────────┬────────────────────────────┘
                     │ Events, metrics, policy results
                     ▼
┌─────────────────────────────────────────────────┐
│  Campaign Mode (Human Orchestration Layer)       │
│  - Mission Definition (success criteria)         │
│  - Team Perspectives (animal archetypes)         │
│  - Quality Gates (Guardian → Governance Gate)    │
│  - Adversarial Testing (Dragon → Trust Auditor)  │
│  - Mentorship (Gandalf → Mission Advisor)        │
│  - Progress Tracking (audit-compatible logs)     │
└─────────────────────────────────────────────────┘
```

**Key Integration Points:**

1. **Mission-as-Code ↔ Quest Definition:** Success criteria in `.campaign/quest.md` map to Agion mission definitions. Machine-readable criteria could be bidirectionally synced.

2. **Governance-as-Code ↔ Guardian Checkpoints:** Guardian decisions (approve/block/conditional) could be informed by real-time policy validation results from the Agion platform. The Guardian becomes a human-readable interface to automated governance.

3. **Dynamic Trust ↔ Dragon Evaluation:** The Dragon's adversarial evaluation could incorporate trust scores from the Agion platform. An agent deployment that scores low on dynamic trust would face a harder Dragon confrontation.

4. **Immutable Audit ↔ Progress Log:** Campaign Mode's append-only progress log extends into Agion's immutable audit trail, providing human-context annotations alongside machine-generated audit records.

5. **Human-AI Partnership ↔ User as Protagonist:** Both systems position humans as strategic decision-makers. Campaign Mode provides the interaction pattern; Agion provides the technical enforcement.

**Effort:** High. Requires API integration, structured data models, and architectural alignment between Campaign Mode's markdown-based state and Agion's platform APIs.

**Value for Agion:** Creates a unique differentiator — no other governance platform provides structured human orchestration with adversarial testing and quality gates as a built-in methodology. Positions Agion as solving both the technical governance problem AND the human coordination problem. Gives customers a repeatable framework for the hardest part of agent deployment: the human decision-making around what to deploy, when to advance, and whether it's truly ready.

**Risk:** Scope is large. Integration complexity could delay both products. Campaign Mode's instruction-based isolation may not meet the auditability standards Agion promises.

**Recommendation:** Phase this. Start with Option A (skin) + Option B (90-day template) as near-term. Pursue Option C as a medium-term product integration with hard isolation as a prerequisite.

---

### Option D: Internal Team Operating System
**What:** Use Campaign Mode as Agion's own internal collaboration and delivery methodology.

**How it works:**
- Agion product development uses Campaign Mode to structure feature initiatives
- Each major feature/sprint is a campaign with defined success criteria
- Animal archetypes map to Agion team functions (already natural: Bear=product vision, Cat=security/risk, Owl=engineering process, Puppy=customer success, Rabbit=partnerships, Wolf=team health)
- Guardian checkpoints before merging major features
- Dragon confrontations before releases
- Council convened for strategic decisions (product direction, architecture choices, market pivots)
- Campaign Mode's Grow mode used for team skill development; Ship mode for delivery sprints

**Effort:** Low. Campaign Mode works today for this use case. Enterprise skin (Option A) is optional but recommended for team buy-in.

**Value for Agion:** Dogfooding creates authentic case study material. Surfaces product improvement ideas from daily use. Demonstrates to customers that Agion practices structured governance internally. The team builds intuition for how Campaign Mode feels in practice, informing future product integration decisions.

**Risk:** Low. Worst case: the team finds it doesn't add value to their workflow and stops using it. That's useful signal too.

**Recommendation:** Start here. It's the lowest-risk, fastest-feedback option. Learnings from internal use directly inform which of Options A/B/C to pursue and how.

---

## Part 5: Recommended Sequencing

```
Phase 1 (Now):     Option D — Internal dogfooding at Agion
                   ↓ learnings
Phase 2 (Near):    Option A — Enterprise skin ("Mission Mode")
                   ↓ enables
Phase 3 (Near):    Option B — 90-Day Implementation template
                   ↓ validates
Phase 4 (Medium):  Option C — Platform integration (requires hard isolation)
```

**Rationale:** Each phase validates assumptions for the next. Internal use (D) reveals what works. Enterprise skin (A) removes adoption barriers. The 90-day template (B) tests customer-facing value. Platform integration (C) is the highest-value but highest-risk option — it should be informed by everything learned in phases 1-3.

---

## Part 6: Enterprise Adoption Barrier Mitigation Summary

| Barrier | Options That Address It | Priority |
|---------|------------------------|----------|
| Fantasy framing credibility risk | **A** (enterprise skin) | Highest |
| Single-user focus | **B** (team roles in 90-day), **C** (multi-user missions) | High |
| No governance tooling integration | **C** (platform integration) | Medium-High |
| No quantifiable ROI | **B** (instrumented checkpoints), **C** (platform metrics) | Medium |
| Onboarding complexity | **A** (enterprise preset), **B** (pre-built template) | Medium |
| Instruction-based isolation insufficient | **C** (hard isolation via Agion platform) | Medium → High |

---

## Part 7: Open Questions for Decision

1. **Scope of engagement:** Is Campaign Mode being considered as an internal tool, a customer-facing methodology, a product integration, or all three?

2. **Brand strategy:** Should the enterprise skin replace or coexist with the fantasy theme? (Recommendation: coexist — different audiences, same architecture.)

3. **Multi-user priority:** How critical is multi-stakeholder support for Agion's immediate needs? The 90-day program involves multiple client stakeholders.

4. **Hard isolation timeline:** When does Agion's platform architecture support API-based agent isolation? This gates Option C's viability.

5. **IP and licensing:** Campaign Mode is CC-BY-SA-4.0. What are the implications for commercial integration with Agion's proprietary platform?

6. **Cultural fit:** Does Agion's team resonate with the Campaign Mode approach? Internal dogfooding (Option D) answers this empirically.

---
---

# EXPANDED ANALYSIS

---

## Part 8: Campaign Mode Benefits & Unexplored Use Cases

Before exploring Agion-specific applications, it is worth cataloguing the benefits Campaign Mode provides and the use cases it could serve beyond its current scope. Many of these have direct relevance to Agion's challenges.

### 8.1 Core Benefits of Campaign Mode

**Structured decision-making under uncertainty.** Campaign Mode imposes a deliberate lifecycle — define success criteria, execute, checkpoint, adversarially test, debrief — on work that would otherwise proceed without structure. This is the single most valuable property for any team deploying AI agents at scale: you cannot govern what you have not defined.

**Forced perspective diversity.** The Council feature convenes six independent cognitive perspectives (vision, risk, process, morale, resources, cohesion) before major decisions. Research shows cognitively diverse teams solve problems up to three times faster than homogeneous teams (HBR). Campaign Mode makes this structural, not optional.

**Quality gates that prevent premature advancement.** The Guardian's three gate decisions (approve, block, conditional) create explicit checkpoints that interrupt the "just push through" anti-pattern. In AI governance, premature deployment of insufficiently governed agents is the primary failure mode — the Guardian directly addresses this.

**Adversarial testing as a first-class activity.** The Dragon confrontation is not a code review or a QA pass. It is a deliberate, structurally isolated, adversarial evaluation of whether success criteria are genuinely met. This maps directly to the "red team" practice recommended by the EU AI Act for high-risk AI systems.

**Transformation tracking, not just task completion.** In Grow mode, Campaign Mode evaluates whether the user (or team) has genuinely learned, not just delivered. This is critical for Agion's customers, who need their teams to build AI governance capability, not just deploy a platform.

**Mentorship without rescue.** Gandalf's "guide on the side" philosophy — asking questions before giving answers, presenting options rather than directives — prevents learned helplessness. Teams that depend on consultants to make governance decisions will fail when the consultants leave. Campaign Mode's mentorship model builds self-sufficiency.

**Append-only audit trail.** The progress log in `.campaign/quest.md` creates a transparent, tamper-resistant record of decisions, checkpoints, and outcomes. This maps directly to compliance and auditability requirements in regulated industries.

### 8.2 Unexplored Use Cases

**Agent Mission Planning.** Each new AI agent deployment could be structured as a campaign: define the agent's mission criteria, identify risks (Cat), plan resources (Rabbit), checkpoint governance readiness (Guardian), adversarially test before production (Dragon). No one does this systematically today.

**Incident Response for Agent Failures.** When an AI agent causes a compliance incident, Campaign Mode's lifecycle could structure the response: define the incident scope (Quest Definition), assign investigation roles via animal archetypes, checkpoint remediation progress (Guardian), and adversarially test the fix before re-deployment (Dragon).

**Regulatory Compliance Readiness.** EU AI Act compliance requires documented risk assessment, human oversight mechanisms, and transparent audit trails. Campaign Mode's lifecycle maps to these requirements: risk assessment (Cat + Council), human oversight (Guardian checkpoints), audit trail (progress log), and adversarial testing (Dragon).

**Vendor Evaluation and Procurement.** Enterprises evaluating AI governance platforms (including Agion) could use Campaign Mode to structure the evaluation: define success criteria, assign evaluation perspectives to animal archetypes, checkpoint at each evaluation stage, and adversarially test the finalist against criteria.

**Team Capability Assessment.** Before deploying Agion's platform, customer teams need to assess their own governance maturity. The Council feature provides a structured multi-perspective diagnostic that reveals gaps in team capability, process, and resources.

**Post-Mortem and Learning.** Campaign Mode's debrief phase (especially in Grow mode) provides structured reflection that turns incidents into learning. Most enterprises skip this step or do it superficially. Campaign Mode makes it a first-class lifecycle phase.

---

## Part 9: Theoretical Grounding — McCallum's Six-Animal Model & Self-Determination Theory

Campaign Mode is not an ad-hoc collection of gamified features. It is built on Dr Simon McCallum's Six-Animal Model, which is itself grounded in one of the most well-established frameworks in motivational psychology: Deci and Ryan's Self-Determination Theory (SDT, 1985, 2000).

This theoretical grounding is what elevates Campaign Mode from "a nice way to organise work" to "a psychologically validated framework for team effectiveness." For Agion, this matters because it means Campaign Mode's approach to diverse perspectives is not arbitrary — it is a rigorous coverage model derived from human motivational needs.

### 9.1 Self-Determination Theory: Three Basic Needs

SDT identifies three basic psychological needs essential for well-being, intrinsic motivation, and optimal functioning:

| Need | Description | Group Expression |
|------|-------------|------------------|
| **Competence** | The need to feel effective, capable, and able to produce desired outcomes | Focus on quality, mastery, and output |
| **Relatedness** | The need to feel connected to others and to experience caring, supportive relationships | Focus on inclusion, harmony, and collaboration |
| **Agency** | The need to feel in control of one's own behaviour, choices, and direction | Focus on process, risk assessment, and independent decision-making |

Every person has all three needs, but their relative strength varies. The Six-Animal Model assigns each animal a primary and secondary need from SDT, creating six unique motivational profiles — one for each ordered permutation of the three needs.

### 9.2 The SDT-Animal Matrix

| Animal | Role | Primary Need | Secondary Need |
|--------|------|-------------|----------------|
| **Bear** | Visionary / Leader | Competence | Agency |
| **Wolf** | Manager | Relatedness | Agency |
| **Cat** | Risk Manager / Cynic | Agency | Competence |
| **Puppy** | Enthusiast | Relatedness | Competence |
| **Owl** | Process Master | Agency | Relatedness |
| **Rabbit** | Facilitator | Competence | Relatedness |

This is not a personality test. As the Six-Animal Model website states: *"The model doesn't tell you who you are. It gives you and your team a shared vocabulary for talking about the roles people play right now, in this group, on this task."*

The key insight: **these are behaviours, not traits, and behaviours can be learned.** The model explicitly encourages people to step into roles their team needs, even if those roles don't come naturally. This is critical for Agion's context — it means the framework can be adopted by any team regardless of composition.

### 9.3 Paired Coverage: Why Six Animals, Not Three

Each SDT need is the primary driver for two animals. The animals that share a primary need differ in their secondary need, giving each a distinct character within the same motivational family:

- **Competence pair:** Bear (+ Agency) and Rabbit (+ Relatedness) — both driven by quality, but Bear leads through vision while Rabbit enables through facilitation
- **Relatedness pair:** Wolf (+ Agency) and Puppy (+ Competence) — both driven by connection, but Wolf manages cohesion while Puppy maintains morale
- **Agency pair:** Cat (+ Competence) and Owl (+ Relatedness) — both driven by independent thinking, but Cat identifies risks while Owl manages process

This dual coverage means that when all six perspectives are active, every SDT dimension is addressed from two complementary angles. Remove any single perspective and the gap is predictable:

- **No Bear:** Group lacks direction; ideas fragment with no unifying vision
- **No Cat:** Risks go unidentified; groupthink and overconfidence dominate
- **No Owl:** Scope creep is rampant; meetings overrun without resolution
- **No Puppy:** Morale drops; creative ideas dismissed; negativity spiral
- **No Wolf:** Individuals work in silos; communication breaks down
- **No Rabbit:** Resources unavailable; external dependencies unmanaged

### 9.4 Why This Matters for Agion

The Six-Animal Model provides a **theoretically complete coverage model** for team decision-making. When Agion's customers deploy AI agents at scale, the decisions they make — which agents to deploy, what governance policies to apply, when to escalate, how to respond to incidents — require all six perspectives:

| Agion Decision Context | Missing Perspective | Predictable Failure |
|------------------------|-------------------|---------------------|
| Agent deployment strategy | No Bear (vision) | Agents deployed without clear mission alignment |
| Governance policy design | No Cat (risk) | Policies miss edge cases and failure modes |
| Implementation timeline | No Owl (process) | Scope creep; milestones missed; no accountability |
| Change management | No Puppy (morale) | Team resistance; adoption stalls; burnout |
| Resource planning | No Rabbit (facilitation) | Infrastructure gaps; vendor dependencies unmanaged |
| Stakeholder alignment | No Wolf (cohesion) | Silos between security, ops, and business teams |

Campaign Mode's Council feature convenes all six perspectives systematically, ensuring no critical dimension is overlooked. This is not a "nice to have" — it is a **governance quality assurance mechanism** grounded in motivational psychology.

### 9.5 Related Academic Foundations

The model draws on established research beyond SDT:

- **McClelland's Theory of Needs (1961)** — Achievement, Affiliation, Power mapping closely to Competence, Relatedness, Agency
- **Belbin's Team Roles (2010)** — Complementary team role theory, though Belbin uses nine roles without SDT grounding
- **Tuckman's Group Development (1965)** — Forming, Storming, Norming, Performing stages align with Campaign Mode's phase lifecycle
- **Edmondson's Psychological Safety (1999)** — The animal metaphor creates safe vocabulary for discussing role failures without triggering defensiveness
- **Vygotsky's Zone of Proximal Development** — Used by Guardian and Dragon to assess whether work represents genuine growth at the edge of capability

The model has been used successfully in Victoria University of Wellington's Executive MBA programme, SWEN303 User Experience courses, IMT3603 Game Development courses at NTNU, and professional workshops for organisations improving team effectiveness.

---

## Part 10: Cognitive Diversity as Quality Infrastructure for Agent Governance

### 10.1 The Cognitive Diversity Thesis

Cognitive diversity — the inclusion of varied reasoning styles, knowledge domains, and experiential worldviews — has been shown to help groups perform better in forecasting, ethical judgment, and institutional resilience. The research evidence is strong:

- Cognitively diverse teams of executives solved simulated problem sets **up to 3x faster** than homogeneous teams (HBR)
- Inclusive organisations are **75% more likely** to see ideas become productised and **87% more likely** to report better decision-making
- Diverse teams outperform homogeneous ones in profitability by **36%** (McKinsey)
- Teams with neurodivergent professionals in certain roles can be **30% more productive** (Deloitte)

But cognitive diversity without structure creates friction. As research consistently shows: *"Teams with cognitive diversity, but without the tools to manage it, often suffer from communication breakdowns, interpersonal tension, and 'us vs. them' dynamics."*

This is exactly what Campaign Mode provides: **structured cognitive diversity** — a framework that ensures all perspectives are heard without creating chaos.

### 10.2 How Campaign Mode Operationalises Cognitive Diversity

Campaign Mode doesn't just recommend diverse perspectives — it systematises them:

**The Council feature** convenes all six animal perspectives independently, then synthesises them through Simon. Each animal explores the project through their archetype lens, producing assessments that cannot influence each other. This is the team equivalent of what statisticians call "independent estimators" — diverse, uncorrelated judgments that combine to outperform any single perspective.

**Context isolation** prevents the Dragon and Guardian from being influenced by party reasoning. This is cognitive diversity at the evaluation level — the evaluators have genuinely different information sets, preventing the "we all looked at the same data and agreed" failure mode.

**Multi-classing compatibility** explicitly identifies which perspective combinations can be held by one person and which conflict (Cat + Puppy = incompatible; Cat + Owl = compatible). This prevents the cognitive dissonance that degrades performance when individuals are asked to simultaneously evaluate risk and champion ideas.

### 10.3 Filling Gaps in Agion's Agent Framework

Agion's AANG Framework is technically sophisticated — Mission-as-Code, Governance-as-Code, Dynamic Trust, Radical Transparency, Human-AI Partnership. But **technical frameworks have predictable blind spots** because they are designed by technically-oriented teams.

Consider which Six-Animal perspectives are likely underrepresented in a typical enterprise AI governance team:

| Perspective | Likely Present? | Why It Matters for Agent Governance |
|------------|----------------|-------------------------------------|
| **Bear** (vision) | Yes — product and strategy leaders | Agent deployment needs clear strategic alignment |
| **Cat** (risk) | Partially — security teams exist but may not be at the table | Risk assessment is the Cat's core function; missing Cat = groupthink |
| **Owl** (process) | Partially — project managers exist but governance process may be ad-hoc | Without Owl, governance becomes inconsistent and unrepeatable |
| **Puppy** (morale) | Rarely — not a traditional enterprise function | Change management and adoption depend on Puppy energy; without it, resistance wins |
| **Rabbit** (facilitation) | Sometimes — procurement and vendor management | Cross-team resource coordination is critical for platform deployments |
| **Wolf** (cohesion) | Rarely — no one is structurally responsible for team alignment | Security, ops, compliance, and business teams need active cohesion management |

The gap is predictable: **enterprise AI governance teams are typically heavy on Competence and Agency (Bear, Cat, Owl) and light on Relatedness (Wolf, Puppy, Rabbit)**. This means the human coordination dimensions — morale, cohesion, facilitation — are systematically underserved.

Campaign Mode's animal archetypes make these gaps visible and addressable. The Council diagnostic shows which perspectives are missing. The character profile system lets teams explicitly assign responsibility for underrepresented perspectives.

### 10.4 Cognitive Diversity in Agent Architecture Design

There is a deeper application: the principles of cognitive diversity apply not just to the human teams governing AI agents, but to the **design of the agent architectures themselves**.

Research from PMC on AI-assisted decision-making found that *"hybrid human-AI pairs, which combine human predictions with varying degrees of accurate AI predictions, can surpass the performance of either human-human or AI-AI pairs."* The key condition: **independence between human and AI predictions** — exactly what Campaign Mode's context isolation provides.

The implication for Agion: when designing multi-agent systems, the same principles that make diverse human teams effective apply to agent team composition. Agents with diverse reasoning approaches (different LLMs, different prompting strategies, different knowledge bases) produce better outcomes — provided their independence is maintained. Campaign Mode's isolation model is a template for this.

---

## Part 11: Neurodiversity — Seeing Gaps in Ourselves and Our Systems

### 11.1 The Neurodiversity Lens

The Six-Animal Model was explicitly designed with neurodiversity awareness as a key influence. As Dr McCallum's website states: *"The model acknowledges that different people have genuinely different motivational drives and communication styles. Rather than expecting everyone to conform to one mode of working, it creates space for varied approaches within a structured framework."*

This is not an afterthought — it is a design principle. The animal metaphor was chosen deliberately because it *"creates psychological separation from personal identity, making it easier to discuss roles without triggering defensiveness."* Saying "we need more Cat energy in this meeting" is far less threatening than "you're not being critical enough."

### 11.2 Neurodiversity in AI Governance: The Case for Inclusion

The World Economic Forum's 2025 analysis argues that neurodivergent individuals are not just users of AI — they could be its most vital architects. Their recommendations include:

- **Co-design with neurodivergent participants** at every stage, from brainstorming to deployment
- **Empower neurodivergent-led audits** to stress-test systems for ethical blind spots and edge cases
- **Flip the mentorship model** — pair leaders with neurodivergent mentors so those most impacted by technology guide those building it
- **Fund labs that think differently** — invest in innovation labs where neurodivergent creators prototype new approaches

Campaign Mode's structure aligns with all four recommendations. The animal framework provides cognitive diversity by design. The Dragon confrontation is an adversarial audit. The "guide on the side" mentorship model inverts traditional power dynamics. And the Campaign lifecycle itself creates a structured "lab" for different approaches.

### 11.3 How Campaign Mode Helps People See Their Own Gaps

The Six-Animal Model is fundamentally diagnostic: *"The model is diagnostic, not punitive. When a group is struggling, the question is not 'who is failing?' but 'which function is missing?'"*

This reframing is powerful for neurodivergent individuals and teams:

**For individuals:**
- The model shows that every cognitive style has value — the cautious analyst (Cat), the enthusiastic connector (Puppy), the independent process thinker (Owl)
- It validates different approaches rather than expecting conformity
- It makes explicit that no single person is expected to fill all roles — multi-classing compatibility rules show which roles naturally combine and which conflict
- It provides a vocabulary for communicating needs: "I'm strong in Cat but I need someone to be Puppy for me"

**For teams:**
- The Council diagnostic reveals which cognitive perspectives are systematically underrepresented
- The Group Failure Diagnosis framework maps symptoms to missing roles: "lack of direction" → no Bear, "risks go unidentified" → no Cat
- Common dysfunction patterns are named and normalised: "All Bear Team" (too many chiefs), "Cat Dominates Team" (paralysis by risk), "Missing Owl Team" (energy without structure)

**For workflows:**
- Campaign Mode's lifecycle forces perspective rotation — you cannot skip risk assessment (Cat), process planning (Owl), or morale check (Puppy) without noticing
- Guardian checkpoints create natural reflection points where gaps become visible
- The Dragon confrontation tests whether gaps have been genuinely addressed or merely papered over

### 11.4 Implications for Agion's Customers

Agion's regulated enterprise customers face a specific neurodiversity challenge: their governance teams tend to be cognitively homogeneous. Compliance, legal, and security professionals share similar training, similar risk frameworks, and similar communication styles. This homogeneity creates blind spots:

- **Blind spot 1: User experience.** Governance frameworks designed by compliance professionals often create friction that drives shadow IT — users find ways around governance because it wasn't designed with their needs in mind (missing Puppy/Wolf perspective)
- **Blind spot 2: Implementation reality.** Policies that are technically correct but practically unimplementable (missing Rabbit perspective — who ensures resources exist to execute?)
- **Blind spot 3: Strategic alignment.** Governance that satisfies regulators but doesn't advance business strategy (missing Bear perspective — what is governance *for*?)

Campaign Mode's animal archetypes make these blind spots visible before they become compliance failures. The Council can diagnose them proactively; Guardian checkpoints can catch them iteratively; the Dragon can test whether they've been genuinely addressed.

---

## Part 12: Conway's Law and the Agent Architecture Mirror

### 12.1 Conway's Law: Systems Mirror Communication Structures

Conway's Law (1967) states: *"Organizations which design systems are constrained to produce designs which are copies of the communication structures of those organizations."*

MIT and Harvard Business School researchers found *"strong evidence to support the mirroring hypothesis"* — the product developed by a loosely-coupled organisation is significantly more modular than the product from a tightly-coupled organisation. As architect Ruth Malan observed: *"If the architecture of the system and the architecture of the organization are at odds, the architecture of the organization wins."*

### 12.2 Conway's Law for Agent Architectures

The agentic AI field is going through its microservices revolution. Single all-purpose agents are being replaced by orchestrated teams of specialised agents — a researcher agent gathers information, a coder agent implements, an analyst agent validates. This multi-agent pattern mirrors how human teams operate.

**Conway's Law applies directly:** the structure of an enterprise's AI agent fleet will mirror the communication structure of the human teams that designed and govern it.

If the governance team is siloed (security separate from compliance separate from operations), the agent architecture will be siloed too — agents governed by different teams with inconsistent policies, gaps between domains, and no cohesive oversight.

If the governance team is cohesive with diverse perspectives (all six animal functions represented), the agent architecture will reflect that coherence — consistent governance across agent types, integrated oversight, and comprehensive policy coverage.

### 12.3 The Reverse Conway Maneuver for Agent Governance

The Reverse Conway Maneuver (LeRoy & Simons, 2010) deliberately restructures teams to produce the desired system architecture. Instead of letting organisational structure dictate architecture, you design the team structure to match the architecture you want.

**Applied to Agion's customers:** If you want a coherent agent governance architecture, you need a coherent governance team. Campaign Mode's animal archetypes provide the template:

| Desired Architecture Property | Required Team Function | Six-Animal Role |
|------------------------------|----------------------|-----------------|
| Consistent agent mission alignment | Strategic vision | Bear |
| Comprehensive risk coverage | Risk identification across domains | Cat |
| Repeatable governance process | Process management and accountability | Owl |
| Adoption across business units | Change management and morale | Puppy |
| Resource and vendor coordination | Cross-functional facilitation | Rabbit |
| Stakeholder alignment | Team cohesion across silos | Wolf |

**The Campaign Mode Council is a Reverse Conway diagnostic.** By convening all six perspectives before designing the agent architecture, teams ensure their communication structure supports the architecture they want — rather than discovering after deployment that their siloed team produced a siloed agent fleet.

### 12.4 Conway's Law Mitigation at Scale

Agion's customers deploy thousands of agents. At this scale, Conway's Law effects compound:

- **Agent sprawl mirrors organisational sprawl.** Each department deploys its own agents with its own governance approach. No one has the full picture. This is the "No Wolf" failure mode — individuals (departments) working in silos.
- **Governance inconsistency mirrors communication gaps.** Agent policies differ across departments because the governance teams don't coordinate. This is the "No Owl" failure mode — no process accountability.
- **Risk blindness mirrors cultural homogeneity.** Security risks go unidentified because the governance team doesn't include operational perspectives. This is the "No Cat" failure mode — groupthink at the governance level.

Campaign Mode provides three mitigation mechanisms:

1. **Council diagnostic** — reveals which Six-Animal perspectives are missing from the governance team structure before deployment
2. **Guardian checkpoints** — creates natural synchronisation points where Conway's Law drift becomes visible
3. **Dragon confrontation** — adversarially tests whether the deployed architecture reflects the intended governance design, not just the organisational communication structure

### 12.5 Agion's Governance-as-Code as Conway Enforcement

There is an elegant synergy: **Agion's Governance-as-Code is a technical mechanism for resisting Conway's Law drift.**

When governance policies are encoded as automated rules, they cannot silently diverge across departments the way manual governance processes do. The Agion platform enforces architectural consistency regardless of organisational communication patterns.

Campaign Mode complements this by ensuring the **human decision-making** that designs those policies is itself diverse and comprehensive. Agion prevents Conway's Law at the technical layer; Campaign Mode prevents it at the human layer. Together, they address both sides of the mirroring problem.

---

## Part 13: Barriers to Adoption for Agion — and How Campaign Mode / Six Animals Can Help

Beyond the enterprise adoption barriers for Campaign Mode itself (Part 3), there are barriers specific to Agion's market position that Campaign Mode's methodology could help address.

### 13.1 The Trust Paradox

**Barrier:** Agion asks enterprises to trust a governance platform to control their AI agents. But trust in AI governance itself is the unsolved problem. 60% of CISOs express deep concern about AI agent risks, yet only 29% of organisations have comprehensive AI governance plans. The customers who need Agion most are the ones least ready to trust a governance platform.

**How Campaign Mode helps:** The campaign lifecycle builds trust incrementally. You don't ask a customer to deploy platform-wide governance on day one. You structure a campaign: define success criteria (Phase 1), execute a limited pilot (Phase 3), checkpoint results (Phase 4), adversarially test before expanding (Phase 5). Each phase builds trust through demonstrated results, not promised capabilities.

The Guardian's "not yet" decision is particularly valuable: it gives customers permission to go slow without feeling like they're failing. *"Not yet is guidance, not judgment."*

### 13.2 The Governance Complexity Gap

**Barrier:** According to Deloitte's State of AI in the Enterprise report, nearly 60% of AI leaders say their primary challenges are integrating with legacy systems and addressing risk/compliance concerns. Governance frameworks are struggling to keep pace with deployment. Only 15-20% of enterprises deploying experimental agents have moved them to production.

**How Campaign Mode helps:** Campaign Mode's phased approach breaks governance complexity into manageable stages. Rather than attempting comprehensive governance from day one, the Advisor (Gandalf) helps define achievable success criteria for the current phase. Guardian checkpoints prevent teams from attempting too much at once. The "Ship" campaign mode focuses on delivery efficiency — get governance working for a specific use case before expanding.

### 13.3 The Change Management Gap

**Barrier:** AI governance is ultimately a people problem, not a technology problem. Enterprise teams resist governance frameworks because they add friction to workflows. The 3 WEF obstacles — infrastructure constraints, trust deficit, and data gap — are all ultimately about human adaptation, not technical capability.

**How Campaign Mode helps:** This is where the Puppy and Wolf perspectives become critical. Most governance platforms address only the technical/compliance dimensions (Bear, Cat, Owl). Campaign Mode ensures the human dimensions are explicitly covered:

- **Puppy** identifies opportunities to make governance adoption positive rather than punitive
- **Wolf** ensures all stakeholders are aligned and no team feels excluded or imposed upon
- **Rabbit** identifies the resources needed for successful adoption (training, tooling, support)

A governance platform that only speaks to CISOs and compliance officers will fail at the adoption stage. Campaign Mode's diverse perspectives ensure adoption is designed in from the start.

### 13.4 The "Pilot Purgatory" Problem

**Barrier:** Gartner's research shows one of the steepest adoption curves in enterprise history — from under 5% of applications embedding agent capabilities in 2025 to 40% projected in 2026. But most organisations are stuck in "perpetual pilot purgatory" — running experiments that never reach production.

**How Campaign Mode helps:** The Guardian checkpoint and Dragon confrontation directly address this. Pilot purgatory happens because teams lack clear criteria for when a pilot is "done" and ready for production. Campaign Mode requires explicit success criteria upfront (Phase 1) and adversarially tests whether they're met (Phase 5). The Dragon doesn't accept "it mostly works" — it tests whether criteria are genuinely satisfied.

This creates a clear binary: either the pilot meets its defined success criteria (Dragon Slain → promote to production) or it doesn't (Dragon Prevails → iterate with specific feedback). No more ambiguous pilot status.

### 13.5 The Regulatory Compliance Urgency

**Barrier:** EU AI Act compliance requirements take effect August 2026. Organisations must align their AI governance programs with these requirements or face significant penalties. The regulatory timeline is fixed and immovable.

**How Campaign Mode helps:** Campaign Mode's lifecycle maps directly to EU AI Act requirements:

| EU AI Act Requirement | Campaign Mode Mechanism |
|----------------------|------------------------|
| Risk assessment and mitigation | Cat perspective (risk) + Council diagnostic |
| Human oversight mechanisms | Guardian checkpoints + User-as-Protagonist principle |
| Transparency and documentation | Progress log (append-only audit trail) |
| Accuracy and robustness testing | Dragon confrontation (adversarial evaluation) |
| Post-market monitoring | Debrief phase + iterative campaigns |

Structuring EU AI Act compliance as a campaign gives organisations a repeatable methodology for demonstrating compliance readiness — not just a checklist, but a documented lifecycle with quality gates and adversarial testing.

### 13.6 The Differentiation Challenge

**Barrier:** Agion competes with cloud-native governance solutions from Azure, AWS, and Google, as well as emerging governance startups. Their differentiation (LLM-agnostic, cloud-agnostic, data sovereignty, Nordic trust principles) is technical and architectural. They need a methodology differentiation, not just a technical one.

**How Campaign Mode helps:** No competing governance platform offers a psychologically grounded human coordination methodology alongside their technical platform. Agion + Campaign Mode would be unique: technical governance (Governance-as-Code) paired with human governance (structured diverse perspectives, adversarial testing, quality gates, mentorship). This positions Agion as solving the complete problem — both the machine-speed governance and the human decision-making that governs the governors.

---

## Part 14: Campaign Mode as Internal Support Framework for Agion Staff

### 14.1 Mapping Animal Archetypes to Agion Team Functions

Agion's team structure maps naturally to the Six-Animal archetypes:

| Animal | Agion Function | Application |
|--------|---------------|-------------|
| **Bear** | CEO / Product Vision (Janne Pulkkinen) | Platform strategy, mission definition, market positioning |
| **Cat** | Security / Risk / Compliance | Governance policy design, threat modelling, EU AI Act compliance |
| **Owl** | Engineering Process (Marko Taipale) | Sprint management, technical architecture, release process |
| **Puppy** | Customer Success / Developer Relations | Customer adoption, community building, partner enthusiasm |
| **Rabbit** | Partnerships / Business Development | Investor relations, vendor coordination, ecosystem facilitation |
| **Wolf** | Team Culture / Cross-functional Alignment (Mikko Alasaarela as Chair) | Board-team alignment, cross-functional cohesion, stakeholder coordination |

### 14.2 Where Campaign Mode Adds Value Internally

**Product development campaigns.** Each major feature (e.g., "Dynamic Trust Scoring v2") is structured as a campaign with defined success criteria, animal-perspective design reviews, Guardian checkpoints before merge, and Dragon confrontation before release. The Council is convened for architectural decisions.

**Customer implementation support.** Agion staff running 90-day implementations use Campaign Mode to structure their work. The campaign lifecycle ensures consistency across implementations while the animal perspectives ensure nothing is missed (risk assessment for the customer's specific context, resource planning, stakeholder alignment).

**Strategic decision-making.** Convening the Council before major strategic decisions (new market entry, pricing changes, partnership evaluations) ensures all six cognitive perspectives are represented. The synthesis reveals blind spots that a leadership team heavy on Bear (vision) and Cat (risk) might miss.

**Team capability development.** Using Grow mode campaigns for skill development — an engineer learning governance concepts, a salesperson learning technical architecture — builds cross-functional capability. The Dragon confrontation tests whether genuine understanding has been achieved, not just surface familiarity.

### 14.3 Detecting and Addressing Team Gaps

The Six-Animal diagnostic framework reveals team gaps proactively:

- If Agion's team is "All Bear" (too many visionaries, not enough execution), the Council will surface it
- If the "No Puppy" failure mode emerges (technical intensity without morale management), campaigns in Grow mode will make it visible
- If Conway's Law is creating product architecture that mirrors Agion's internal silos, the Council diagnostic will flag it

The Group Failure Diagnosis framework from the Six-Animal Model provides specific, actionable patterns:

| Observed Symptom | Probable Gap | Intervention |
|-----------------|-------------|--------------|
| Features shipped without governance testing | No Cat in dev process | Assign Cat role to design reviews |
| Customer implementations stalling | No Puppy in customer engagement | Add change management perspective |
| Cross-team miscommunication | No Wolf in team structure | Assign Wolf role to standups |
| Resource bottlenecks | No Rabbit in planning | Add facilitation/resource perspective |
| Scope creep on features | No Owl in sprint planning | Add process accountability |

### 14.4 The Dogfooding Flywheel

Internal use creates a virtuous cycle:

1. **Agion uses Campaign Mode internally** → builds intuition for the methodology
2. **Intuition reveals product improvements** → Campaign Mode evolves based on real use
3. **Evolved Campaign Mode is offered to customers** → customers benefit from battle-tested methodology
4. **Customer feedback flows back** → further improvements informed by diverse enterprise contexts
5. **Case study material accumulates** → authentic stories of Campaign Mode in practice at Agion

This flywheel is the strongest argument for starting with Option D (internal dogfooding) before pursuing external-facing options.

---

## Part 15: Revised Strategic Recommendation

The expanded analysis strengthens the original recommendation but adds nuance:

```
Phase 1 (Now):     Option D — Internal dogfooding at Agion
                   + Council diagnostic of Agion's own team structure
                   + Conway's Law assessment of product architecture vs. team structure
                   ↓ learnings

Phase 2 (Near):    Option A — Enterprise skin ("Mission Mode")
                   + Cognitive diversity framing for enterprise positioning
                   + Neurodiversity-aware onboarding language
                   ↓ enables

Phase 3 (Near):    Option B — 90-Day Implementation template
                   + Six-Animal diagnostic as Day 1 Discovery tool
                   + EU AI Act compliance campaign template
                   ↓ validates

Phase 4 (Medium):  Option C — Platform integration
                   + Conway's Law diagnostic for customer team structures
                   + Cognitive diversity metrics in governance dashboards
                   + Hard isolation via Agion platform for Dragon/Guardian
```

### The Core Argument for Agion

Agion solves the **technical** governance problem: how do you enforce policies on thousands of AI agents at machine speed?

Campaign Mode solves the **human** governance problem: how do you ensure the humans designing those policies have diverse cognitive perspectives, structured quality gates, and adversarial testing?

Together, they address both sides of what Conway's Law tells us: **systems mirror the teams that build them.** If you want governed AI agents, you need governed human teams. Agion governs the agents. Campaign Mode governs the governance process.

The differentiator is not "we have better technology" — every governance vendor claims that. The differentiator is: **"We have a psychologically grounded methodology for ensuring the humans who design AI governance are as rigorous as the platform that enforces it."**

That is a story no competitor can tell.

---
---

# DOVIEW PLANNING ANALYSIS

---

## Part 16: DoView Planning — Deep Research

### 16.1 What DoView Planning Is

DoView Planning is a visual strategy methodology developed by Dr Paul Duignan (strategy psychologist, outcomes theorist, Fulbright Senior Scholar). It uses standardised "This-Then" logic diagrams — called DoView strategy/outcomes diagrams — to make the causal structure of any initiative explicit and visible.

The core insight: **every initiative attempting action in the world has an implicit or explicit outcomes system — a set of causal claims about what will happen if certain actions are taken.** DoView Planning makes those claims visible, testable, and shareable.

**Key characteristics:**
- **Open and free** — anyone can use, teach, and build on the methodology with attribution
- **Grounded in outcomes theory** — a unified theoretical framework applicable to any agent (human or AI) taking action in the world
- **Visual-first** — diagrams are the primary artefact, not text documents
- **Tool-agnostic** — works in PowerPoint, Google Slides, or the free legacy DoView app (used in 55+ countries)
- **AI-native** — explicitly designed for human-AI collaboration, with AI DoView Drawing Prompts available
- **Gartner-recognised** — won Gartner's "Cool Vendor" award for enterprise portfolio management

### 16.2 Outcomes Theory: The Theoretical Foundation

DoView Planning rests on **outcomes theory**, which Duignan developed after observing "confused and inconsistent approaches to outcomes issues" across hundreds of organisations globally, including governments and international bodies like the IMF.

**Two foundational propositions:**
1. Any action taken in the world — by humans or AI agents — can be conceptualised as an outcomes system
2. Claims about causal "This-Then" logic underlying outcomes systems are best represented as DoView strategy/outcomes diagrams

**The theory comprises:**
- **Definitions Framework** — Precise differentiation of outcomes, indicators, outputs, inputs, and controllability classifications
- **Outcomes System Concept** — Recognition that every initiative has an implicit or explicit outcomes system underpinning it
- **DoView Planning Framework** — Specifies essential components any outcomes system should include
- **DoView Strategy Diagrams** — Visual representation of causal hierarchies
- **13 Drawing Rules** — Formal protocols ensuring diagrams are fit-for-purpose
- **Typology of Box Elements** — Classification system resolving terminological confusion
- **Evaluation & Economic Design Frameworks** — Assessment and impact tools

**Academic reference:** Duignan, P. (2009) "Using Outcomes Theory to Solve Important Conceptual and Practical Problems in Evaluation, Monitoring and Performance Management Systems"

### 16.3 How DoView Diagrams Work

A DoView diagram maps all steps needed to achieve desired high-level outcomes:

**Structure:**
- **Boxes** represent outcomes and intermediate steps
- **Arrows** show logical "This-Then" connections (causal or temporal)
- **Left-to-right flow** — earlier/more controllable steps on the left, higher-level/less controllable outcomes on the right
- **Overview pages** with drill-down subpages for detail
- **Navigation** between helicopter views and granular details

**Five-step planning process:**
1. **Visualise** — Create DoView diagrams showing outcomes and steps
2. **Prioritise** — Rate boxes (A/B/C/D/E or BAU) for each planning period
3. **Measure** — Attach KPIs and indicators to specific boxes, with "@" notation distinguishing controllable from non-controllable indicators
4. **Evaluate** — Map evaluation questions to specific boxes to reveal coverage gaps
5. **Dashboard** — Traffic-light (colour-code) progress status on each box

**Psychological grounding of the visual format:**
- Left-to-right flow matches how many cultures process sequences, reducing cognitive load
- Continuous flow creates psychological momentum ("going on a journey" metaphor)
- Stable structure helps users build consistent mental models
- Controllability gradient (more controllable left → less controllable right) mirrors natural reasoning

### 16.4 DoViews for AI Systems — The GUI Thesis

Dr Duignan's Substack article argues that the current state of AI system management resembles 1980s text-based computing: developers rely on "prompts, logs, and configuration files" — a text-centric approach that doesn't scale for managing agent swarms.

**The core argument:** Just as graphical user interfaces revolutionised computing, **DoView diagrams should become the visual development and management interface for AI agent systems.** The visual representation itself becomes the development interface, not hidden code-based construction.

**How DoView GUIs function:**
- **Status tracking** — Traffic-light visualisation (yellow for in-progress, green for completed) on each agent task/outcome
- **Interactive feedback** — AI requests human input on specific components shown visually
- **Dynamic iteration** — Diagrams update as the system develops
- **Governance integration** — Humans approve significant decisions (like escalation thresholds) at specific boxes
- **Transparent dependencies** — Visual mapping of prerequisites and relationships

**The Customer Service Agent Swarm example** demonstrates:
- Initial diagram establishing all necessary components
- Prioritised task sequencing
- Real-time status updates with annotations
- Human approval gates for critical decisions
- Addition of new elements with explicit authorisation

**Key differentiator from existing tools:** LangFlow, OpenAI Swarm, CrewAI, and Miro offer visualisation but lack DoView's iterative approach where *"the diagram becomes both the development method and the collaboration interface."*

### 16.5 DoViews Applied to AI Governance

The DoView site provides specific AI governance applications:

**AI Alignment & Constitution Mapping.** Claude's 80-page constitution was converted into a DoView diagram, enabling rapid visual overview of behavioural guidelines. This means anyone can *"produce a DoView outcomes diagram of the constitution or alignment documentation of any AI system"* for auditing actual versus intended conduct.

**The Paperclip Problem visualised.** Two contrasting DoViews show alignment failure: a "Bad Paperclip AI Agent" pursuing unconstrained production versus a "Good Paperclip AI Agent" including resource constraints and human safety. The visual format makes the failure mode instantly comprehensible.

**AI Governance Framework.** An organisational AI governance DoView can be used in meetings to verify *"whether or not they are implementing AI governance and risk management appropriately"* — enabling tailored deployment oversight.

**Agent Swarm Development.** DoViews structure the development of multi-agent systems, mapping outcomes and concrete steps for agent swarm deployment.

**Behavioural Analysis (Strategy X-Ray).** DoView methodology can extract underlying behavioural claims from AI agent outputs, revealing actionable "This-Then" patterns — essentially making implicit agent reasoning explicit and auditable.

**Five-Step AI Management Cycle (Tool J2):**
1. Define intended outcomes and beneficiaries
2. Map intermediate outcomes and AI-influenceable activities
3. Specify constraints, assumptions, risks explicitly
4. Attach indicators and evaluation plans
5. Review and revise diagrams based on observed impacts

---

## Part 17: Structural Parallels — DoView × Campaign Mode × Six Animals × Agion

### 17.1 The Three-Layer Convergence

These three frameworks address different layers of the same fundamental problem: **how do you ensure that complex, multi-agent initiatives (human or AI) achieve their intended outcomes while maintaining quality, accountability, and oversight?**

```
┌─────────────────────────────────────────────────────────────────┐
│  Layer 1: WHAT — Outcomes Architecture (DoView Planning)        │
│  Visual strategy maps showing what we're trying to achieve,     │
│  the causal logic connecting actions to outcomes, and how        │
│  we'll measure success. The blueprint.                          │
├─────────────────────────────────────────────────────────────────┤
│  Layer 2: WHO — Cognitive Coverage (Six Animals)                │
│  Ensuring all necessary human perspectives are represented:     │
│  vision, risk, process, morale, resources, cohesion.            │
│  SDT-grounded team completeness. The team.                      │
├─────────────────────────────────────────────────────────────────┤
│  Layer 3: HOW — Lifecycle Governance (Campaign Mode)            │
│  Structured phases from definition through adversarial testing  │
│  to debrief, with quality gates, mentorship, and context        │
│  isolation. The process.                                        │
├─────────────────────────────────────────────────────────────────┤
│  Foundation: ENFORCEMENT (Agion Platform)                       │
│  Technical governance-as-code enforcing policies at machine     │
│  speed with immutable audit trails. The engine.                 │
└─────────────────────────────────────────────────────────────────┘
```

No single framework covers all four layers. Agion provides the enforcement engine. DoView provides the strategy blueprint. Six Animals provides the team diversity model. Campaign Mode provides the lifecycle process. Together, they constitute a **complete governance stack** for enterprise AI agent deployments.

### 17.2 Specific Structural Parallels

| DoView Concept | Campaign Mode Equivalent | Agion Equivalent |
|---------------|-------------------------|-----------------|
| "This-Then" causal logic | Success criteria (testable conditions) | Mission-as-Code (KPIs as executable missions) |
| Traffic-light status tracking | Progress log (append-only audit trail) | Immutable audit trail |
| Priority ratings (A/B/C/D/E) | Campaign modes (Grow/Ship) prioritise learning vs. delivery | Dynamic Trust tiers (escalating autonomy) |
| Evaluation questions mapped to boxes | Dragon confrontation (adversarial evaluation against criteria) | Policy validation (<10ms) |
| Human approval gates in diagrams | Guardian checkpoints (approve/block/conditional) | Governance-as-Code (automated policy enforcement) |
| Overview + drill-down subpages | Council (overview) + animal perspectives (detail) | Dashboard + agent-level monitoring |
| Drawing Rules (13 formal protocols) | SKILL.md definitions (formal NPC behaviour rules) | AANG Framework (five governance principles) |
| Draft → Review → Update workflow | Quest Definition → Execution → Checkpoint → Confrontation | Discovery → Deployment → Go-live |
| Outcomes theory (any agent taking action) | SDT (any human with motivational needs) | Governance-as-Code (any AI agent executing) |
| Shared thinking tool | Council synthesis | Radical transparency |

### 17.3 Complementary Strengths — Where Each Framework Fills Gaps

**What DoView provides that Campaign Mode lacks:**
- **Visual strategy representation.** Campaign Mode's quest.md is text-based. DoView provides a visual blueprint showing causal relationships between outcomes. A campaign's success criteria would be dramatically more understandable as a DoView diagram than as a markdown list.
- **Outcomes architecture.** DoView's five-step process (Visualise → Prioritise → Measure → Evaluate → Dashboard) provides the structural backbone that Campaign Mode's phases lack. Campaign Mode has quality gates but no visual strategy map.
- **Controllability gradient.** DoView explicitly maps which outcomes are controllable versus influenceable versus beyond control. Campaign Mode doesn't distinguish between criteria the team can directly control and those dependent on external factors.
- **Multi-level detail management.** DoView's overview/subpage architecture handles complexity through layers. Campaign Mode's single quest.md file doesn't scale to complex multi-team initiatives.

**What Campaign Mode provides that DoView lacks:**
- **Adversarial testing.** DoView has evaluation questions but no structurally isolated, adversarial evaluator. The Dragon confrontation fills a critical gap — someone who tests whether the outcomes DoView claims to achieve are genuinely achieved, without access to the team's reasoning.
- **Quality gates with gatekeepers.** DoView has checkpoints but no independent gatekeeper. The Guardian's role — independently evaluating readiness before advancement — is not part of DoView's methodology.
- **Mentorship.** DoView is a planning methodology, not a coaching framework. Gandalf's "guide on the side" mentorship fills the gap between having a plan and being able to execute it.
- **Cognitive diversity.** DoView doesn't prescribe who should be involved in planning. Six Animals' SDT-grounded archetypes ensure all necessary perspectives are represented when creating and evaluating DoView diagrams.
- **Transformation tracking.** DoView tracks outcome achievement. Campaign Mode (in Grow mode) tracks whether the team has genuinely learned, not just delivered — a dimension DoView doesn't address.

**What Six Animals provides that both DoView and Campaign Mode need:**
- **Perspective completeness guarantee.** Neither DoView nor Campaign Mode ensures that the humans using them represent all necessary cognitive perspectives. The Six-Animal Model provides a theoretically complete SDT-grounded coverage model: if all six perspectives are active, no critical dimension is overlooked.
- **Diagnostic capability.** When a DoView is poorly constructed or a campaign is failing, Six Animals can diagnose why: "No Cat perspective led to a DoView that omits risk pathways" or "No Owl perspective led to a campaign without process accountability."

**What Agion provides that the frameworks need:**
- **Machine-speed enforcement.** Frameworks produce plans and governance processes. Agion enforces them at <10ms validation speed across thousands of agents.
- **Hard architectural isolation.** Campaign Mode's instruction-based NPC isolation is soft. Agion's platform could provide the hard architectural boundaries needed for genuinely independent evaluation.
- **Scale.** DoView, Campaign Mode, and Six Animals are designed for human-scale initiatives. Agion operates at enterprise scale with thousands of agents.

### 17.4 The Integration Vision: DoView as the Strategy Layer for Agion's Governance Stack

**Conceptual Architecture:**

```
┌─────────────────────────────────────────────────────────────────────┐
│  DoView Visual Strategy Layer                                       │
│  ┌─────────────────────────────────────────────────────────────┐   │
│  │ Agent Mission DoView — visual blueprint of what the agent    │   │
│  │ swarm should achieve, with causal logic, priority ratings,   │   │
│  │ controllability indicators, and evaluation questions          │   │
│  └──────────────────────────┬──────────────────────────────────┘   │
│                              │ Outcomes, criteria, measures         │
│  ┌──────────────────────────▼──────────────────────────────────┐   │
│  │ Campaign Mode Lifecycle — structured phases:                  │   │
│  │ Define mission (DoView) → Assign perspectives (Six Animals)  │   │
│  │ → Execute → Guardian checkpoint → Dragon confrontation       │   │
│  │ → Debrief                                                    │   │
│  └──────────────────────────┬──────────────────────────────────┘   │
│                              │ Validated outcomes, audit trail      │
│  ┌──────────────────────────▼──────────────────────────────────┐   │
│  │ Agion Platform — Governance-as-Code engine enforcing policies │   │
│  │ at machine speed, with Dynamic Trust and immutable logging    │   │
│  └─────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────────────────────────────────────────┘
```

**How this works in practice:**

1. **Mission Planning.** Customer team creates a DoView diagram for their agent deployment initiative. The Council (all six animal perspectives) reviews the DoView, ensuring it includes risk pathways (Cat), resource dependencies (Rabbit), stakeholder alignment (Wolf), process milestones (Owl), adoption drivers (Puppy), and strategic coherence (Bear).

2. **Success Criteria Extraction.** The Advisor (Gandalf) translates the DoView's highest-level outcome boxes into testable success criteria for the campaign. The DoView's priority ratings map to campaign mode selection (Ship for operational deployment, Grow for capability-building, Grow & Ship for both).

3. **Execution with Visual Tracking.** During campaign execution, the DoView diagram serves as the real-time status dashboard — boxes are traffic-lighted as agent components are deployed. The progress log in quest.md provides narrative context alongside the visual status.

4. **Guardian Checkpoints Against DoView.** The Guardian evaluates readiness by reviewing the DoView's traffic-light status. Are the prerequisite boxes (left side) green before advancing to outcome boxes (right side)? Are measurement indicators attached and reporting?

5. **Dragon Confrontation Against DoView.** The Dragon receives the DoView diagram and the success criteria derived from it. It adversarially tests whether the claimed causal logic actually holds: "You claim THIS leads to THEN — show me the evidence."

6. **Agion Enforcement.** Once the Dragon confirms the governance architecture is sound, Agion's platform enforces the validated policies at machine speed. The DoView becomes the documented governance blueprint; the campaign lifecycle provides the quality assurance process; Agion provides the enforcement engine.

---

## Part 18: DoView × Agion — Specific Opportunities

### 18.1 Opportunity: Agent Mission DoViews as Standard Governance Artefacts

**The problem Agion's customers face:** When deploying thousands of AI agents, each agent's mission, constraints, and expected outcomes exist as configuration files, prompts, and scattered documentation. No standardised visual format makes the governance architecture legible to non-technical stakeholders.

**The DoView solution:** Every agent deployment creates a DoView diagram as a standard governance artefact. The diagram shows:
- What the agent is intended to achieve (outcome boxes, right side)
- What steps the agent takes (activity boxes, left side)
- What constraints apply (constraint boxes)
- What risks are mitigated (risk boxes)
- How success is measured (indicator attachments)
- What human approval gates exist (approval boxes)

**Value for Agion:**
- **Regulatory compliance.** EU AI Act requires documented risk assessment and human oversight. A DoView diagram is a visual compliance artefact showing exactly how governance is structured.
- **Stakeholder communication.** CIOs, compliance officers, and board members can understand agent governance from a DoView in minutes, without reading technical documentation.
- **Audit trail.** The DoView's traffic-light history provides a visual audit record showing when each governance milestone was reached.

### 18.2 Opportunity: DoView as the 90-Day Implementation Blueprint

Agion's 90-day customer implementation maps naturally to a DoView:

| DoView Box (Left → Right) | 90-Day Phase | Campaign Phase |
|---------------------------|-------------|----------------|
| Discovery workshop completed | Day 1 | Quest Definition |
| Agent inventory catalogued | Week 1-2 | Execution |
| Governance policies defined | Week 2-3 | Execution |
| Pilot agents deployed | Week 3-4 | Guardian Checkpoint |
| Trust scoring calibrated | Week 4-5 | Execution |
| Integration testing passed | Week 5-6 | Guardian Checkpoint |
| Production readiness verified | Week 6-7 | Dragon Confrontation |
| Full deployment live | Week 7-8 | Execution |
| Monitoring dashboard active | Week 8-10 | Guardian Checkpoint |
| Customer team self-sufficient | Week 10-12 | Dragon Confrontation / Debrief |

The DoView makes the implementation roadmap visual and trackable. Each box can be traffic-lighted in real time. Priority ratings can shift if customer needs change. Measurement indicators attach to specific boxes to verify progress.

### 18.3 Opportunity: AI Alignment Auditing via DoView

Duignan's work converting Claude's 80-page constitution into a DoView diagram demonstrates a powerful auditing technique. Applied to Agion's context:

- Each AI agent deployed through Agion has a mission definition (Mission-as-Code)
- That mission can be converted into a DoView showing the causal logic: "If the agent does THIS, THEN this outcome results"
- Auditors can compare the DoView (intended behaviour) against the agent's actual behaviour (logged by Agion's immutable audit trail)
- Discrepancies between the DoView and actual behaviour reveal governance gaps

This creates a **visual alignment verification loop**: DoView (intent) → Agion enforcement (execution) → Audit trail (evidence) → DoView comparison (verification).

### 18.4 Opportunity: The "Strategy X-Ray" for Agent Swarm Behaviour

Duignan's "Strategy X-Ray" technique extracts underlying "This-Then" claims from communications. Applied to agent swarms:

- Agion logs all agent actions and decisions
- A Strategy X-Ray automatically generates a DoView diagram showing the *actual* causal patterns in agent behaviour
- Comparing the "intended DoView" (what the agent was designed to do) with the "actual DoView" (what the agent actually did) reveals drift, unexpected behaviours, and emergent patterns
- This is radically more legible than reviewing log files

### 18.5 Opportunity: Shared Thinking Tool for Governance Teams

Duignan's concept of DoViews as "shared thinking tools" that bring *"people's mental models out of their heads"* directly addresses a core Agion challenge: governance teams where different stakeholders have different mental models of what the agent deployment is supposed to achieve.

When combined with Six Animals perspectives:
- **Bear** creates the DoView's high-level vision (rightmost outcome boxes)
- **Cat** adds risk pathways and constraint boxes
- **Owl** structures the timeline and milestones (left-to-right sequence)
- **Puppy** ensures adoption and change management boxes are included
- **Rabbit** maps resource dependencies and external stakeholder connections
- **Wolf** ensures all team functions are represented in the diagram

The result: a DoView that no single perspective could have created alone, with guaranteed cognitive diversity in the planning process.

---

## Part 19: The Convergence Thesis — Why These Frameworks Belong Together

### 19.1 Three Theoretical Traditions, One Problem

| Framework | Theoretical Tradition | Core Question |
|-----------|----------------------|---------------|
| **DoView Planning** | Outcomes theory (Duignan, 2009) | "What are we trying to achieve and what causal logic connects our actions to those outcomes?" |
| **Six Animals** | Self-Determination Theory (Deci & Ryan, 1985) | "Do we have all the human perspectives needed to make this work?" |
| **Campaign Mode** | Constructivist pedagogy + adversarial evaluation | "Are we genuinely ready, and how do we test that rigorously?" |
| **Agion** | Governance-as-Code | "How do we enforce these decisions at machine speed across thousands of agents?" |

These are not competing approaches — they are **orthogonal solutions to different dimensions of the same problem.** An initiative can have a perfect DoView (clear outcomes) but fail because the team lacks cognitive diversity (missing Six Animals). A team can have diverse perspectives but no structured quality gates (missing Campaign Mode). A campaign can have quality gates but no visual strategy map (missing DoView). And all three can be perfect but unenforced at scale (missing Agion).

### 19.2 The Cognitive Load Argument

DoView Planning explicitly addresses cognitive load: *"Left-to-right flow fits with how humans within many cultures process sequences, reducing mental effort required to understand the model."*

Campaign Mode addresses cognitive load through structured phases: you don't have to think about everything at once — quest definition, then execution, then checkpoint, then confrontation, each with clear boundaries.

Six Animals addresses cognitive load through role specialisation: you don't have to think about everything from every perspective — Bear thinks about vision, Cat thinks about risk, each perspective has a defined scope.

Together, they create a **layered cognitive load management system**:
1. **DoView** reduces the load of understanding the strategy (visual > text)
2. **Six Animals** reduces the load of perspective coverage (specialised roles > "everyone think about everything")
3. **Campaign Mode** reduces the load of process management (structured phases > "figure it out as you go")
4. **Agion** reduces the load of enforcement (automated governance > manual oversight)

### 19.3 The Universal Agent Theory Connection

Duignan's outcomes theory makes a striking claim: it is *"a general theory that applies to any agent (human or AI) seeking to take any type of action in the world."*

The Six-Animal Model makes a parallel claim: it maps to the three universal psychological needs (Competence, Relatedness, Agency) that drive all human behaviour.

Campaign Mode's lifecycle reflects universal patterns found in any structured endeavour: define → execute → evaluate → reflect.

Agion's AANG Framework applies universal governance principles: mission definition, policy enforcement, trust calibration, transparency, human-AI partnership.

**The convergence is not coincidental.** All four frameworks are attempting to formalise universal patterns in how agents (human or AI) plan, collaborate, evaluate, and govern complex initiatives. They arrive at the same territory from different theoretical starting points — outcomes theory, motivational psychology, pedagogical theory, and software governance — and find complementary rather than competing solutions.

### 19.4 Revised Positioning for Agion

The three-framework convergence enables a significantly stronger market position for Agion:

**Before (technical differentiation only):**
> "Agion provides governance-as-code for enterprise AI agents — LLM-agnostic, cloud-agnostic, EU AI Act compliant."

**After (methodology + technical differentiation):**
> "Agion provides the complete governance stack for enterprise AI agents:
> - **Visual strategy** (DoView) — see what your agents are trying to achieve and why
> - **Cognitive diversity** (Six Animals) — ensure your governance team covers all perspectives
> - **Structured quality assurance** (Campaign Mode) — test whether your governance is genuinely ready
> - **Machine-speed enforcement** (Agion Platform) — enforce validated policies across thousands of agents
>
> No other vendor offers a psychologically grounded, theoretically unified methodology alongside their governance platform."

---

## Part 20: Revised Strategic Recommendation (Final)

The addition of DoView Planning to the analysis adds a new dimension to the phased approach:

```
Phase 1 (Now):     Option D — Internal dogfooding at Agion
                   + Create DoView diagram of Agion's own product strategy
                   + Council diagnostic of Agion's team structure
                   + Conway's Law assessment via DoView comparison
                   ↓ learnings

Phase 2 (Near):    Option A — Enterprise skin ("Mission Mode")
                   + DoView template for "Agent Mission Blueprint"
                   + Six-Animal diagnostic as discovery tool
                   + Neurodiversity-aware onboarding language
                   ↓ enables

Phase 3 (Near):    Option B — 90-Day Implementation template
                   + DoView as the visual implementation roadmap
                   + Campaign lifecycle for quality assurance
                   + EU AI Act compliance campaign template
                   ↓ validates

Phase 4 (Medium):  Option C — Full platform integration
                   + DoView as the visual governance interface
                   + Campaign Mode lifecycle for human-side QA
                   + Six Animals for cognitive diversity metrics
                   + Agion platform for machine-speed enforcement
                   + Strategy X-Ray for agent behaviour auditing
```

### The Final Thesis

Agion's market thesis is *"AI without control is as useless as no AI at all."*

The expanded thesis becomes: **"AI without *visible, diverse, tested* control is as useless as no AI at all."**

- **Visible** — DoView makes governance legible (visual strategy diagrams, not buried configuration)
- **Diverse** — Six Animals ensures governance teams represent all necessary perspectives (SDT-complete coverage)
- **Tested** — Campaign Mode provides adversarial quality assurance (Dragon confrontation, Guardian checkpoints)
- **Enforced** — Agion Platform executes validated governance at machine speed

Four layers. Four theoretical traditions. One complete governance stack.

That is a product story that scales from a CIO's board presentation to a developer's command line — and no competitor has anything like it.

---
---

# SOURCES & CITATIONS

---

## DoView Planning — Primary Sources

### Website
- **DoView Planning** — https://www.doviewplanning.org/ — Official site for DoView Planning methodology, examples, handbook, free app, and AI integration resources. All DoView website citations below are subpages of this domain.

### Subpages Consulted
- **DoView Planning Method** — https://www.doviewplanning.org/method — Five-step DoView Planning process (Visualise, Prioritise, Measure, Evaluate, Dashboard), drawing rules, and methodology overview.
- **DoView Planning Theory** — https://www.doviewplanning.org/theory — Outcomes theory foundation, two foundational propositions, seven theoretical components, psychological grounding (cognitive load, psychological momentum, controllability gradient), and human-AI collaboration principles.
- **AI Systems Management** — https://www.doviewplanning.org/aiuse — Application of DoView Planning to AI agent governance, alignment, transparency, and the DoView Planning Handbook Part J (tools J1-J7 for AI applications).
- **AI System DoViews** — https://www.doviewplanning.org/aisystemdoviews — Specific DoView examples for AI: Paperclip Problem DoViews (good/bad alignment), Claude Constitution DoView [/a057], AI Governance and Risk Management DoView [/a064], AI Agent Swarm Development DoView [/a031], Moltbook Strategy X-Ray [/a065].
- **DoView Planning Uses** — https://www.doviewplanning.org/uses — Three primary application domains: Government, Research, AI Systems Management.
- **Government Use** — https://www.doviewplanning.org/governmentuse — Ten-step government planning/implementation/reporting cycle; budget optimisation example ($80M reduced to $14M via DoView Visual Alignment).
- **AI DoView Drawing Prompt** — https://www.doviewplanning.org/prompt — Three-stage AI prompt system for generating DoView diagrams: structure definition, detailed content, Python/PowerPoint code generation. Drawing rules, quality controls, and user-AI collaboration checkpoints.
- **Collaborate** — https://www.doviewplanning.org/collaborate — Open collaboration model: free adoption with attribution, open invitation to joint ventures, permissive intellectual property approach.
- **DoView Planning Handbook** — https://www.doviewplanning.org/book — *DoView Planning and Outcomes Theory Handbook: 100+ Innovative, Integrated Tools for Solving Key Issues in Planning, Implementation, Contracting, Measurement, Evaluation and Reporting (for Humans and AI Agents)* by Dr Paul Duignan (2025). 100+ tools across 10 parts (A-J).
- **Free App** — https://www.doviewplanning.org/app — Legacy DoView app (Windows, free, formerly paid), Gartner Cool Vendor Award recipient. XML-saveable, mergeable files, drill-down subpages.

### DoView Examples Consulted
- **Large Company DoViews** — https://www.doviewplanning.org/largecompanydoviews — Illustrative strategy diagrams for Amazon [/a060], Anthropic [/a034], Apple [/a036], Google [/a037], JPMorgan Chase, KPMG US [/a053], Microsoft [/a032], Nike [/a039], OpenAI [/a033], Tesla. (Not endorsed by these companies; created from public information.)
- **Generic DoViews** — https://www.doviewplanning.org/genericdoviews — Templates for Company, Early Childhood Centre, Gym/Fitness Centre, Law Firm, Police District, Restaurant/Cafe, School.
- **NZ Government DoViews** — https://www.doviewplanning.org/nzgovernmentdoviews — New Zealand government illustrative examples (not endorsed by NZ government).
- **NZ Company DoViews** — https://www.doviewplanning.org/nzcompanydoviews
- **EU DoViews** — https://www.doviewplanning.org/eudoviews
- **UK Government DoViews** — https://www.doviewplanning.org/ukgovernmentdoviews
- **International Collaboration DoViews** — https://www.doviewplanning.org/internationalcollaborationdoviews — U.S., China, and E.U. collaboration on reducing risk of Artificial General Intelligence DoView.
- **World Economic Forum DoViews** — https://www.doviewplanning.org/worldeconomicforumdoviews — Three DoViews derived from WEF Global Risk Report 2026: Governments Response [/a054], Corporates Response [/a055], Civil Society Response [/a056].
- **Research Domain DoViews** — https://www.doviewplanning.org/researchdomaindoviews — Space-Based Infrastructure [/a030], Climate Tipping Points [/a031].

### Substack Article
- Duignan, P. (2025). "DoViews as GUIs for Building and Running AI Agent Systems." *Dr Paul Duignan's Substack.* https://drpaulduignan.substack.com/p/doviews-as-guis-for-building-and — Core argument: DoView diagrams should serve as visual development/management interfaces for AI agent systems, replacing text-based prompts/logs/configs. Customer Service Agent Swarm mock-up. Comparison to 1980s text-based computing. Differentiation from LangFlow, OpenAI Swarm, CrewAI, Miro.

### Academic Publication
- Duignan, P. (2009). "Using Outcomes Theory to Solve Important Conceptual and Practical Problems in Evaluation, Monitoring and Performance Management Systems." — Seminal paper describing outcomes theory in comprehensive detail. Referenced throughout the DoView Planning methodology as the theoretical foundation.

### Author Background
- **Dr Paul Duignan** — Strategy psychologist and outcomes theorist. Doctoral studies in strategic evaluation. University research group management. National Parliament research unit directorship. Fulbright Senior Scholar at the Urban Institute, Washington D.C. Consulting across hundreds of organisations globally, including governments and international bodies (IMF).

---

## Agion — Primary Sources

- **Agion Website** — https://agion.ai/ — "The Agentic OS for the Sovereign Enterprise." Governance-as-Code platform for enterprise AI agent deployments.
- **AANG Framework** — Agion's five governance principles: Mission-as-Code, Dynamic Trust, Governance-as-Code, Radical Transparency, Human-AI Partnership. (Referenced from Agion website and product documentation.)

---

## McCallum's Six-Animal Model — Primary Sources

### Website
- **The Six-Animal Model** — http://103.224.130.189/ (in development) — Official website for McCallum's Six-Animal Model. "A practical toolkit for better teamwork." Includes animal role descriptions, interactive quiz, theoretical foundations, group failure diagnosis, digital/AI tools, and consultation booking.

### Subpages Consulted
- **Home** — http://103.224.130.189/ — Model overview, key insights ("Tools, Not Labels", "Behaviours You Can Learn", "Make Space for Others", "Every Style Has Value"), SDT grounding summary, group failure preview, introductory video.
- **The Animals** — http://103.224.130.189/animals — Individual animal role pages: Bear (Visionary/Leader), Wolf (Manager), Cat (Risk Manager/Cynic), Puppy (Enthusiast), Owl (Process Master), Rabbit (Facilitator). Each with individual detail pages at `/animals/bear`, `/animals/wolf`, `/animals/cat`, `/animals/puppy`, `/animals/owl`, `/animals/rabbit`.
- **Find Your Role (Quiz)** — http://103.224.130.189/quiz — Interactive quiz for identifying primary and secondary animal roles.
- **Theory** — http://103.224.130.189/theory — Theoretical foundations: SDT mapping (primary/secondary needs per animal), animal pairs by primary need, why SDT was chosen, related work section. Full academic references list (see below).
- **Group Diagnosis** — http://103.224.130.189/group-failures — Diagnostic tool: "Which function is missing?" Predictable failure patterns when each role is absent (No Bear = no direction; No Wolf = silos; No Cat = unidentified risks; No Puppy = morale drops; No Owl = no process; No Rabbit = no facilitation).
- **Digital/AI** — http://103.224.130.189/digital — AI implementations: ChatGPT Six-Animal Model GPT (Avatar Mode, Groupwork Mode, Review Mode); Claude Six Animal Agent Skills (six specialised SKILL.md definitions for Anthropic's Claude). Campaign Mode listed as complementary quest-based extension.
- **About** — http://103.224.130.189/about — Model origins (observation of hundreds of student project teams and professional groups), where the model is used (VUW Executive MBA, CS User Experience SWEN303, Game Development IMT3603, professional workshops), key influences (Nordic management culture, neurodiversity awareness, gamification, psychological safety), Dr McCallum biography.
- **Book** — http://103.224.130.189/book — Forthcoming book: *The Six-Animal Model: A Practical Guide to Understanding and Managing Group Dynamics* by Dr Simon McCallum. Four parts: Foundations, The Animals, Application, Appendices.
- **Consultation** — http://103.224.130.189/contact — Professional consultation and workshop booking.

### Author Background
- **Dr Simon McCallum** — Academic and practitioner spanning computer science, game development, education, and organisational psychology. Positions at Victoria University of Wellington (New Zealand) and Norwegian University of Science and Technology (NTNU). Teaches software engineering, game development, and user experience design. Research interests: group dynamics, gamification of learning, neurodiversity in education, application of psychological frameworks to practical team management.

### SDT Mapping (from Theory page)

| Animal | Role | Primary Need | Secondary Need |
|--------|------|-------------|----------------|
| Bear | Visionary / Leader | Competence | Agency |
| Wolf | Manager | Relatedness | Agency |
| Cat | Risk Manager / Cynic | Agency | Competence |
| Puppy | Enthusiast | Relatedness | Competence |
| Owl | Process Master | Agency | Relatedness |
| Rabbit | Facilitator | Competence | Relatedness |

### Academic References (from Theory page)
- McClelland, D.C. (1961). *The Achieving Society.* Van Nostrand. — Original Theory of Needs (Achievement, Affiliation, Power) that informed the model's initial development.
- McClelland, D.C. (1987). *Human Motivation.* Cambridge University Press.
- Deci, E.L. & Ryan, R.M. (1985). *Intrinsic Motivation and Self-Determination in Human Behavior.* Plenum Press. — Foundational SDT text establishing the three basic psychological needs: Competence, Relatedness, Autonomy.
- Ryan, R.M. & Deci, E.L. (2000). "Self-determination theory and the facilitation of intrinsic motivation, social development, and well-being." *American Psychologist, 55*(1), 68-78. — Extended SDT framework; the model shifted from McClelland to SDT for "a richer theoretical foundation" aligned with "contemporary motivational research."
- Belbin, R.M. (2010). *Team Roles at Work* (2nd ed.). Butterworth-Heinemann. — Related work on team role theory.
- Tuckman, B.W. (1965). "Developmental sequence in small groups." *Psychological Bulletin, 63*(6), 384-399. — Group development stages model.
- Edmondson, A. (1999). "Psychological safety and learning behavior in work teams." *Administrative Science Quarterly, 44*(2), 350-383. — Psychological safety research that influenced the animal metaphor design (safe way to discuss role failures without triggering defensiveness).

---

## Campaign Mode — Primary Sources

### Repository
- **Campaign Mode** — https://github.com/cgbarlow/campaign-mode — Quest-based extension for the Six Animals team collaboration framework. CC-BY-SA-4.0 license.

### Key Source Files
- **CLAUDE.md** — `/home/user/campaign-mode/CLAUDE.md` — Cross-cutting conventions: agent identity, core archetype constraints (core vs. flex behaviours), context isolation levels (Advisory/Independent/Maximum), six-phase campaign lifecycle, campaign progress tracking, mode selection (Grow/Ship/Grow & Ship), profile rules, file conventions, debrief protocol, user-as-protagonist principle.
- **Gandalf Agent SKILL.md** — `/home/user/campaign-mode/skills/gandalf-agent/SKILL.md` — Mentor NPC: quest framing, campaign mode selection, success criteria definition, quest state persistence, character profile facilitation, guide-on-the-side philosophy. Author: Chris Barlow. License: CC-BY-SA-4.0.
- **Dragon Agent SKILL.md** — `/home/user/campaign-mode/skills/dragon-agent/SKILL.md` — Adversary NPC: success criteria evaluation, adversarial stress testing, independent judgement, maximum context isolation, Dragon Slain/Dragon Prevails verdict. Author: Chris Barlow. License: CC-BY-SA-4.0.
- **Guardian Agent SKILL.md** — `/home/user/campaign-mode/skills/guardian-agent/SKILL.md` — Gatekeeper NPC: checkpoint evaluation, quality gate function (Approve/Block/Conditional), readiness assessment, Zone of Proximal Development assessment, confidence-weighted verification. Author: Chris Barlow. License: CC-BY-SA-4.0.

### Architecture Decision Records (ADRs)
- `/home/user/campaign-mode/docs/2_adrs/` — 15 ADRs (ADR-CM-001 through ADR-CM-015) documenting design decisions in WH(Y) format. Key ADRs: Campaign Mode Architecture (001), Quest Agent Decomposition (002), NPC Context Isolation (003), Campaign Mode Selection grounded in SDT (005), Council Feature (011), Animal Campaign Extensions (014).

### Design Specifications (SPECs)
- `/home/user/campaign-mode/docs/3_specs/` — 14 specifications covering skill architecture, campaign lifecycle, individual NPC agents, context isolation protocol, campaign state directory, plugin structure, and animal campaign extensions.

### Vision Document
- **north-star.md** — `/home/user/campaign-mode/docs/north-star.md` — Campaign Mode vision, problem statement, architecture (Party + NPCs + Supervisor layers), design principles, implementation strategy.

### Authors
- **Chris Barlow** — Campaign Mode design and implementation (all NPC agents, commands, ADRs, specifications, documentation)
- **Dr Simon McCallum** — Six Animals framework, pedagogical foundation, Simon agent design

---

## Conway's Law — Sources

- Conway, M.E. (1968). "How Do Committees Invent?" *Datamation, 14*(4), 28-31. — Original statement of Conway's Law: "Organizations which design systems are constrained to produce designs which are copies of the communication structures of those organizations." (First circulated 1967, published 1968.)
- LeRoy, J. & Simons, M. (2010). *Reverse Conway Maneuver.* — Concept of deliberately restructuring teams to produce desired system architecture, rather than letting organisational structure dictate architecture. (Referenced in Part 12.)

---

## Other Sources Referenced

- **Harvard Business Review (HBR)** — Referenced in Part 8 for research showing cognitively diverse teams solve problems up to three times faster than homogeneous teams.
- **Gartner** — DoView app received Gartner "Cool Vendor" Award for enterprise portfolio management. Referenced for Agentic AI adoption projections (under 5% of applications embedding agent capabilities in 2025, projected 40% in 2026).
- **EU AI Act** — European Union's regulatory framework for AI systems, requiring documented risk assessment and human oversight. Referenced as compliance driver for DoView-based governance artefacts.
- **Microsoft** — Referenced for recommending outcomes-focused (rather than siloed functional) organisational planning, aligning with outcomes theory principles. (Cited on DoView Planning theory page.)
- **World Economic Forum** — WEF Global Risk Report 2026 used as source for three illustrative DoViews (Government, Corporate, Civil Society risk responses).
- **YouTube** — Six-Animal Model introductory video embedded on the Six-Animal Model website home page: https://www.youtube-nocookie.com/embed/WnVVkcqnIGw
