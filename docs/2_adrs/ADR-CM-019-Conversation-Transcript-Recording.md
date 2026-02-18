# ADR-CM-019: Conversation Transcript Recording

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-019 |
| **Type** | Standard ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-18 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode conversations being ephemeral — when a session ends, everything discussed with agents is lost, and the Progress Log in `quest.md` captures only milestone summaries (e.g., "Guardian checkpoint — Approved"), not the reasoning, advice, or discussion that led there,

**facing** the problem that users cannot review what was discussed with specific agents, trace how thinking evolved across animal consultations, or recall detailed feedback from previous sessions,

**we decided for** per-session transcript files in `.campaign/conversations/`, written silently by each agent at the end of every consultation, with one file per conversation session using date-first filenames for chronological sorting,

**and neglected** (a) summary-only logs (user wants verbatim records, not compressed summaries), (b) a single chronological log file (unbounded growth as campaigns progress), (c) per-agent append files (individual files grow large over many sessions, making it hard to find specific conversations),

**to achieve** full verbatim conversation history that persists across sessions, enabling users to review past advice, trace reasoning evolution, and pick up context from previous consultations without relying on memory or the brief Progress Log entries,

**accepting that** transcript files add storage to `.campaign/`, agents must perform a silent write operation at the end of every consultation, and context isolation rules (ADR-CM-003) must be carefully maintained — Guardian and Dragon write their own transcripts but must NOT read any, as party reasoning remains off-limits to independent evaluators.

---

## Context

Campaign Mode conversations are ephemeral. When a Claude Code session ends, everything discussed with agents is lost. The Progress Log in `.campaign/quest.md` captures only milestone summaries — phase transitions, Guardian verdicts, Dragon confrontations — but not the reasoning, advice, or discussion that produced those milestones.

This creates several problems:
- Users cannot review what a specific animal advisor said about a particular success criterion
- Thinking that evolved across multiple animal consultations is not traceable
- Detailed feedback from Guardian checkpoints or Dragon confrontations is lost once the session ends
- When resuming a quest via `/continue-quest`, only the Progress Log provides history — not the rich discussion context

The solution is automatic transcript recording: every agent consultation produces a full verbatim transcript saved to `.campaign/conversations/`. One file per conversation session, written silently by the agent at the end of each consultation.

**Critical constraint:** Context isolation (ADR-CM-003) must be preserved. Guardian and Dragon write their own transcripts but must NOT read any — party reasoning remains off-limits to independent evaluators.

## Options Considered

### Option 1: Per-Session Transcript Files (Selected)

One file per conversation session in `.campaign/conversations/`, named with date-first format (`{YYYY-MM-DD}-{HH-MM}-{agent}.md`) for chronological sorting.

**Pros:**
- Each conversation is a discrete, findable file
- Date-first naming ensures `ls` shows files in chronological order
- Files stay small — one session per file
- Easy to grep across conversations for specific topics
- Natural integration with `/continue-quest` (glob for recent files)

**Cons:**
- Many files accumulate over a long campaign
- Requires `mkdir -p` on first write

### Option 2: Summary-Only Logs (Rejected)

Write condensed summaries instead of verbatim transcripts.

**Why rejected:** The user wants verbatim records. The Progress Log already provides summaries. The value of transcripts is in preserving the full exchange — the exact advice, the exact questions, the exact reasoning.

### Option 3: Single Chronological Log File (Rejected)

Append all conversations to a single `.campaign/conversation-log.md` file.

**Why rejected:** Unbounded growth. A long campaign with many animal consultations, Guardian checkpoints, and Gandalf sessions would produce a file that becomes unwieldy to read or search. File-per-session keeps each record manageable.

### Option 4: Per-Agent Append Files (Rejected)

One file per agent (e.g., `.campaign/conversations/cat.md`) that grows over time.

**Why rejected:** Individual files grow large over many sessions. Finding a specific conversation requires scrolling through the entire file. The per-session approach makes each conversation independently addressable.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-012-A](../3_specs/SPEC-CM-012-A-Conversation-Transcript-Protocol.md) | Conversation Transcript Protocol | Directory structure, file format, write protocol, isolation rules, per-agent timing |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-010 | Quest State Tracking | Adds conversation history alongside the Progress Log in quest.md |
| Extends | ADR-CM-003 | NPC Context Isolation | Transcripts follow the same isolation rules — Guardian and Dragon must not read them |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Campaign State Directory | Specification | [SPEC-CM-006-B](../3_specs/SPEC-CM-006-B-Campaign-State-Directory.md) |
| REF-002 | Context Isolation Protocol | Specification | [SPEC-CM-003-A](../3_specs/SPEC-CM-003-A-Context-Isolation-Protocol.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-18 |
| Accepted | Chris Barlow | 2026-02-18 |
