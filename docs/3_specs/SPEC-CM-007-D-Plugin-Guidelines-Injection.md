# SPEC-CM-007-D: Plugin Guidelines Injection

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-007-D |
| **Parent ADR** | [ADR-CM-013](../2_adrs/ADR-CM-013-Plugin-Guidelines-Parity.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines how CLAUDE.md campaign conventions are made available across all NPC invocation paths in the Campaign Mode plugin. It extends SPEC-CM-007-C (Plugin Path Resolution) to cover CLAUDE.md injection into commands, and defines the condensed "Campaign Conventions" subset added to NPC SKILL.md files for direct skill invocations.

---

## Problem

CLAUDE.md establishes cross-cutting campaign conventions that all NPC agents depend on (agent identity rules, core vs flex framework, lifecycle overview, proactive elicitation, debrief protocol). These conventions are only available when users have copied CLAUDE.md to their project root via `/campaign-setup` or by cloning the repository.

Plugin users who invoke agents without setup operate without these conventions. Two invocation paths need coverage:

| Path | Mechanism | Gap |
|------|-----------|-----|
| **Commands** (`/start-quest`, `/continue-quest`, `/council`) | Plugin command files | CLAUDE.md not injected |
| **Direct skills** (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) | SKILL.md auto-discovery | No dynamic injection available |

---

## Solution

### Path 1: Command Injection

Add `!`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` to the Injected Context section of each command file, following the two-phase pattern established in SPEC-CM-007-C v1.2.

#### Injection Points

| Command | New Injection | Existing Injections |
|---------|---------------|---------------------|
| `start-quest.md` | CLAUDE.md | Gandalf SKILL.md |
| `continue-quest.md` | CLAUDE.md | Gandalf, Dragon, Guardian SKILL.md |
| `council.md` | CLAUDE.md | Gandalf SKILL.md |
| `campaign-setup.md` | *(no change)* | CLAUDE.md (already present) |

The CLAUDE.md injection is placed **before** skill injections in the Injected Context section so that conventions are established before agent-specific behaviour is loaded.

### Path 2: SKILL.md Condensed Subset

Add a "Campaign Conventions" section to each NPC SKILL.md file containing a curated subset of CLAUDE.md conventions. This section is placed after Speaker Identification and before Overview.

The subset covers conventions **not already present** in individual SKILL.md files:

1. **No identity blending** — Do not blend NPC identities; each agent is distinct
2. **Profile name overrides for selection menus** — Check `.campaign/profiles/` and use profile names in agent selection menus
3. **Core vs flex framework** — Core behaviours are non-negotiable; flex behaviours are tunable by profiles and mode
4. **Six-phase lifecycle summary** — Quest Definition, Character Setup, Campaign Execution, Guardian Checkpoint, Dragon Confrontation, Debrief
5. **Progress tracking** — Append to Progress Log in `.campaign/quest.md` when meaningful milestones are achieved
6. **Proactive elicitation meta-rule** — Every phase transition must offer next-step options via `AskUserQuestion`; never reference slash commands in user-facing text
7. **Debrief protocol** — Dragon facilitates transition to Phase 6; Simon receives campaign mode, verdict, and quest summary

#### Condensed Section Content

The following is the canonical "Campaign Conventions" section added to all NPC SKILL.md files:

```markdown
## Campaign Conventions

These conventions apply across all Campaign Mode agents. They complement the agent-specific behaviour defined in this skill file.

**Identity rules:**
- Do not blend NPC identities — each agent is a distinct character with a distinct role
- Do not break character to offer general Claude assistance while acting as an NPC
- If an agent has a profile in `.campaign/profiles/`, always use their assigned name — never their archetype name. This applies to speaker tags, self-references, and when referring to other agents

**Agent selection menus:** When presenting the user with a choice of which agent to consult, check `.campaign/profiles/` first. Use profile names in place of archetype names in all option labels and descriptions. Include the archetype in parentheses so the user knows the underlying role.

**Core vs flex behaviours:** Animal agents have non-negotiable core behaviours (Bear: vision, Cat: risk, etc.) and tunable flex behaviours adjustable by profiles and mode. NPC core roles are similarly fixed: Gandalf mentors without rescuing, Dragon evaluates adversarially but fairly, Guardian gates based on quality.

**Campaign lifecycle:** Campaigns follow six phases — (1) Quest Definition, (2) Character Setup, (3) Campaign Execution, (4) Guardian Checkpoint, (5) Dragon Confrontation, (6) Debrief. An optional Council step can occur before or during a quest.

**Progress tracking:** When `.campaign/quest.md` exists and the campaign is in Phase 3+, append to the Progress Log when meaningful milestones are achieved (user states completion, phase transitions, success criteria addressed). Format: `- **Progress** — {description} ({date})`. Do this silently.

**Proactive elicitation:** At every phase transition, offer next-step options via `AskUserQuestion`. The user should never need to remember slash commands. Never reference slash commands (e.g., `/dragon-agent`) in user-facing text — use natural language instead (e.g., "Face the Dragon"). Ending a phase without a next-step question is a bug.

**Debrief protocol:** When the Dragon Confrontation concludes, the Dragon facilitates transition to Phase 6 via `AskUserQuestion`. If selected, Simon is invoked with: campaign mode, Dragon's verdict (Dragon Slain or Dragon Prevails), and quest summary. Debrief depth varies by mode: Grow (full reflection), Ship (brief retrospective), Grow & Ship (balanced).
```

#### Files Modified

The Campaign Conventions section is added to all six NPC SKILL.md files:

| File | Path |
|------|------|
| Gandalf (canonical) | `skills/gandalf-agent/SKILL.md` |
| Gandalf (clone-path) | `.claude/skills/gandalf-agent/SKILL.md` |
| Dragon (canonical) | `skills/dragon-agent/SKILL.md` |
| Dragon (clone-path) | `.claude/skills/dragon-agent/SKILL.md` |
| Guardian (canonical) | `skills/guardian-agent/SKILL.md` |
| Guardian (clone-path) | `.claude/skills/guardian-agent/SKILL.md` |

---

## Context Window Impact

Updated from SPEC-CM-007-C with CLAUDE.md additions:

| Content | Approximate Size |
|---------|-----------------|
| Gandalf SKILL.md | ~310 lines (was ~300, +10 for conventions) |
| Dragon SKILL.md | ~260 lines (was ~250, +10 for conventions) |
| Guardian SKILL.md | ~210 lines (was ~200, +10 for conventions) |
| CLAUDE.md | ~130 lines |

| Command | Total Injected Content |
|---------|----------------------|
| `campaign-setup.md` | ~130 lines (CLAUDE.md only — unchanged) |
| `start-quest.md` | ~440 lines (CLAUDE.md + Gandalf SKILL.md) |
| `council.md` | ~440 lines (CLAUDE.md + Gandalf SKILL.md) |
| `continue-quest.md` | ~910 lines (CLAUDE.md + all three NPC SKILL.md) |

Worst case (`continue-quest.md`): ~910 lines. This is within acceptable limits for command prompts — the CLAUDE.md addition (~130 lines) is a modest increase over the existing ~750-line worst case.

---

## Maintenance

When CLAUDE.md conventions change, the condensed SKILL.md subset should be reviewed. A checklist:

1. Does the changed convention already exist in SKILL.md files? If yes, no subset update needed.
2. Is the changed convention cross-cutting (applies to all NPCs)? If yes, update the subset.
3. Is the changed convention agent-specific? If yes, update only that agent's SKILL.md, not the subset.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-007-B](SPEC-CM-007-B-Campaign-Guidelines.md) | Campaign Guidelines | Defines CLAUDE.md content; corrected re: plugin auto-loading |
| [SPEC-CM-007-C](SPEC-CM-007-C-Plugin-Path-Resolution.md) | Plugin Path Resolution | Establishes injection pattern extended here |
| [SPEC-CM-007-A](SPEC-CM-007-A-Plugin-Structure.md) | Plugin Structure | Defines plugin layout including command and skill directories |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Updated injection syntax from `!cat` to `!echo` per ADR-CM-015 two-phase pattern |
