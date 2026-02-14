# ADR-CM-005: Campaign Mode Selection

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-005 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode's quest lifecycle and the range of users who may adopt it,

**facing** the reality that users approach campaigns with fundamentally different priorities -- some want personal growth and self-discovery, some want to ship work efficiently, and some want both -- and that the current design implicitly assumes a balanced orientation with no way for the user to express their intent,

**we decided for** three named campaign modes (Grow, Ship, Grow & Ship) selected by the user during Phase 1 (Quest Definition), with each mode tuning all NPC agent behaviour through mode-aware context,

**and neglected** a single fixed mode (forces all users into one framing), per-interaction mode switching (inconsistency mid-campaign), and a continuous slider (too abstract),

**to achieve** user agency over their campaign experience, appropriate NPC behaviour calibration, and alignment with SDT's autonomy principle,

**accepting that** all three modes must be maintained in every NPC skill (increasing complexity), and that the mode distinction adds a decision point at campaign start.

---

## Context

Campaign Mode currently treats all campaigns identically -- an implicit assumption that every user wants the same balance of learning and productivity. In practice, users approach campaigns with fundamentally different priorities:

1. **Learning-oriented users** want self-discovery, reflection, and personal transformation. The journey matters more than the destination. They want Gandalf to ask deep questions, the Guardian to assess understanding, and the Dragon to test growth.

2. **Productivity-oriented users** want to ship work efficiently. Campaign Mode's structured approach and diverse NPC perspectives help them cover blind spots and produce better deliverables. They want efficiency, not reflection.

3. **Balanced users** want both -- growth through doing real work. They want the full campaign experience without artificial separation of learning from delivery.

This aligns with Self Determination Theory's autonomy principle: users should have agency over their own experience. Forcing a single orientation undermines the autonomy that makes Campaign Mode effective.

### The User as Protagonist

This decision also addresses a gap in Campaign Mode's framing: the documentation describes 10 AI agents but never explains what the human does. The user is the **protagonist** -- the decision-maker who drives the quest, invokes agents, produces work, and faces NPCs. Mode selection is the first expression of this agency: the user chooses how they want to approach their campaign before the campaign begins.

## Options Considered

### Option 1: Three Named Modes -- Grow, Ship, Grow & Ship (Selected)

Three distinct modes selected at campaign start, each tuning NPC behaviour through mode-aware context passed to all agents.

**Pros:**
- Clear, memorable labels that users can immediately understand
- Covers the full spectrum of user intent
- Default (Grow & Ship) preserves current behaviour for users who don't choose
- Mode is set once and persists, providing consistent framing throughout
- Aligns with SDT autonomy -- the user chooses their experience

**Cons:**
- Three modes must be maintained in every NPC skill file
- Adds a decision point at campaign start (minor friction)
- Users might choose "wrong" and feel locked in (mitigated by default being balanced)

### Option 2: Single Fixed Mode (Rejected)

All campaigns use the same orientation (implicitly Grow & Ship).

**Why rejected:** Forces all users into one framing. Productivity-oriented users find the reflection unnecessary; learning-oriented users find the deliverable focus distracting. Undermines user agency.

### Option 3: Per-Interaction Mode Switching (Rejected)

Allow users to change mode at any point during the campaign.

**Why rejected:** Inconsistency mid-campaign would make NPC behaviour unpredictable. Success criteria defined under one mode would be evaluated under another. The Guardian and Dragon need stable expectations to evaluate against.

### Option 4: Continuous Slider (Rejected)

A spectrum from "pure learning" to "pure shipping" with infinite granularity.

**Why rejected:** Too abstract. Users cannot meaningfully distinguish between 60% learning and 70% learning. NPC behaviour cannot be meaningfully calibrated to arbitrary positions on a continuum. Three named modes are simpler to understand and implement.

---

## Mode Definitions

### Grow (Learning Experience)

| Aspect | Detail |
|--------|--------|
| **Priority** | Self-discovery, reflection, role exploration, transformation |
| **Framing** | "What will you learn? Who will you become?" |
| **Philosophy** | The journey matters more than the destination |
| **Phase 2** | Encouraged -- character setup adds reflective depth |
| **Phase 6** | Full pedagogical reflection and debrief |

### Ship (Productivity)

| Aspect | Detail |
|--------|--------|
| **Priority** | Deliverables, efficiency, covering blind spots |
| **Framing** | "What will you deliver? What does done look like?" |
| **Philosophy** | The campaign framing is a means to getting work done |
| **Phase 2** | Skipped -- character setup is not productivity-relevant |
| **Phase 6** | Brief retrospective focused on process improvement |

### Grow & Ship (Balanced -- Default)

| Aspect | Detail |
|--------|--------|
| **Priority** | Both learning and delivery |
| **Framing** | "What will you learn AND deliver?" |
| **Philosophy** | Growth happens through doing real work |
| **Phase 2** | Optional -- user chooses |
| **Phase 6** | Balanced debrief covering both growth and deliverables |

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-005-A](../specs/SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | Mode-agent interaction matrix defining how each mode tunes NPC behaviour |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Modes tune the behaviour of the three NPCs |
| Relates To | ADR-CM-003 | NPC Context Isolation | Campaign mode is added to NPC context |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Self Determination Theory | Theoretical Foundation | Ryan & Deci (2000) -- Autonomy, Competence, Relatedness |
| REF-002 | Six Animals Framework | External Project | [github.com/SimonMcCallum/six-animals](https://github.com/SimonMcCallum/six-animals) |
| REF-003 | Campaign Mode North Star | Vision Document | [docs/north-star.md](../north-star.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
| Accepted | Chris Barlow | 2026-02-14 |
