# ADR-CM-002: Quest Agent Decomposition

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-002 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Proposed |

---

## WH(Y) Decision Statement

**In the context of** reimagining quest-council's quest-agent for campaign-mode,

**facing** the problem that a single 674-line skill conflates mentorship, adversarial testing, gatekeeping, quest design expertise, and platform architecture concerns into one monolithic agent,

**we decided for** decomposing into three focused NPC agents — Gandalf (Mentor), Dragon (Adversary), Guardian (Gatekeeper) — each with a single responsibility,

**and neglected** retaining the monolithic quest-agent and a two-agent split (mentor + adversary),

**to achieve** clear role boundaries, independent invocation, and alignment with the north-star's 3-NPC model,

**accepting that** some quest-agent content (platform architecture, NPC technical implementation, quest examples) is deferred to post-v1.

---

## Context

The quest-council project contains a monolithic `quest-agent` skill (674 lines) that combines:
- Quest Definition Framework and philosophy ("quests not goals")
- The Dragon concept and metaphor
- Progressive complexity, gating, and quality verification
- Technical architecture (NPC systems)
- 12 quest examples across multiple categories
- Design principles and implementation methodology

Additionally, the `simon-agent` provides pedagogical foundations that inform NPC behaviour:
- "Guide on the side" philosophy → Gandalf's mentorship approach
- Dragon as learning edge → Dragon's pedagogical foundation
- Zone of Proximal Development → Guardian's readiness assessment
- Confidence-weighted verification → Guardian's quality evaluation

Combining all these concerns into a single agent creates problems:
1. **Role confusion** — Users don't know whether they're getting mentorship, adversarial testing, or gatekeeping
2. **No independent invocation** — Can't summon just the adversary or just the mentor
3. **Context leakage** — A single agent can't maintain context isolation between mentor and adversary functions
4. **Maintenance burden** — 674 lines of interleaved concerns are hard to evolve

## Options Considered

### Option 1: Three-NPC Decomposition (Selected)

Decompose into Gandalf (Mentor), Dragon (Adversary), and Guardian (Gatekeeper), each as a standalone Claude Code skill.

**Pros:**
- Single responsibility per agent
- Independent invocation
- Enables context isolation (critical for Dragon and Guardian objectivity)
- Aligns with north-star vision
- Each agent is ~150-250 lines (manageable, focused)

**Cons:**
- Some content must be distributed across agents
- Platform architecture content deferred
- Users must learn three agents instead of one

### Option 2: Retain Monolithic Quest-Agent (Rejected)

Keep the quest-agent as-is and add it to campaign-mode.

**Why rejected:** Perpetuates the conflation problem. Cannot support context isolation. Does not align with the north-star's 3-NPC architecture.

### Option 3: Two-Agent Split — Mentor + Adversary (Rejected)

Split into a Mentor (combining mentorship and gatekeeping) and an Adversary.

**Why rejected:** Conflates mentorship with gatekeeping. The Guardian's gatekeeper function is distinct from Gandalf's mentor function — a mentor guides and encourages, while a gatekeeper evaluates and blocks. Combining them weakens both.

---

## Content Distribution

### From quest-agent:

| Content | Destination | Rationale |
|---------|-------------|-----------|
| Quest Definition Framework | Gandalf | Mentor frames the quest |
| Core Philosophy: Quests Not Goals | Gandalf | Mentor sets the mindset |
| Implementation Methodology (Steps 1-4) | Gandalf | Mentor designs quest structure |
| The Dragon Concept / Dragon Metaphor | Dragon | Adversary embodies the challenge |
| Success Criteria evaluation | Dragon | Adversary tests completion |
| Progressive Complexity / Gating | Guardian | Gatekeeper controls progression |
| Verification & Quality Assurance | Guardian | Gatekeeper evaluates quality |
| NPC Agent System (technical) | Deferred | Platform architecture, not skill content |
| 12 Quest Examples | Deferred | Reference material |
| Quest Design Template | Gandalf (reference) | Mentor uses this to structure quests |

### From simon-agent:

| Content | Destination | Rationale |
|---------|-------------|-----------|
| Guide on the Side philosophy | Gandalf | Mentor mentors, doesn't rescue |
| Behind the Curtain transparency | Stays with Simon | Meta-pedagogy is Simon's role |
| Dragon as Learning Edge | Dragon | Pedagogical foundation for Dragon |
| Confidence-Weighted Verification | Guardian | Quality assessment method |
| Zone of Proximal Development | Guardian | Readiness assessment framework |
| Cultural Responsiveness | All NPCs (lightly) | Embedded as design principle |

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-002-A](../specs/SPEC-CM-002-A-Gandalf-Agent.md) | Gandalf Agent Specification | Full skill design for the Mentor NPC |
| [SPEC-CM-002-B](../specs/SPEC-CM-002-B-Dragon-Agent.md) | Dragon Agent Specification | Full skill design for the Adversary NPC |
| [SPEC-CM-002-C](../specs/SPEC-CM-002-C-Guardian-Agent.md) | Guardian Agent Specification | Full skill design for the Gatekeeper NPC |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Relates To | ADR-CM-003 | NPC Context Isolation | Dragon and Guardian require context isolation |
| Relates To | ADR-CM-004 | Skill-Based Implementation | Delivery mechanism for the three NPCs |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Quest Agent SKILL.md | Source Material | quest-council/skills/quest-agent/SKILL.md |
| REF-002 | Simon Agent SKILL.md | Source Material | quest-council/skills/simon-agent/SKILL.md |
| REF-003 | North Star | Vision Document | docs/north-star.md |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| — | — | — | — | Quarterly | — |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
