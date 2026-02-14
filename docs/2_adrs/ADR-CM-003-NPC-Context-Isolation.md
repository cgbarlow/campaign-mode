# ADR-CM-003: NPC Context Isolation

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-003 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Proposed |

---

## WH(Y) Decision Statement

**In the context of** NPC agents needing to provide independent evaluation of party work,

**facing** the risk that shared context would allow the AI to "game the system" by feeding NPC judgement with party reasoning, undermining the objectivity that makes adversarial testing and gatekeeping valuable,

**we decided for** explicit context isolation where NPCs operate as sub-agents without access to party conversation history, with isolation enforced by instruction in the skill definitions,

**and neglected** shared-context NPCs (simpler but biased) and full process isolation via separate API sessions (overkill for current Claude architecture),

**to achieve** objective evaluation by Dragon and Guardian agents, ensuring that adversarial testing tests the work not the reasoning, and gatekeeping evaluates readiness not persuasiveness,

**accepting that** context isolation within Claude Code skills is currently advisory (enforced by instruction, not architecture) and may require future plugin/API evolution for hard enforcement.

---

## Context

Campaign Mode introduces NPC agents (Dragon, Guardian, and to a lesser extent Gandalf) that must evaluate party work independently. The value of these NPCs depends on their objectivity:

- **The Dragon** (Adversary) must test whether success criteria are met based on the work product alone. If the Dragon can see the party's reasoning, it may accept work that "sounds good" rather than work that "is good".
- **The Guardian** (Gatekeeper) must evaluate readiness based on deliverable quality. If the Guardian can see the party's internal discussions, it may approve based on good intentions rather than good output.
- **Gandalf** (Mentor) has a softer isolation requirement — Gandalf's counsel should not leak to Dragon or Guardian, but Gandalf naturally has more context about the party.

The fundamental principle: **NPCs evaluate the work, not the workers**. Shared context collapses this distinction.

## Options Considered

### Option 1: Instruction-Based Context Isolation (Selected)

NPCs are implemented as Claude Code skills with explicit instructions that they:
- Operate independently of party conversation history
- Evaluate only the work product and defined criteria
- Do not ask the party to explain their reasoning
- Are invoked as sub-agents (Claude Code Task tool) where possible

**Pros:**
- Works within current Claude Code architecture
- No additional infrastructure required
- Clear, explicit instructions in each NPC skill
- Progressive — can be strengthened later

**Cons:**
- Advisory, not enforced — the AI can theoretically access prior context
- Depends on Claude following instructions faithfully
- No hard architectural guarantee

### Option 2: Shared-Context NPCs (Rejected)

All agents (party and NPCs) share the same conversation context.

**Why rejected:** Defeats the purpose. A Dragon that can see party reasoning is not an independent evaluator — it's a rubber stamp. A Guardian that can see party discussions may approve based on intent rather than evidence.

### Option 3: Full Process Isolation via Separate API Sessions (Rejected)

Each NPC operates in a completely separate Claude API session with no shared context at all.

**Why rejected:** Overkill for the current implementation. Requires infrastructure for managing multiple sessions, passing work products between them, and coordinating results. This may be the right approach for a future plugin or API-based architecture, but it's excessive for v1 skill-based delivery.

---

## Isolation Levels

The specification defines three isolation levels:

| Level | NPC | What they receive | What they don't receive |
|-------|-----|-------------------|------------------------|
| **Advisory** | Gandalf | Quest context, party situation (when consulted) | Dragon/Guardian assessments |
| **Independent** | Guardian | Stage work product, general expectations | Party reasoning, Gandalf counsel, Dragon criteria |
| **Maximum** | Dragon | Success criteria + final work product only | Everything else |

---

## Enforcement Mechanism

In v1, context isolation is enforced through:

1. **Skill instructions** — Each NPC SKILL.md contains explicit isolation directives
2. **Sub-agent invocation** — NPCs are invoked via Claude Code's Task tool, which creates a sub-agent with a fresh context
3. **Input scoping** — The invoking prompt includes only the information the NPC should receive
4. **No-ask directives** — NPCs are instructed not to ask the party for explanations or reasoning

### Future Evolution

| Mechanism | Timeline | Effect |
|-----------|----------|--------|
| Skill instructions | v1 (now) | Advisory isolation |
| Sub-agent invocation | v1 (now) | Practical isolation (fresh context) |
| Claude plugin architecture | Post-v1 | Architectural isolation (separate sessions) |
| Custom API integration | Post-v1 | Full process isolation |

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-003-A](../specs/SPEC-CM-003-A-Context-Isolation-Protocol.md) | Context Isolation Protocol | Detailed protocol for each NPC's isolation level |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Context isolation is required by the 3-NPC design |
| Relates To | ADR-CM-004 | Skill-Based Implementation | Skills are the mechanism for enforcing isolation |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | North Star - Design Principles | Vision Document | docs/north-star.md (Context Isolation principle) |
| REF-002 | Claude Code Task Tool | Technical Reference | Claude Code documentation |

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
