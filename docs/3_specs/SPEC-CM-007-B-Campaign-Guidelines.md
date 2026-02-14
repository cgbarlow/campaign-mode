# SPEC-CM-007-B: Campaign Guidelines

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-007-B |
| **Parent ADR** | [ADR-CM-007](../2_adrs/ADR-CM-007-Plugin-Based-Distribution.md) |
| **Version** | 1.2 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the content and structure of the CLAUDE.md campaign guidelines file and the `/campaign-setup` slash command that copies it to user projects. CLAUDE.md establishes cross-cutting campaign conventions loaded every session, complementing the per-invocation NPC behaviour defined in SKILL.md files.

---

## CLAUDE.md Content Specification

### Design Principles

1. **Convention-focused, not behaviour-focused** — CLAUDE.md establishes rules and conventions. Individual NPC behaviour lives in SKILL.md files.
2. **Concise** — Target under 120 lines. Every line costs context window budget.
3. **Non-duplicative** — Does not repeat what SKILL.md files already define (interaction patterns, mode-agent matrices, detailed isolation protocols).
4. **Cross-cutting** — Covers conventions that apply across all NPCs and sessions.

### Required Sections

| # | Section | Purpose | Approximate Lines |
|---|---------|---------|-------------------|
| 1 | Campaign Mode | Brief context — what this is, where it comes from | 5-8 |
| 2 | Agent Identity | Adopt full NPC identity from SKILL.md, don't blend | 5-8 |
| 3 | Core Archetype Constraints | Animal core behaviours non-negotiable, flex tunable | 8-12 |
| 4 | Context Isolation | Three levels (advisory/independent/maximum), what each NPC receives | 10-15 |
| 5 | Campaign Lifecycle | 6-phase flow overview | 8-10 |
| 6 | Campaign Mode Selection | Grow/Ship/Grow & Ship summary, mode persists | 5-8 |
| 7 | Profile Rules | .campaign/profiles/, core vs flex, NPC skins | 5-8 |
| 8 | File Conventions | .campaign/, skills/, commands/ purpose | 5-8 |
| 9 | User as Protagonist | User drives, agents serve | 5-8 |

### Intentionally Excluded Content

The following content lives in SKILL.md files and must NOT be duplicated in CLAUDE.md:

- Individual NPC interaction patterns
- Mode-agent matrices (detailed per-NPC mode tuning)
- Detailed isolation protocols (what exactly Dragon receives vs Guardian)
- Profile format specifications
- Campaign lifecycle triggers and transitions

---

## `/campaign-setup` Command Specification

### Frontmatter

```yaml
---
description: Set up Campaign Mode in your project — copy guidelines and create .campaign/ directory
allowed-tools: [Read, Write, Bash, Glob]
---
```

### Command Actions

1. **Copy CLAUDE.md guidelines** to user's project root
   - If no existing CLAUDE.md: copy directly
   - If existing CLAUDE.md: ask user to choose: append, replace, or skip
2. **Create `.campaign/profiles/` directory** if it doesn't exist
3. **Confirm setup** and suggest `/start-quest` to begin a campaign

### User Interaction Flow

```
User: /campaign-setup

Agent: [Checks for existing CLAUDE.md]

If no CLAUDE.md:
  → Copies guidelines to project root
  → Creates .campaign/profiles/
  → "Campaign Mode is set up. Run /start-quest to begin a quest."

If CLAUDE.md exists:
  → "Found existing CLAUDE.md. How should I add campaign guidelines?"
  → Options: Append | Replace | Skip
  → Proceeds based on user choice
  → Creates .campaign/profiles/ if needed
  → "Campaign Mode is set up. Run /start-quest to begin a quest."
```

---

## Loading Behaviour

### Plugin Users

CLAUDE.md is included in the plugin root but is **not** auto-loaded by Claude Code when the plugin is installed. Plugin CLAUDE.md files are not automatically injected into sessions — only CLAUDE.md files in the user's project root are loaded per session.

To ensure conventions are available, Campaign Mode uses two mechanisms:
- **Commands** (`/start-quest`, `/continue-quest`, `/council`) inject CLAUDE.md via `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` at invocation time (see [SPEC-CM-007-D](SPEC-CM-007-D-Plugin-Guidelines-Injection.md))
- **Direct skills** (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) include a condensed "Campaign Conventions" subset directly in their SKILL.md files
- **`/campaign-setup`** copies CLAUDE.md to the user's project root, ensuring per-session loading for all subsequent sessions

### Clone Users

CLAUDE.md lives at the repository root. Claude Code loads it automatically when working within the cloned repo directory.

### Copy Users

Users who copy skills to their project should also run `/campaign-setup` (plugin users) or manually copy CLAUDE.md to their project root to get per-session guidelines.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-007-A](SPEC-CM-007-A-Plugin-Structure.md) | Plugin Structure | Defines where CLAUDE.md lives in the plugin |
| [SPEC-CM-003-A](SPEC-CM-003-A-Context-Isolation-Protocol.md) | Context Isolation Protocol | CLAUDE.md reinforces isolation conventions defined here |
| [SPEC-CM-005-A](SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | CLAUDE.md summarises mode selection defined here |
| [SPEC-CM-006-B](SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | `/campaign-setup` creates the `.campaign/` directory defined here |

---

## Quest Entry Commands

Two additional commands complement `/campaign-setup` for quest lifecycle management:

| Command | Purpose |
|---------|---------|
| `/start-quest` | Begin a new quest. Checks for active campaigns, then delegates to Gandalf for Phase 1 quest framing. |
| `/continue-quest` | Re-enter an active campaign. Reads `.campaign/quest.md` to detect campaign state, then offers context-aware next-step options via `AskUserQuestion`. |

Both commands follow the proactive elicitation pattern (ADR-CM-008): natural-language options, no slash command references in user-facing text. See [ADR-CM-009](../2_adrs/ADR-CM-009-Quest-Entry-Commands.md) for the decision record.

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Added `/start-quest` and `/continue-quest` documentation, updated `/gandalf-agent` references to `/start-quest` |
| 1.2 | 2026-02-14 | Chris Barlow | Corrected Plugin Users section: CLAUDE.md is NOT auto-loaded by plugin infrastructure. Documented hybrid injection approach (SPEC-CM-007-D). |
