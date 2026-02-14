# ADR-CM-010: Quest State Tracking

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-010 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-001](ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** implementing the reserved `.campaign/quest.md` for durable campaign state,

**facing** NPC handoffs relying on conversation context rather than persisted state — `/continue-quest` cannot reconstruct where the user left off, Dragon and Guardian receive criteria and mode from conversational memory instead of a canonical source, and session boundaries break campaign continuity,

**we decided for** a simple markdown file with YAML frontmatter (`.campaign/quest.md`) written by Gandalf at quest definition and updated by Guardian and Dragon at key moments, with an append-only progress log recording phase transitions,

**and neglected** database or JSON state management (over-engineered for a skill-based system), external state services (introduces dependencies), and no persistence (the broken status quo),

**to achieve** durable campaign state across sessions, context-aware re-entry via `/continue-quest`, reliable NPC handoffs where Dragon and Guardian read success criteria and campaign mode from file rather than conversation context, and a human-readable quest record,

**accepting that** agents must remember to update the file at transition points (state is advisory, not enforced), the progress log is append-only and may grow long in extended campaigns, and the file format is not machine-validated.

---

## Context

Campaign state tracking was architecturally reserved in [SPEC-CM-006-B](../3_specs/SPEC-CM-006-B-Campaign-State-Directory.md) — the `.campaign/quest.md` file was listed in the directory structure but marked "reserved, not yet specified." The entry commands (`/start-quest`, `/continue-quest`) already check for its existence, but nothing writes it. Gandalf's SKILL.md instructs "Record the mode in the quest definition" but provides no mechanism to do so.

This creates a practical gap:

1. **Session continuity** — `/continue-quest` detects whether `quest.md` exists but cannot reconstruct quest context (narrative, criteria, phase, mode) because the file is never written
2. **NPC handoffs** — Dragon and Guardian are supposed to receive success criteria and campaign mode, but these exist only in conversation context, which is lost between sessions
3. **Progress visibility** — There is no durable record of Guardian checkpoints or Dragon confrontations

## Decision

Use the same markdown-with-YAML-frontmatter pattern established by character profiles ([SPEC-CM-006-A](../3_specs/SPEC-CM-006-A-Character-Profile-Format.md)). The file is created by Gandalf at the end of Phase 1 and updated by NPC agents at key transitions.

### File Format

```yaml
---
campaign-mode: Grow & Ship
phase: 3
created: 2026-02-14
---

## Quest Narrative
[Gandalf's framing of the quest]

## Success Criteria
1. [Criterion text]
2. [Criterion text]

## Anticipated Dragon
[The internal obstacle the user identified]

## Progress Log
- **Phase 1 complete** — Quest defined (2026-02-14)
- **Guardian checkpoint** — Approved (2026-02-14)
```

### Who Writes What

| Agent | Action | When |
|-------|--------|------|
| **Gandalf** | Creates `quest.md` with full content | End of Phase 1 (quest definition complete) |
| **Gandalf** | Updates phase, appends Phase 2 log entry | End of Phase 2 (or skip) |
| **Guardian** | Reads criteria/mode, appends checkpoint result | After delivering verdict |
| **Dragon** | Reads criteria/mode, appends confrontation result | After delivering verdict |

### Design Choices

- **Phase as integer** — Simple `phase: 1-6` field, updated at transitions. No complex state machine.
- **Append-only progress log** — Each NPC appends a one-line entry. No editing of previous entries.
- **Human-readable** — The file is plain markdown that users can read and understand.
- **Same pattern as profiles** — YAML frontmatter + markdown body, consistent with SPEC-CM-006-A.

## Consequences

### Positive
- `/continue-quest` can reconstruct full campaign context from the file
- Dragon and Guardian read criteria from a canonical source rather than conversation context
- Campaign progress is visible and durable across sessions
- The format is human-readable and follows existing conventions

### Negative
- Agents must consistently write to the file — a missed write breaks state tracking
- State is advisory (instruction-enforced), not architecturally enforced
- The progress log grows over time in long campaigns

---

## Related Decisions

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Parent | [ADR-CM-001](ADR-CM-001-Campaign-Mode-Architecture.md) | Campaign Mode Architecture | Master ADR |
| Relates To | [ADR-CM-006](ADR-CM-006-Character-Generation.md) | Character Generation | Established `.campaign/` directory and profile file pattern |
| Relates To | [ADR-CM-009](ADR-CM-009-Quest-Entry-Commands.md) | Quest Entry Commands | `/continue-quest` depends on quest.md for state reconstruction |

---

## Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-B](../3_specs/SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Updated to specify quest.md format |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
| Accepted | Chris Barlow | 2026-02-14 |
