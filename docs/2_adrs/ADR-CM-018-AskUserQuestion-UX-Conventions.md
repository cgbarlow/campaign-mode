# ADR-CM-018: AskUserQuestion UX Conventions

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-018 |
| **Type** | Standard ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-17 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Claude Desktop rendering `AskUserQuestion` immediately and stealing scroll focus before the user has read the agent's preceding text — a known Claude Desktop limitation with no client-side fix available,

**facing** the problem that Campaign Mode uses `AskUserQuestion` extensively for proactive elicitation (ADR-CM-008), causing repeated focus-stealing throughout quest sessions, particularly during Phase 3 where animal Next Perspective handoffs and recovery flows trigger frequent questions,

**we decided for** a hybrid approach — keeping `AskUserQuestion` for phase transition questions (with mandatory context summaries in the question text so users don't need to scroll up) and switching to plain-text numbered choices for mid-flow advisory questions (to avoid focus-stealing entirely),

**and neglected** (a) all plain text for every question (loses the structured UI and established elicitation convention for critical phase decisions), (b) all `AskUserQuestion` with "press to continue" pauses before each question (doubles the turn count and makes sessions tedious), (c) status quo (known UX problem that degrades the quest experience),

**to achieve** a quest experience where users always have sufficient context to answer questions — either through embedded summaries in `AskUserQuestion` or through inline plain-text choices that don't steal focus — without doubling session turn count or losing structured UI for critical decisions,

**accepting that** agents must now classify each question as "phase transition" or "mid-flow advisory", plain-text choices require agents to parse free-form user responses (number or description), and the convention adds implementation complexity to every agent that presents options.

---

## Context

In Claude Desktop, `AskUserQuestion` renders as a structured UI component (chips/buttons) that appears immediately and steals scroll focus. This means the user is pulled away from reading the agent's preceding text — the narrative framing, assessment details, or context that makes the question meaningful.

Campaign Mode relies heavily on `AskUserQuestion` for proactive elicitation (established in ADR-CM-008). Every phase transition, every animal Next Perspective handoff (ADR-CM-017), every Guardian gate decision, and every Dragon verdict ends with an `AskUserQuestion`. In a typical quest session, this means dozens of focus-stealing events.

The impact varies by question type:

- **Phase transitions** (e.g., "Guardian approved — what's next?", "Dragon slain — begin debrief?") are critical decisions where the structured UI adds value. The problem is solvable by embedding context summaries in the question text.
- **Mid-flow advisory** (e.g., animal Next Perspective handoffs, Guardian block recovery, Dragon prevails recovery) are lighter-weight suggestions where the structured UI adds less value and the focus-stealing is most disruptive.

## Options Considered

### Option 1: Hybrid — AskUserQuestion for Phase Transitions, Plain Text for Mid-Flow (Selected)

Classify each question type and apply the appropriate presentation:
- Phase transitions use `AskUserQuestion` with mandatory context summaries
- Mid-flow advisory uses plain-text numbered choices in the response body

**Pros:**
- Preserves structured UI for critical decisions (campaign mode selection, phase transitions, Dragon verdict)
- Eliminates focus-stealing for frequent mid-flow questions (Next Perspective, recovery flows)
- Context summaries ensure users always understand the question without scrolling
- Minimal disruption to existing convention — most `AskUserQuestion` calls are retained

**Cons:**
- Two presentation patterns to maintain and document
- Plain-text responses require parsing (user types number or description)
- Agents must classify each question correctly

### Option 2: All Plain Text (Rejected)

Replace every `AskUserQuestion` with plain-text numbered choices.

**Why rejected:** Loses the structured UI entirely. Phase transition questions (campaign mode selection, Dragon confrontation outcomes) benefit from the structured presentation — these are consequential decisions, not casual suggestions. Also breaks the established convention from ADR-CM-008 more than necessary.

### Option 3: All AskUserQuestion with Pause Prompts (Rejected)

Keep every `AskUserQuestion` but precede each with a "press to continue" pause so the user reads context first.

**Why rejected:** Doubles the turn count for every question. A quest session with 15 questions becomes 30 turns. This creates tedium that undermines the quest experience — the cure is worse than the disease.

### Option 4: Status Quo (Rejected)

Accept the focus-stealing as a Claude Desktop limitation.

**Why rejected:** The UX degradation is real and measurable — users report losing context when questions appear. Campaign Mode's heavy use of `AskUserQuestion` makes this worse than typical Claude Desktop usage. A mitigation is achievable without major architectural changes.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-011-A](../3_specs/SPEC-CM-011-A-AskUserQuestion-Presentation-Protocol.md) | AskUserQuestion Presentation Protocol | Classification rules, context summary requirements, plain-text format, per-question-type guidance |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-008 | Proactive Elicitation | Refines how `AskUserQuestion` is used — adds context summaries and plain-text alternative |
| Relates To | ADR-CM-017 | Proactive Party Engagement | Next Perspective handoffs switch from `AskUserQuestion` to plain text |
| Relates To | ADR-CM-014 | Animal Campaign Extensions | Animal extension file updated for plain-text Next Perspective |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Animal Campaign Extensions | Extension File | [extensions/animal-campaign-context.md](../../extensions/animal-campaign-context.md) |
| REF-002 | Guardian Agent Skill | Internal Skill | [skills/guardian-agent/SKILL.md](../../skills/guardian-agent/SKILL.md) |
| REF-003 | Dragon Agent Skill | Internal Skill | [skills/dragon-agent/SKILL.md](../../skills/dragon-agent/SKILL.md) |
| REF-004 | Gandalf Agent Skill | Internal Skill | [skills/gandalf-agent/SKILL.md](../../skills/gandalf-agent/SKILL.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-17 |
| Accepted | Chris Barlow | 2026-02-17 |
