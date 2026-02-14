# SPEC-CM-005-A: Campaign Mode Profiles

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-005-A |
| **Parent ADR** | [ADR-CM-005](../adrs/ADR-CM-005-Campaign-Mode-Selection.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines how each campaign mode (Grow, Ship, Grow & Ship) tunes the behaviour of all three NPC agents and affects each phase of the campaign lifecycle. It serves as the reference matrix for implementing mode-aware behaviour in skill files.

---

## Mode Selection Protocol

Mode selection occurs during Phase 1 (Quest Definition), owned by Gandalf. The protocol:

1. Gandalf greets the user and establishes initial context
2. Before framing the quest, Gandalf presents the mode selection:

```
Before we frame this quest, what matters most to you?

  Grow        -- Learning experience. Discover something about yourself.
  Ship        -- Get work done. Diverse perspectives covering blind spots.
  Grow & Ship -- Both. Growth through doing. (Default)

What's your focus?
```

3. The user selects a mode (or accepts the default)
4. Gandalf acknowledges the selection and proceeds with mode-appropriate quest framing
5. The selected mode is recorded in the quest definition and passed to all subsequent NPC interactions

### Default Behaviour

If the user does not express a preference or skips the selection, **Grow & Ship** is used as the default. This preserves the current balanced behaviour and ensures no user gets an unexpected experience.

### Mode Persistence

The mode is set once per campaign and does not change. All NPCs receive the mode as part of their context for the duration of the campaign. This ensures consistent expectations from quest framing through Dragon confrontation.

---

## Mode-Agent Interaction Matrix

### Gandalf (Mentor)

| Dimension | Grow | Ship | Grow & Ship |
|-----------|------|------|-------------|
| **Quest framing** | Reflective questions: "What will you learn? Who will you become?" | Clear objectives: "What will you deliver? What does done look like?" | Both: "What will you learn AND deliver?" |
| **Success criteria** | Weighted toward transformation criteria -- growth and understanding alongside deliverables | Weighted toward deliverable criteria -- concrete outputs and quality measures | Both required -- transformation and deliverable criteria given equal weight |
| **Mentorship style** | Socratic -- deeper check-ins, more probing questions, encourages reflection on process | Direct and efficient -- focused counsel, minimal reflection overhead | Balanced -- reflection woven into practical guidance |
| **Dragon preparation** | Emphasises both transformation and deliverable readiness | Focuses on deliverable completeness and quality | Reviews both dimensions pragmatically |
| **Interaction frequency** | More frequent touchpoints encouraged | Touchpoints when needed, not mandated | Touchpoints as natural checkpoints |

### Dragon (Adversary)

| Dimension | Grow | Ship | Grow & Ship |
|-----------|------|------|-------------|
| **Evaluation scope** | Tests both transformation AND deliverable criteria | Tests deliverable criteria only | Tests both, pragmatically |
| **Transformation assessment** | Required for Dragon Slain -- evidence of growth must be demonstrated | Not assessed -- the Dragon evaluates work product only | Assessed but not strictly required -- noted as strength or gap |
| **Rigour on deliverables** | Standard -- deliverables must meet criteria | Maximum -- this is the primary evaluation axis | Standard -- balanced across both dimensions |
| **Feedback on failure** | Highlights growth gaps alongside deliverable gaps | Focuses on what deliverables are missing or incomplete | Addresses both dimensions in feedback |

### Guardian (Gatekeeper)

| Dimension | Grow | Ship | Grow & Ship |
|-----------|------|------|-------------|
| **Checkpoint focus** | ZPD assessment, understanding, lenient on polish -- is the party growing? | Deliverable quality and completeness -- is the work ready? | Both -- quality and growth assessed together |
| **Progression speed** | Deliberate -- growth takes time, don't rush past learning moments | Efficient -- move forward when deliverables meet the bar | Balanced -- neither rushing nor artificially slow |
| **Blocking threshold** | Blocks on shallow understanding even if deliverables look correct | Blocks on deliverable quality gaps, not on understanding depth | Blocks on significant gaps in either dimension |
| **Feedback style** | Developmental -- "here's what you might explore further" | Practical -- "here's what needs to change" | Both -- practical guidance with growth observations |

---

## Mode Effects on Campaign Phases

### Phase 1: Quest Definition

| Mode | Effect |
|------|--------|
| **Grow** | Gandalf asks deeper reflective questions. Transformation criteria are primary. Success criteria include "what will you understand differently?" |
| **Ship** | Gandalf focuses on clear objectives and deliverables. Success criteria are concrete and measurable. Minimal reflection overhead. |
| **Grow & Ship** | Gandalf balances both. Success criteria include both deliverables and transformation. |

### Phase 2: Character Setup

| Mode | Effect |
|------|--------|
| **Grow** | Encouraged. Character profiles add reflective depth and help the user explore different perspectives. |
| **Ship** | Skipped. Character setup is not productivity-relevant. Proceed directly to Phase 3. |
| **Grow & Ship** | Optional. The user chooses whether character setup adds value to their campaign. |

### Phase 3: Campaign Execution

| Mode | Effect |
|------|--------|
| **Grow** | More reflective pauses. Gandalf may prompt: "What are you noticing about your process?" Animals encouraged to surface learning moments. |
| **Ship** | Efficient execution. Focus on deliverable progress. Animals contribute their archetype strengths toward output. |
| **Grow & Ship** | Natural balance. Reflection happens through the work, not as separate activity. |

### Phase 4: Guardian Checkpoint

| Mode | Effect |
|------|--------|
| **Grow** | Guardian assesses understanding and ZPD alongside deliverable quality. More lenient on polish, stricter on depth. |
| **Ship** | Guardian focuses on deliverable quality and completeness. Faster progression when quality bar is met. |
| **Grow & Ship** | Guardian evaluates both dimensions. Balanced progression speed. |

### Phase 5: Dragon Confrontation

| Mode | Effect |
|------|--------|
| **Grow** | Dragon evaluates both transformation and deliverable criteria. Transformation evidence required for Dragon Slain. |
| **Ship** | Dragon evaluates deliverable criteria only. Transformation is not assessed. |
| **Grow & Ship** | Dragon evaluates both. Transformation is assessed and noted but not strictly required for Dragon Slain. |

### Phase 6: Debrief

| Mode | Effect |
|------|--------|
| **Grow** | Full pedagogical reflection. Simon analyses role performance, group dynamics, learning moments, and personal growth. Deeper "behind the curtain" insights. |
| **Ship** | Brief retrospective. Simon focuses on process effectiveness, what worked, what to improve next time. Minimal pedagogical analysis. |
| **Grow & Ship** | Balanced debrief. Simon covers both growth insights and process effectiveness. |

---

## Context Isolation Update

Campaign mode is added to the context that each NPC receives:

| NPC | Current Context | Added Context |
|-----|-----------------|---------------|
| **Gandalf** | Quest topic, party interactions | Campaign mode selection |
| **Dragon** | Success criteria, final work product | Campaign mode selection |
| **Guardian** | Work product, stage expectations | Campaign mode selection |

The mode does not break context isolation -- it is a single piece of metadata (Grow / Ship / Grow & Ship) that helps NPCs calibrate their behaviour appropriately.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Mode selection occurs in Phase 1 and affects all phases |
| [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md) | Context Isolation Protocol | Mode is added to NPC context without breaking isolation |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
