# ADR-CM-008: Proactive Elicitation

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-008 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-001](ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode's six-phase lifecycle requiring smooth transitions between phases,

**facing** silent phase transitions that drop the user — agents deliver output then go quiet, expecting users to remember which slash command to type next, breaking flow and violating the protagonist principle,

**we decided for** proactive elicitation — every agent uses `AskUserQuestion` at phase transitions to offer structured next-step options in natural language,

**and neglected** fully autonomous agent orchestration (violates the User as Protagonist principle by removing user agency) and the status quo (proven broken in testing — users lose momentum at every transition),

**to achieve** seamless phase transitions where the user never needs to remember slash commands, the protagonist principle is preserved through meaningful choices at every decision point, and campaign flow feels continuous rather than fragmented,

**accepting that** agent responses at transitions are slightly longer, all NPC agents must consistently offer transitions (a missed transition is a bug), and agents must never reference slash commands in user-facing text.

---

## Context

Campaign Mode's workflow has a structural problem at phase boundaries. When an agent completes its work in a phase — Gandalf finishes quest framing, Guardian delivers a verdict, Dragon announces a result — the conversation simply stops. The user is left to remember which `/slash-command` invokes the next agent.

This creates three problems:
1. **Flow drops** — Momentum built during a phase evaporates at the boundary
2. **Cognitive load** — Users must remember the command vocabulary instead of focusing on their quest
3. **Slash command leakage** — Agents reference internal commands (e.g., "invoke `/dragon-agent`") rather than facilitating the transition directly

The protagonist principle says the user drives the quest. But "driving" should mean making meaningful choices, not memorising commands.

## Options Considered

### Option 1: Proactive Elicitation (Selected)

At every phase transition, the active agent uses `AskUserQuestion` to present natural-language options for what to do next. The user chooses; the system facilitates.

**Pros:** User retains agency through choices, flow never drops, no command memorisation required, consistent with existing `AskUserQuestion` mechanics
**Cons:** Slightly longer agent responses at transitions, requires discipline across all agents

### Option 2: Fully Autonomous Orchestration (Rejected)

Agents automatically invoke the next agent when a phase completes — no user involvement in transitions.

**Why rejected:** Violates the User as Protagonist principle. The user would become a passenger in their own quest. Removing transition choices removes agency.

### Option 3: Status Quo (Rejected)

Keep the current pattern where agents deliver output and wait for the user to invoke the next agent.

**Why rejected:** Proven broken in practice. Users consistently lose momentum at phase boundaries and must be told which command to use next.

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Refines | ADR-CM-001 | Campaign Mode Architecture | Adds transition behaviour to the campaign lifecycle |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Affects how NPCs hand off between phases |
| Relates To | ADR-CM-003 | NPC Context Isolation | Transitions must respect isolation boundaries |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Campaign Lifecycle Spec | Internal Spec | [SPEC-CM-001-B](../3_specs/SPEC-CM-001-B-Campaign-Lifecycle.md) |
| REF-002 | NPC SKILL.md Files | Internal Skills | `skills/gandalf-agent/`, `skills/guardian-agent/`, `skills/dragon-agent/` |

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
