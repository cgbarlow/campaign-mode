# SPEC-CM-010-A: Phase 3 Party Engagement

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-010-A |
| **Parent ADR** | [ADR-CM-017](../2_adrs/ADR-CM-017-Proactive-Party-Engagement.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-16 |

---

## Overview

This specification defines how animal agents proactively engage during Phase 3 (Campaign Execution). It covers four mechanisms: a recommended first advisor at Phase 3 entry, the Next Perspective protocol for inter-animal handoffs, proactive trigger detection per archetype, and Party Assignments mapping success criteria to animal advisors.

Together these mechanisms transform the advisory council from passive tools into an active team that guides the user through the campaign.

---

## 1. Recommended First Advisor

When Gandalf transitions to Phase 3 (after quest framing and optional character setup), Gandalf analyses the quest characteristics and recommends which animal advisor to consult first.

### Selection Criteria

| Quest Characteristic | Recommended Advisor | Reason |
|---------------------|-------------------|--------|
| High risk or uncertainty | Cat | Risk assessment should precede action |
| Tight timeline or complex sequencing | Owl | Structure and planning before execution |
| Unclear direction or competing priorities | Bear | Vision and direction to focus effort |
| Low motivation or daunting scope | Puppy | Enthusiasm and opportunity-finding to build momentum |
| Resource constraints or dependencies | Rabbit | Resource mapping before commitment |
| Multi-stakeholder or team alignment needed | Wolf | Cohesion and buy-in before divergent work |

Gandalf evaluates the quest narrative, success criteria, and anticipated dragon to select the most relevant advisor. If multiple characteristics are present, Gandalf uses judgement to select the most pressing one.

### Phase 3 Entry Options

Gandalf replaces the generic Phase 3 transition with a recommended first advisor. The `AskUserQuestion` options are:

1. **Consult {recommended advisor} first** — with a one-line reason tied to the quest (e.g., "Your quest has significant unknowns — the Cat can map the risks before you begin")
2. **Begin working** — with trigger phrases planted for mid-campaign transitions ("When you're ready for a checkpoint, say 'I'm ready for a checkpoint'")
3. **Review quest summary** — show the quest definition, success criteria, and campaign mode
4. **Consult a different advisor** — the user wants a different animal perspective first

If the user selects "Consult a different advisor", present the full animal selection menu (with profile names if applicable).

---

## 2. Next Perspective Protocol

After every Phase 3 animal consultation, the animal uses `AskUserQuestion` to suggest the next perspective. This creates continuity between consultations rather than leaving the user alone after each conversation.

### AskUserQuestion Options

At the end of every Phase 3 consultation, the animal presents:

1. **Consult {suggested next animal}** — with a one-line reason based on the conversation (e.g., "We've identified three risks — the Owl can help structure a plan around them")
2. **Consult a different advisor** — the user wants a perspective not suggested
3. **Continue working** — the user is ready to work on their own
4. **Request a checkpoint** — the user wants a Guardian evaluation
5. **Consult Gandalf** — the user wants strategic counsel from the mentor

### Archetype Complement Fallback Table

Animals adapt their suggestion to the conversation content. When conversation context does not clearly indicate a next perspective, use this fallback table:

| Animal | Default Suggestion | Reason |
|--------|-------------------|--------|
| Bear | Cat or Owl | Direction set — assess risks or structure the path |
| Cat | Owl or Rabbit | Risks mapped — plan around them or check resources |
| Owl | Bear or Rabbit | Structure ready — validate direction or identify needs |
| Puppy | Cat or Wolf | Opportunities found — stress-test or check alignment |
| Rabbit | Owl or Wolf | Resources mapped — schedule work or ensure buy-in |
| Wolf | Bear or Puppy | Alignment checked — revisit direction or build momentum |

The table is a fallback, not a script. Animals should adapt based on what was actually discussed. Use profile names when profiles are assigned.

---

## 3. Proactive Engagement Triggers

Each animal archetype has trigger signals — topics or patterns in conversation that indicate another archetype's perspective is needed. Animals use these triggers to make informed Next Perspective suggestions and to proactively address cross-archetype concerns.

### Per-Archetype Trigger Signals

| Archetype | Trigger Signals (detect in conversation) |
|-----------|----------------------------------------|
| **Bear** | Direction unclear, competing priorities, "what should we focus on?", vision drift |
| **Cat** | Risks mentioned, unknowns identified, "what could go wrong?", scope concerns, assumptions surfaced |
| **Owl** | Timeline discussed, sequencing questions, "how long?", process gaps, scheduling concerns |
| **Puppy** | Low energy, discouragement, missed opportunities, "this is hard", scope for enthusiasm |
| **Rabbit** | Resource constraints, dependency questions, "who do we need?", tool/skill gaps, budget concerns |
| **Wolf** | Team misalignment, stakeholder friction, "they don't agree", collaboration gaps, buy-in issues |

### Trigger Response Protocol

1. **If you detect YOUR archetype's trigger** — address it directly as part of your response. This is your core strength.
2. **If you detect ANOTHER animal's trigger** — mention the observation briefly in your response ("I notice there are resource questions here that the Rabbit could help with") and prioritise that animal in your Next Perspective suggestion.
3. **Multiple triggers detected** — prioritise the most urgent or foundational trigger in your Next Perspective suggestion. Use judgement.

---

## 4. Party Assignments

Party Assignments map each success criterion from the quest to a primary and secondary animal advisor. This creates a structured relationship between the quest's goals and the advisory council's strengths.

### quest.md Format

Gandalf writes the Party Assignments table to `.campaign/quest.md` during Phase 1 (Quest Definition), between the Anticipated Dragon and Progress Log sections:

```markdown
## Party Assignments

| Criterion | Primary Advisor | Secondary Advisor |
|-----------|----------------|-------------------|
| {criterion 1} | {animal} ({archetype reason}) | {animal} ({archetype reason}) |
| {criterion 2} | {animal} ({archetype reason}) | {animal} ({archetype reason}) |
```

### Assignment Principles

- **Primary advisor** — The animal whose core archetype is most directly relevant to the criterion
- **Secondary advisor** — A complementary perspective that strengthens the primary assessment
- Use profile names if profiles are assigned; include archetype in parentheses
- Gandalf writes assignments based on archetype-criterion fit, not fixed rules

### Archetype-Criterion Mapping Guidance

| Criterion Type | Likely Primary | Likely Secondary |
|---------------|---------------|-----------------|
| Deliverable quality / output | Owl | Cat |
| Risk mitigation / safety | Cat | Owl |
| Vision / direction / strategy | Bear | Wolf |
| Team alignment / stakeholder buy-in | Wolf | Bear |
| Resource acquisition / dependencies | Rabbit | Owl |
| Motivation / engagement / momentum | Puppy | Wolf |
| Transformation / learning (Grow mode) | Bear | Puppy |

This is guidance, not a fixed mapping. Gandalf adapts based on the specific quest.

### How Animals Use Party Assignments

Animals read the Party Assignments table from quest.md (as part of their Campaign Awareness step). When progress is made on an assigned criterion, the animal suggests the primary advisor for the next unaddressed criterion in their Next Perspective options.

---

## 5. Context Window Impact

The animal campaign extension file grows from ~40 lines to ~100-120 lines with the addition of three new sections (Next Perspective, Proactive Engagement, Criterion Progress Awareness).

### Updated Size Estimates

| Content | Previous Size | New Size | Delta |
|---------|--------------|----------|-------|
| Animal Campaign Extensions | ~40 lines | ~100-120 lines | +60-80 lines |

| Command | Previous Total | New Total | Delta |
|---------|---------------|-----------|-------|
| `start-quest.md` | ~480 lines | ~540-560 lines | +60-80 |
| `council.md` | ~480 lines | ~540-560 lines | +60-80 |
| `continue-quest.md` | ~950 lines | ~1010-1030 lines | +60-80 |

Worst case (`continue-quest.md`): ~1030 lines. The increase is proportionate to the capability gained — three new mid-phase engagement mechanisms for ~80 additional lines.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-008-A](SPEC-CM-008-A-Animal-Campaign-Extensions.md) | Animal Campaign Extensions | Base extension file that this spec extends |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Phase 3 definition and transition protocol |
| [SPEC-CM-002-A](SPEC-CM-002-A-Gandalf-Agent.md) | Gandalf Agent | Gandalf's Phase 1 and Phase 3 transition behaviour |
| [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | Profile name usage in Next Perspective suggestions |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-16 | Chris Barlow | Initial specification |
