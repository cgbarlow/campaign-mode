# SPEC-CM-012-A: Conversation Transcript Protocol

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-012-A |
| **Parent ADR** | [ADR-CM-019](../2_adrs/ADR-CM-019-Conversation-Transcript-Recording.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-18 |

---

## Overview

This specification defines the protocol for recording full verbatim conversation transcripts during Campaign Mode sessions. Every agent consultation produces a transcript file in `.campaign/conversations/`, preserving the complete exchange for future reference across sessions.

---

## Directory & Naming

### Directory

```
.campaign/conversations/
```

Created on first use via `mkdir -p .campaign/conversations/`.

### Filename Format

```
{YYYY-MM-DD}-{HH-MM}-{agent}.md
```

- Date-first ensures chronological sort order when listing files by name
- Time uses 24-hour format
- Agent is the archetype name (lowercase), not the profile name

### Agent Values

Valid agent identifiers for filenames:

| Agent | Filename Value |
|-------|---------------|
| Bear | `bear` |
| Cat | `cat` |
| Owl | `owl` |
| Puppy | `puppy` |
| Rabbit | `rabbit` |
| Wolf | `wolf` |
| Gandalf | `gandalf` |
| Guardian | `guardian` |
| Dragon | `dragon` |
| Council | `council` |

### Example Filenames

```
2026-02-18-14-32-cat.md
2026-02-18-15-10-owl.md
2026-02-18-16-00-guardian.md
2026-02-19-09-15-gandalf.md
```

---

## Transcript File Format

```yaml
---
agent: cat
profile-name: Rogue
phase: 3
campaign-mode: Grow & Ship
date: 2026-02-18T14:32:00
---

## Conversation Transcript

### Context
Quest: {quest name}
Consultation purpose: {e.g., Phase 3 advisory, Guardian checkpoint, Dragon confrontation}

### Exchange
**User:** {verbatim}

**🐱 Rogue:** {verbatim}

{...full exchange...}

### Outcome
{Verdict, recommendation, action items — if applicable}
```

### Frontmatter Fields

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `agent` | String | Yes | Archetype identifier (lowercase) — matches filename |
| `profile-name` | String | No | Assigned profile name, if a profile exists. Omit if no profile is assigned. |
| `phase` | Integer (1–6) | Yes | Current campaign phase at time of conversation |
| `campaign-mode` | String | Yes | One of `Grow`, `Ship`, or `Grow & Ship` |
| `date` | DateTime (ISO 8601) | Yes | Timestamp of conversation start |

### Body Sections

| Section | Description | Required |
|---------|-------------|----------|
| **Context** | Quest name and consultation purpose | Yes |
| **Exchange** | Full verbatim exchange with speaker tags | Yes |
| **Outcome** | Verdict, recommendation, or action items | Only if applicable (e.g., Guardian verdict, Dragon verdict, specific recommendations) |

### Speaker Tags in Exchange

Use the same speaker identification format as the agent's normal responses:
- Animals: `**{emoji} {Name}:**` (e.g., `**🐱 Rogue:**` or `**🐱 Cat:**`)
- NPCs: `**{emoji} {Name}:**` (e.g., `**🧙 Gandalf:**`, `**🛡️ Guardian:**`, `**🐉 Dragon:**`)
- User: `**User:**`
- Council animals: Each animal uses its own speaker tag within the council transcript

---

## Write Protocol

Every agent follows this protocol at the end of each consultation:

1. **Ensure directory exists:** Use Bash to run `mkdir -p .campaign/conversations/`
2. **Construct filename:** Use the agent's archetype name and the current date/time in the format `{YYYY-MM-DD}-{HH-MM}-{agent}.md`
3. **Construct transcript:** Build the full transcript from the conversation, including frontmatter, context, verbatim exchange, and outcome (if applicable)
4. **Write file:** Use the Write tool to create the file in `.campaign/conversations/`
5. **Do silently:** Do not mention the transcript to the user. Do not break character to perform this step. This is a background housekeeping task.

---

## Isolation Rules for Transcript Access

Context isolation (ADR-CM-003, SPEC-CM-003-A) applies to transcript files. Transcripts contain party reasoning, advisory context, and internal discussion — exactly the kind of information that evaluators must not access.

| Agent | Can Write Own Transcript | Can Read Other Transcripts |
|-------|--------------------------|---------------------------|
| Animals (Bear, Cat, Owl, Puppy, Rabbit, Wolf) | Yes | Yes |
| Gandalf | Yes | Yes |
| Guardian | Yes | **No** — transcripts contain party reasoning |
| Dragon | Yes | **No** — transcripts contain party reasoning + advisory context |
| Council | Yes | Yes |

### Enforcement

- Guardian and Dragon SKILL.md files include explicit isolation warnings against reading transcript files
- When acting as Guardian or Dragon, do not access `.campaign/conversations/` for reading
- Guardian and Dragon may only write their own transcript file at the end of their evaluation

---

## When Each Agent Writes

| Agent | Trigger | Timing |
|-------|---------|--------|
| Animal (Phase 3) | End of consultation | Before presenting Next Perspective options |
| Gandalf (Phase 1) | End of quest definition | Before Phase 2/3 transition |
| Gandalf (mid-campaign) | End of strategic counsel | Before presenting transition options |
| Gandalf (Phase 5 prep) | End of readiness review | Before Dragon transition options |
| Guardian | End of checkpoint | After verdict + quest.md update, before transition options |
| Dragon | End of confrontation | After verdict + quest.md update, before transition options |
| Council | End of council session | After council report write, before transition options |

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Defines the `.campaign/` directory that contains the `conversations/` subdirectory |
| [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md) | Context Isolation Protocol | Isolation rules that govern transcript read access |
| [SPEC-CM-010-A](SPEC-CM-010-A-Proactive-Party-Engagement.md) | Proactive Party Engagement | Animals write transcripts before Next Perspective options |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-18 | Chris Barlow | Initial specification |
