# SPEC-CM-001-B: Campaign Lifecycle

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-001-B |
| **Parent ADR** | [ADR-CM-001](../adrs/ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Version** | 1.3 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the six-phase campaign lifecycle — the flow from quest inception through to debrief. Each phase identifies the primary actor (user and/or NPC), triggers, outputs, and transitions.

The user is the **protagonist** throughout — the decision-maker who drives the quest, invokes agents, produces work, and faces NPCs. Agents (both animals and NPCs) serve the user's quest; they do not drive it.

---

## Campaign Flow

```
1. Quest Definition       →  User selects campaign mode; Gandalf frames the challenge
        │
2. Character Setup        →  Animals adopt campaign roles (optional; mode-dependent)
        │
3. Campaign Execution     →  User works the quest with animal support
        │
4. Guardian Checkpoint    →  Guardian evaluates readiness to progress (mode-aware)
        │                     (repeats at key stages)
5. Dragon Confrontation   →  Dragon tests success criteria (mode-aware scope)
        │
6. Debrief                →  Simon provides feedback (depth varies by mode)
```

---

## Phase Definitions

### Phase 1: Quest Definition

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | User + Gandalf (Mentor) |
| **Trigger** | User invokes `/gandalf-agent` to begin a campaign |
| **Activities** | **Campaign mode selection** (Grow / Ship / Grow & Ship); frame the quest narrative; establish success criteria; identify the anticipated dragon (internal obstacle); define what "done" looks like |
| **Outputs** | Campaign mode selection + quest definition (narrative, success criteria, anticipated challenges) |
| **Transition** | Quest definition complete → Phase 2 or Phase 3. Gandalf facilitates the transition through `AskUserQuestion`, offering options to begin working, review the quest summary, or consult an animal advisor. |

**Campaign Mode Selection:** Before framing the quest, Gandalf asks the user to choose their campaign mode. This is the user's first act of agency as protagonist — choosing how they want to approach the campaign. See [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) for how each mode tunes NPC behaviour. The default is Grow & Ship.

Gandalf draws from the Quest Definition Framework (quest-agent source) and the "guide on the side" mentorship philosophy (simon-agent source). The quest is framed as an invitation, not an assignment — the user should feel agency in accepting and shaping the quest.

**Mode effects:** In Grow mode, Gandalf emphasises reflective questions and transformation criteria. In Ship mode, Gandalf focuses on clear deliverable objectives. In Grow & Ship mode, both dimensions are balanced.

### Phase 2: Character Setup (Optional, Mode-Dependent)

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | User (facilitated by Gandalf) |
| **Trigger** | Quest definition complete, mode allows (Grow: encouraged, Ship: skipped, Grow & Ship: optional) |
| **Activities** | User selects profile depth (vanilla/flavour/modifier), chooses theme (neutral/fantasy/custom), assigns profiles to selected animals, optionally skins NPCs. Gandalf facilitates and enforces archetype compatibility. |
| **Outputs** | Character profile files in `.campaign/profiles/`. Each profile defines tone, voice, and optionally behavioural modifiers. |
| **Transition** | Setup complete → Phase 3. Gandalf facilitates the transition through `AskUserQuestion` (same options as Phase 1 transition). |

This phase is **optional** and user-driven. Gandalf facilitates the process, offering depth selection, theme selection, and per-animal profile assignment. Users can profile any subset of animals — the rest stay vanilla (default archetypes).

**Profile Depths:**
- **Vanilla** — No profile. Animal uses its default archetype.
- **Flavour** — Narrative only. Changes tone, voice, vocabulary, and metaphors. Core behaviours unchanged.
- **Modifier** — Narrative + behavioural tuning. Tunes flex behaviours within archetype bounds. Core behaviours unchanged.

**Archetype Guardrails:** Core animal behaviours are non-negotiable. Gandalf warns AND blocks incompatible profiles. A Bear without vision isn't Bear. See [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md) for the core vs flex behaviour matrix.

**NPC Skins:** NPCs (Gandalf, Dragon, Guardian) can optionally receive light thematic skins — changing presentation, vocabulary, and display name without altering core NPC behaviour.

**Mode effects:** In Grow mode, character setup is encouraged as it adds reflective depth. In Ship mode, this phase is skipped — it is not productivity-relevant. In Grow & Ship mode, it is the user's choice.

**Storage:** Profiles are stored as markdown files in `.campaign/profiles/`. See [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) for the directory structure and export protocol.

### Phase 3: Campaign Execution

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | User (with animal support) |
| **Trigger** | Quest defined (Phase 1 complete) |
| **Activities** | The user works through the quest, invoking animal agents for their archetype strengths. Gandalf provides strategic counsel when consulted. |
| **Outputs** | Work product, decisions, progress toward success criteria |
| **Transition** | Key milestone reached → Phase 4; all criteria addressed → Phase 5. The user triggers transitions using natural-language phrases planted during Phase 1 (e.g., "I'm ready for a checkpoint", "I'm ready to face the Dragon"). |

The user drives the work. Animals provide perspectives and support; NPCs operate with isolated context (they cannot see party reasoning).

**Mode effects:** In Grow mode, Gandalf may prompt reflective pauses. In Ship mode, execution is focused on deliverable progress. In Grow & Ship mode, reflection happens naturally through the work.

### Phase 4: Guardian Checkpoint

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | User invokes Guardian; Guardian evaluates |
| **Trigger** | User reaches a key milestone; user invokes `/guardian-agent` |
| **Activities** | Guardian independently evaluates progress against quality criteria. Reviews work product without access to the user's internal reasoning or party discussions. |
| **Outputs** | Gate decision: Approve (proceed), Block (with feedback), or Conditional Approval (proceed with caveats) |
| **Transition** | Approved → Phase 3 (next stage) or Phase 5; Blocked → Phase 3 (rework). Guardian facilitates the transition through `AskUserQuestion`, offering options appropriate to the gate decision (continue, face Dragon, consult Gandalf, address gaps, or discuss the verdict). |

Guardian checkpoints can repeat multiple times during a campaign. Each checkpoint evaluates the current stage's deliverables against readiness criteria.

**Mode effects:** In Grow mode, the Guardian focuses on ZPD and understanding, more lenient on polish. In Ship mode, the Guardian focuses on deliverable quality with faster progression. In Grow & Ship mode, both dimensions are assessed.

**Context Isolation:** The Guardian operates independently. It receives the work product and campaign mode but not the party's discussion, reasoning, or intermediate decisions. See [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md).

### Phase 5: Dragon Confrontation

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | User invokes Dragon; Dragon evaluates |
| **Trigger** | User believes all success criteria are met; user invokes `/dragon-agent` |
| **Activities** | Dragon adversarially tests whether Gandalf's success criteria have been genuinely met. Stress-tests the work. Challenges assumptions. |
| **Outputs** | Confrontation result: Dragon Slain (criteria met), Dragon Prevails (criteria not met, with specific feedback) |
| **Transition** | Dragon Slain → Phase 6; Dragon Prevails → Phase 3 (rework). Dragon facilitates the transition through `AskUserQuestion`, offering options appropriate to the verdict (begin debrief, celebrate, return to quest, consult Gandalf, or request Guardian checkpoint). |

The Dragon is the culminating test. It operates adversarially but fairly — rigorous but not destructive.

**Mode effects:** In Grow mode, the Dragon evaluates both transformation and deliverable criteria — transformation evidence is required for Dragon Slain. In Ship mode, the Dragon evaluates deliverable criteria only. In Grow & Ship mode, both are evaluated but transformation is assessed rather than required.

**Context Isolation:** The Dragon operates with maximum independence. It receives only the success criteria (from Gandalf's quest definition), the campaign mode, and the final work product. It does not see party discussions, Guardian feedback, or intermediate work. See [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md).

### Phase 6: Debrief

| Aspect | Detail |
|--------|--------|
| **Primary Actor** | Simon (Supervisor) + User |
| **Trigger** | Dragon confrontation complete (regardless of outcome) |
| **Activities** | Simon provides feedback on the journey. Analyses role performance, group dynamics, what was learned. Pulls back the curtain on pedagogical dynamics. |
| **Outputs** | Debrief insights, growth reflections, recommendations for future quests |
| **Transition** | Campaign complete; optionally leads to next quest definition (Phase 1). Simon facilitates the transition through `AskUserQuestion`, offering options to begin a new quest or conclude. |

**Mode effects:** In Grow mode, full pedagogical reflection — deep analysis of learning moments, role performance, and personal growth. In Ship mode, brief retrospective focused on process effectiveness and improvement. In Grow & Ship mode, balanced debrief covering both dimensions.

---

## Phase Transition Protocol

Every phase transition is facilitated by the active agent through `AskUserQuestion`. No agent should end a phase with a passive statement — every phase boundary must present the user with structured next-step options.

**Principles:**
- **Proactive, not passive** — Agents offer the next step; they never assume the user knows what to do next
- **Natural language, not commands** — Transition options use plain language ("Face the Dragon", "Consult Gandalf") rather than slash commands (`/dragon-agent`, `/gandalf-agent`)
- **User retains agency** — The user chooses from options; the agent does not advance the campaign autonomously
- **Context isolation preserved** — Transition handoffs respect NPC isolation boundaries. When Gandalf hands off to the Dragon, only success criteria, campaign mode, and work product are passed.

**Transition responsibilities by agent:**

| Agent | Transition Points | Options Offered |
|-------|-------------------|-----------------|
| **Gandalf** | After quest framing/character setup | Begin working, Review quest summary, Consult an animal advisor |
| **Gandalf** | Before Dragon Confrontation | Face the Dragon, Address gaps first, Request a Guardian checkpoint first |
| **Guardian** | After Approve | Continue the quest, Face the Dragon, Consult Gandalf |
| **Guardian** | After Block | Address the gaps, Consult Gandalf, Discuss the verdict |
| **Guardian** | After Conditional Approval | Continue the quest, Address conditions first, Consult Gandalf |
| **Dragon** | After Dragon Slain | Begin the debrief, Celebrate first |
| **Dragon** | After Dragon Prevails | Return to the quest, Consult Gandalf, Request a Guardian checkpoint |

**Flow drop rule:** Ending a phase without a next-step `AskUserQuestion` is a flow drop and a bug.

---

## Flow Variations

### Minimal Campaign (No Checkpoints)
```
Quest Definition → Campaign Execution → Dragon Confrontation → Debrief
```

### Multi-Checkpoint Campaign
```
Quest Definition → Execution → Checkpoint → Execution → Checkpoint → Dragon → Debrief
```

### Failed Dragon (Iteration)
```
... → Dragon Confrontation (fails) → Execution (rework) → Dragon Confrontation (succeeds) → Debrief
```

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-001-A](SPEC-CM-001-A-Skill-Architecture.md) | Skill Architecture | Structure of the skills that participate in this lifecycle |
| [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md) | Context Isolation Protocol | How NPC independence is maintained during phases 4 and 5 |
| [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | How mode selection tunes behaviour across all phases |
| [SPEC-CM-006-A](SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format | Profile file structure, depth levels, themes, and core vs flex behaviours |
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | Where profile files are stored and export protocol |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Added mode selection to Phase 1, mode annotations to all phases, user-as-protagonist framing |
| 1.2 | 2026-02-14 | Chris Barlow | Replaced Phase 2 placeholder with full character generation spec, added SPEC-CM-006-A and SPEC-CM-006-B references |
| 1.3 | 2026-02-14 | Chris Barlow | Added Phase Transition Protocol, updated all phase Transition rows with proactive elicitation via `AskUserQuestion` (ADR-CM-008) |
