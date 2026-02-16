# ADR-CM-017: Proactive Party Engagement

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-017 |
| **Type** | Standard ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-16 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Phase 3 (Campaign Execution) being the longest and most unstructured phase, where animals currently act as passive tools only speaking when explicitly invoked,

**facing** the gap that after Gandalf transitions to Phase 3 the user receives generic options ("Begin working" / "Review quest summary" / "Consult an animal advisor") with no guidance on who to consult or when, leaving the advisory council feeling like passive tools rather than an active team,

**we decided for** four proactive engagement mechanisms — a recommended first advisor at Phase 3 entry, Next Perspective handoffs after every animal consultation, proactive trigger detection per archetype, and Party Assignments mapping success criteria to animal advisors in quest.md — all facilitated through `AskUserQuestion`,

**and neglected** autonomous self-invocation (infeasible within the Skill tool architecture — agents cannot invoke other agents without user action), fixed rotation schedules (ignores conversation context and quest characteristics), and narrative-only suggestions without `AskUserQuestion` (too easy to ignore and breaks the established elicitation convention from ADR-CM-008),

**to achieve** an active advisory council that guides the user through Phase 3 with context-aware perspective suggestions, smooth handoffs between animal consultations, and clear mapping of which advisors are most relevant to each success criterion,

**accepting that** the animal campaign extension grows from ~40 to ~100-120 lines per command invocation, animals must adapt suggestions to conversation content rather than following rigid scripts, and Party Assignments are written by Gandalf during Phase 1 which adds a step to quest definition.

---

## Context

Phase 3 (Campaign Execution) is the "doing" phase — the user works through their quest, invoking animal agents for their archetype strengths. Currently, this phase has two structural weaknesses:

1. **No entry guidance** — When Gandalf finishes Phase 2 and transitions to Phase 3, the user gets generic options with no recommendation on which animal to consult first or why
2. **No mid-phase continuity** — After consulting an animal, the conversation ends. The user must decide on their own who to talk to next, with no suggestion from the animal they just spoke with

ADR-CM-008 (Proactive Elicitation) established that agents must use `AskUserQuestion` at phase transitions. ADR-CM-014 (Animal Campaign Extensions) gave animals campaign awareness via the extension file. This decision extends both — bringing proactive elicitation into the mid-phase experience and giving animals the ability to recommend next perspectives.

## Options Considered

### Option 1: AskUserQuestion-Based Handoffs with Criterion Mapping (Selected)

Four mechanisms working together:
- **Recommended first advisor** — Gandalf analyses quest characteristics and recommends which animal to consult first
- **Next Perspective protocol** — Every animal ends Phase 3 consultations with `AskUserQuestion` suggesting the next advisor
- **Proactive trigger detection** — Animals detect when another archetype's perspective is needed based on conversation content
- **Party Assignments** — quest.md maps each success criterion to primary and secondary animal advisors

**Pros:**
- Consistent with established `AskUserQuestion` convention (ADR-CM-008)
- Context-aware — suggestions adapt to conversation content, not rigid scripts
- User retains full agency — every suggestion is a choice, not an action
- Criterion mapping creates a natural structure for Phase 3 progression

**Cons:**
- Extension file grows significantly (~40 → ~100-120 lines)
- Animals must exercise judgement in adapting suggestions
- Adds complexity to Gandalf's Phase 1 flow (Party Assignments)

### Option 2: Autonomous Self-Invocation (Rejected)

Animals automatically invoke the next relevant animal when they detect a need.

**Why rejected:** Infeasible within the Skill tool architecture — agents cannot invoke other agents without user action. Also violates the User as Protagonist principle (ADR-CM-008).

### Option 3: Fixed Rotation Schedule (Rejected)

Animals follow a predetermined consultation order (e.g., Bear → Cat → Owl → Puppy → Rabbit → Wolf).

**Why rejected:** Ignores conversation context and quest characteristics. A quest focused on risk management doesn't need the same consultation order as one focused on team alignment. Fixed rotation creates busywork rather than value.

### Option 4: Narrative-Only Suggestions (Rejected)

Animals mention other perspectives in their response text without using `AskUserQuestion`.

**Why rejected:** Too easy for the user to ignore or miss. Breaks the established convention that next-step options use `AskUserQuestion` (ADR-CM-008). Inconsistent with the proactive elicitation pattern used everywhere else in Campaign Mode.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-010-A](../3_specs/SPEC-CM-010-A-Phase-3-Party-Engagement.md) | Phase 3 Party Engagement | Recommended first advisor, Next Perspective protocol, proactive triggers, Party Assignments format, context window impact |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-008 | Proactive Elicitation | Extends mid-phase `AskUserQuestion` handoffs into Phase 3 |
| Extends | ADR-CM-014 | Animal Campaign Extensions | Adds new extension content for mid-phase engagement |
| Relates To | ADR-CM-010 | Quest State Tracking | Party Assignments added to quest.md |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Gandalf's Phase 1 role expanded with Party Assignments |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Animal Campaign Extensions | Extension File | [extensions/animal-campaign-context.md](../../extensions/animal-campaign-context.md) |
| REF-002 | Campaign Lifecycle Spec | Internal Spec | [SPEC-CM-001-B](../3_specs/SPEC-CM-001-B-Campaign-Lifecycle.md) |
| REF-003 | Gandalf Agent Skill | Internal Skill | [skills/gandalf-agent/SKILL.md](../../skills/gandalf-agent/SKILL.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-16 |
| Accepted | Chris Barlow | 2026-02-16 |
