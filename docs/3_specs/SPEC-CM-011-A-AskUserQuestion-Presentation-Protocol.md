# SPEC-CM-011-A: AskUserQuestion Presentation Protocol

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-011-A |
| **Parent ADR** | [ADR-CM-018](../2_adrs/ADR-CM-018-AskUserQuestion-UX-Conventions.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-17 |

---

## Overview

This specification defines how agents present questions and choices to the user in Campaign Mode. It addresses the Claude Desktop focus-stealing problem — where `AskUserQuestion` renders immediately and pulls the user away from the agent's preceding text — by classifying questions into two categories with different presentation rules.

**Phase transition questions** use `AskUserQuestion` with mandatory context summaries embedded in the question text, so the user has full context without scrolling up. **Mid-flow advisory questions** use plain-text numbered choices in the response body, avoiding focus-stealing entirely.

The classification is based on the question's role in the campaign lifecycle: consequential decisions that change the campaign phase use the structured UI; lighter-weight suggestions within a phase use plain text.

---

## 1. Question Classification

Every question presented to the user is classified as either a **phase transition** or a **mid-flow advisory** question.

### Phase Transition Questions (use AskUserQuestion)

These are consequential decisions that advance or redirect the campaign. They benefit from the structured UI and warrant the user's full attention.

| Question | Agent | When |
|----------|-------|------|
| Campaign mode selection | Gandalf | Phase 1 — Quest Definition |
| Transition to Campaign Execution | Gandalf | Phase 1→3 transition |
| Transition to Dragon Confrontation | Gandalf | Phase 3→5 transition |
| Guardian Approve — next step | Guardian | Phase 4 — after approval |
| Guardian Conditional — next step | Guardian | Phase 4 — after conditional approval |
| Dragon Slain — next step | Dragon | Phase 5 — after Dragon Slain |
| Continue-quest menu | Continue Quest | Mid-campaign re-entry |
| Start-quest mid-campaign options | Start Quest | Existing quest detected |
| No-quest options | Continue Quest | No active quest |

### Mid-Flow Advisory Questions (use plain text)

These are lighter-weight suggestions within a phase. They occur frequently and the focus-stealing is most disruptive here.

| Question | Agent | When |
|----------|-------|------|
| Animal Next Perspective handoff | Any animal | After every Phase 3 consultation |
| Guardian Block — recovery options | Guardian | Phase 4 — after block verdict |
| Dragon Prevails — recovery options | Dragon | Phase 5 — after Dragon Prevails |

---

## 2. Context Summary Requirement

Every `AskUserQuestion` must include a 1-2 sentence summary in the `question` field so the user has full context without scrolling up. The user should be able to understand the situation and make a decision from the question text alone.

### Per-Question Context Summary Guidance

| Question | What to summarise |
|----------|-------------------|
| Campaign mode selection | The quest topic established so far (e.g., "Your quest is about redesigning the authentication system. Before we frame it, what matters most to you?") |
| Transition to Campaign Execution | The recommended first advisor and why (e.g., "Your quest has significant unknowns and three risk-related criteria. How would you like to begin Phase 3?") |
| Transition to Dragon Confrontation | Readiness assessment (e.g., "You've addressed 4 of 5 criteria and feel confident on all. Ready for the Dragon?") |
| Guardian Approve | Verdict summary (e.g., "Your API design passed the checkpoint — endpoints are well-structured and error handling is consistent. What's next?") |
| Guardian Conditional | Conditions summary (e.g., "Your work is approved with conditions: rate limiting strategy needs detail before the next stage. What's next?") |
| Dragon Slain | Verdict summary (e.g., "All 4 success criteria met — the Dragon is slain. What would you like to do?") |
| Continue-quest menu | Progress summary (e.g., "Quest: Auth system redesign. Phase 3, Grow & Ship mode. Last progress: API design completed. What would you like to do?") |
| Start-quest mid-campaign options | Quest context (e.g., "You have an active quest: Auth system redesign (Phase 3, Grow & Ship). What would you like to do?") |

The summary must be derived from the actual campaign state — read from `quest.md`, the evaluation just completed, or the conversation context. Do not use generic placeholder text.

---

## 3. Plain-Text Format

Mid-flow advisory questions use plain-text numbered choices in the agent's response body. The user responds by typing a number or describing their choice in natural language.

### Format

```
Here's what I'd suggest next:

1. **{Option label}** — {one-line description}
2. **{Option label}** — {one-line description}
3. **{Option label}** — {one-line description}

What would you like to do?
```

### Context Embedding

The agent's preceding response text already provides context (the animal's advice, the Guardian's block reasoning, the Dragon's failure analysis). For plain-text questions, embed a brief summary of the key finding or status in the text immediately before the numbered options, so the options and context appear together without scrolling.

### Parsing User Responses

When the user responds to a plain-text question, agents must accept:
- A number (e.g., "1", "2", "3")
- A partial match on the option label (e.g., "consult the Cat", "address gaps")
- A free-form description of intent (e.g., "I want to talk to someone about the risks")

If the response is ambiguous, ask a brief clarifying follow-up in plain text.

---

## 4. Per-Question Detailed Guidance

### 4.1 Animal Next Perspective (Plain Text)

After every Phase 3 consultation, the animal presents plain-text numbered options:

```
Based on our discussion, here's what I'd suggest:

1. **Consult {suggested animal}** — {reason based on conversation}
2. **Consult a different advisor** — get a perspective I haven't suggested
3. **Continue working** — you're ready to work on your own
4. **Request evaluation or counsel** — Guardian checkpoint, Dragon confrontation, or Gandalf strategic counsel

What would you like to do?
```

The animal should include a brief summary of the key takeaway from the consultation before presenting options (e.g., "We've mapped three key risks and identified the authentication flow as the highest priority.").

### 4.2 Guardian Block Recovery (Plain Text)

After a block verdict, the Guardian presents plain-text numbered options:

```
The gaps identified are: {brief list of gaps}. Here are your options:

1. **Address the gaps** — return to campaign execution to strengthen the work
2. **Consult Gandalf** — get strategic counsel on how to address the gaps
3. **Discuss the verdict** — understand or challenge the Guardian's assessment

What would you like to do?
```

### 4.3 Dragon Prevails Recovery (Plain Text)

After a Dragon Prevails verdict, the Dragon presents plain-text numbered options:

```
{Criterion/criteria} not met. The following options remain:

1. **Return to the quest** — address the gaps in campaign execution
2. **Consult Gandalf** — seek the Mentor's counsel on what the Dragon found
3. **Request a Guardian checkpoint** — get an independent quality assessment before returning

What would you like to do?
```

The Dragon maintains its terse, unsentimental voice even in plain-text format.

### 4.4 Guardian Approve (AskUserQuestion with Context Summary)

The question text must include a summary of the approval verdict:

> "Your {stage} passed the checkpoint — {1-sentence summary of strengths}. What's your next step?"

### 4.5 Guardian Conditional (AskUserQuestion with Context Summary)

The question text must include a summary of the conditions:

> "Your {stage} is approved with conditions: {brief list of conditions to address}. What's your next step?"

### 4.6 Dragon Slain (AskUserQuestion with Context Summary)

The question text must include a summary of the verdict:

> "All {N} success criteria met — the Dragon is slain. What would you like to do?"

### 4.7 Gandalf Campaign Mode Selection (AskUserQuestion with Context Summary)

The question text must include the quest topic:

> "Your quest is about {topic}. Before we frame it, what matters most to you?"

### 4.8 Gandalf Transition to Campaign Execution (AskUserQuestion with Context Summary)

The question text must include the recommended advisor rationale:

> "Your quest has {key characteristic} — {recommended advisor reasoning}. How would you like to begin?"

### 4.9 Gandalf Transition to Dragon (AskUserQuestion with Context Summary)

The question text must include readiness assessment:

> "You've addressed {N} of {M} criteria and {confidence summary}. How would you like to proceed?"

### 4.10 Continue-Quest Menu (AskUserQuestion with Context Summary)

The question text must include the progress summary:

> "{Quest name}, {campaign mode}, {phase}. Last progress: {most recent entry}. What would you like to do?"

### 4.11 Start-Quest Mid-Campaign Options (AskUserQuestion with Context Summary)

The question text must include quest context:

> "You have an active quest: {quest name} ({phase}, {mode}). What would you like to do?"

---

## 5. Migration Summary

### Files Changed

| File | Change |
|------|--------|
| `CLAUDE.md` | New "AskUserQuestion Presentation" section |
| `extensions/animal-campaign-context.md` | Next Perspective switches from `AskUserQuestion` to plain-text numbered choices |
| `skills/guardian-agent/SKILL.md` | Block → plain text; Approve/Conditional get context summary instructions |
| `skills/dragon-agent/SKILL.md` | Prevails → plain text; Slain gets context summary instruction |
| `skills/gandalf-agent/SKILL.md` | Three questions get context summary instructions |
| `commands/continue-quest.md` | Menu question gets context summary instruction |
| `commands/start-quest.md` | Mid-campaign question gets context summary instruction |

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-010-A](SPEC-CM-010-A-Phase-3-Party-Engagement.md) | Phase 3 Party Engagement | Next Perspective protocol updated from AskUserQuestion to plain text |
| [SPEC-CM-008-A](SPEC-CM-008-A-Animal-Campaign-Extensions.md) | Animal Campaign Extensions | Extension file updated with plain-text Next Perspective |
| [SPEC-CM-002-A](SPEC-CM-002-A-Gandalf-Agent.md) | Gandalf Agent | Context summary instructions added to three transition questions |
| [SPEC-CM-002-B](SPEC-CM-002-B-Dragon-Agent.md) | Dragon Agent | Dragon Prevails → plain text; Dragon Slain gets context summary |
| [SPEC-CM-002-C](SPEC-CM-002-C-Guardian-Agent.md) | Guardian Agent | Block → plain text; Approve/Conditional get context summaries |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-17 | Chris Barlow | Initial specification |
