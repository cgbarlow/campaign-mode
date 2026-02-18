# SPEC-CM-003-A: Context Isolation Protocol

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-003-A |
| **Parent ADR** | [ADR-CM-003](../adrs/ADR-CM-003-NPC-Context-Isolation.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-18 |

---

## Overview

This specification defines how context isolation is implemented for each NPC in Campaign Mode. Context isolation ensures that NPC agents provide independent evaluation by controlling what information they can access.

---

## Isolation Principle

> NPCs evaluate the **work**, not the **workers**. Any context that reveals party reasoning, internal discussion, or emotional state compromises this independence.

---

## NPC Isolation Profiles

### Gandalf (Mentor) — Advisory Isolation

Gandalf has the **softest** isolation requirement because the mentor role requires understanding the party's situation to provide relevant counsel.

**Receives:**
- Quest definition (which Gandalf created)
- Party's current situation and challenges (when consulted)
- General progress information
- Conversation transcripts from `.campaign/conversations/` (advisory context for continuity across sessions)

**Does NOT receive:**
- Dragon's evaluation criteria or assessments
- Guardian's checkpoint results or feedback
- Other NPCs' internal reasoning

**Rationale:** Gandalf's value comes from understanding context to provide relevant guidance. However, Gandalf's knowledge must not leak to Dragon or Guardian — the mentor's context is kept separate from the evaluators.

### Guardian (Gatekeeper) — Independent Isolation

The Guardian has **moderate** isolation to ensure objective quality evaluation.

**Receives:**
- Work product for the current checkpoint stage
- General expectations for the current stage (what "ready to advance" means)
- The quest's overall structure (to understand what stage this is)

**Does NOT receive:**
- Party conversation history or internal discussions
- Gandalf's counsel or mentorship notes
- Dragon's success criteria or assessment methods
- Party's reasoning, justifications, or confidence levels (unless expressed in the work product itself)
- Previous Guardian checkpoint results (each checkpoint is independently evaluated)
- Conversation transcripts from `.campaign/conversations/` (contain party reasoning and advisory context)

**Rationale:** The Guardian must evaluate work quality on its own merits. Access to party reasoning would bias evaluation toward intent over evidence. Each checkpoint is independently assessed to prevent cumulative bias.

### Dragon (Adversary) — Maximum Isolation

The Dragon has the **strictest** isolation to ensure purely objective adversarial testing.

**Receives:**
- Success criteria (from Gandalf's quest definition in Phase 1)
- Final work product (the party's deliverable)

**Does NOT receive:**
- Party conversation history
- Gandalf's mentorship notes, counsel, or rationale for the criteria
- Guardian checkpoint results (whether the party passed intermediate gates)
- Intermediate work products (only the final submission)
- Party's reasoning, justifications, or explanations
- Any information about the party's process, struggles, or journey
- Conversation transcripts from `.campaign/conversations/` (contain all of the above)

**Rationale:** The Dragon is the ultimate test of whether the work stands on its own. If the Dragon can see that the party struggled mightily or that Gandalf guided them through a tough spot, it may unconsciously give credit for effort rather than evaluating output. Maximum isolation ensures the Dragon evaluates only what's delivered.

---

## Enforcement Mechanisms

### v1: Instruction-Based Isolation

Each NPC's SKILL.md contains explicit isolation directives:

```markdown
## Context Isolation

You operate independently of the party's conversation context. You:
- Evaluate only the work product provided to you
- Do NOT ask the party to explain their reasoning
- Do NOT access or reference party conversation history
- Form your assessment based solely on the materials provided
```

### v1: Sub-Agent Invocation

When invoking NPCs, the recommended pattern is to use Claude Code's Task tool to create a sub-agent:

```
User invokes /dragon-agent with work product
→ Claude creates a sub-agent (fresh context)
→ Sub-agent receives: success criteria + work product
→ Sub-agent returns: evaluation results
→ Results presented to the user
```

The sub-agent mechanism provides practical isolation because the sub-agent starts with a clean context window. It does not inherit the parent conversation's history.

### Input Scoping

The invoking prompt should explicitly scope what the NPC receives:

**Good (scoped):**
> "Evaluate this work against the following success criteria: [criteria]. Here is the work product: [product]."

**Bad (unscoped):**
> "The party has been working on this quest and they've had some challenges but they think they've met the criteria. Can you check?"

---

## Isolation Boundaries Diagram

```
┌─────────────────────────────────────────────────────┐
│                    PARTY CONTEXT                      │
│  Bear, Cat, Owl, Puppy, Rabbit, Wolf                 │
│  (shared conversation, mutual visibility)             │
├─────────────────────────────────────────────────────┤
│                                                       │
│  .campaign/conversations/  [transcript files]         │
│  ┌───────────────────────────────────────────┐       │
│  │ Animals, Gandalf, Council: READ + WRITE   │       │
│  │ Guardian, Dragon:          WRITE ONLY     │       │
│  └───────────────────────────────────────────┘       │
│                                                       │
│  ┌──────────┐    ┌──────────┐    ┌──────────┐       │
│  │ Gandalf  │    │ Guardian │    │  Dragon  │       │
│  │ Advisory │    │ Independ.│    │ Maximum  │       │
│  │          │    │          │    │          │       │
│  │ Sees:    │    │ Sees:    │    │ Sees:    │       │
│  │ Quest +  │    │ Stage    │    │ Criteria │       │
│  │ situation│    │ work     │    │ + final  │       │
│  │ + transcr│    │ product  │    │ work     │       │
│  └──────────┘    └──────────┘    └──────────┘       │
│       ↑               ↑               ↑              │
│       │               │               │              │
│  [quest context   [stage work]   [criteria +         │
│   + transcripts]                  final work]        │
│                                                       │
│  ╳ No cross-NPC communication                        │
│  ╳ No party reasoning flows to evaluators            │
│  ╳ No transcript reading by Guardian or Dragon       │
└─────────────────────────────────────────────────────┘
```

---

## Limitations and Future Evolution

### Current Limitations (v1)

1. **Advisory, not architectural** — Claude may still have access to prior context in the conversation window. Instruction-based isolation depends on the model faithfully following directives.
2. **Sub-agent limitations** — Claude Code's Task tool creates sub-agents, but the isolation boundary is practical (fresh context) rather than cryptographic (separate sessions).
3. **User can bypass** — A user can choose to paste party reasoning into a Dragon evaluation prompt. The skill cannot prevent this, only advise against it.

### Future Strengthening

| Approach | Effect | Timeline |
|----------|--------|----------|
| Claude plugin architecture | Separate plugin sessions per NPC | When available |
| Custom API orchestration | Fully separate API calls per NPC | Post-v1 |
| Multi-agent frameworks | Architectural isolation via agent boundaries | Post-v1 |

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-002-A](SPEC-CM-002-A-Gandalf-Agent.md) | Gandalf Agent | Gandalf's advisory isolation profile |
| [SPEC-CM-002-B](SPEC-CM-002-B-Dragon-Agent.md) | Dragon Agent | Dragon's maximum isolation profile |
| [SPEC-CM-002-C](SPEC-CM-002-C-Guardian-Agent.md) | Guardian Agent | Guardian's independent isolation profile |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Which phases require isolation |
| [SPEC-CM-012-A](SPEC-CM-012-A-Conversation-Transcript-Protocol.md) | Conversation Transcript Protocol | Transcript isolation rules extend this protocol |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.1 | 2026-02-18 | Chris Barlow | Added conversation transcript isolation rules — Gandalf receives transcripts, Guardian and Dragon do not. Updated isolation boundaries diagram. |
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
