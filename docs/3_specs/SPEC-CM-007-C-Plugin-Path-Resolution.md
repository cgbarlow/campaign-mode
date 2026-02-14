# SPEC-CM-007-C: Plugin Path Resolution

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-007-C |
| **Parent ADR** | [ADR-CM-012](../2_adrs/ADR-CM-012-Plugin-Desktop-Compatibility.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines how Campaign Mode plugin commands resolve references to skill files and CLAUDE.md content using Claude Code's dynamic context injection syntax. It replaces runtime path resolution (which fails in Claude Desktop) with invocation-time content injection.

---

## Problem

Plugin commands contain instructions that reference files by relative path:

| Command | Problematic Reference |
|---------|----------------------|
| `start-quest.md` | "loading the skill from `skills/gandalf-agent/SKILL.md`" |
| `continue-quest.md` | "load their skill from `skills/{agent}/SKILL.md`" |
| `council.md` | "loading the skill from `skills/gandalf-agent/SKILL.md`" |
| `campaign-setup.md` | "Read the Campaign Mode CLAUDE.md from this plugin's root directory" |

These paths resolve against the user's project directory, not the plugin cache. In Claude Desktop (and Claude Code when the user is in their own project), the files are not found and commands fail silently.

---

## Solution: Dynamic Context Injection

### Injection Syntax

Claude Code supports injecting external content into command prompts at invocation time:

```
!`shell-command`
```

The shell command is executed when the command is invoked, and its output replaces the directive in the prompt. Combined with `${CLAUDE_PLUGIN_ROOT}`:

```
!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
```

This injects the full skill definition into the command prompt, eliminating the need for the agent to locate and read the file at runtime.

### Injection Pattern

Each command file appends injection blocks at the end of the file, after all behavioural instructions. The command text references these injected definitions rather than file paths.

```markdown
# Command Title

[Command instructions reference "the skill definition provided below"
rather than file paths]

---

## Injected Context

The following content is injected at invocation time and should not be
modified directly. Edit the source files instead.

### Gandalf Skill Definition

!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
```

---

## Injection Points

### `start-quest.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |

**Command text change:** Step 2 references "the Gandalf skill definition provided at the end of this command" instead of a file path. CLAUDE.md injected for campaign conventions (v0.2.6).

### `continue-quest.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |
| Dragon skill | `!`cat ${CLAUDE_PLUGIN_ROOT}/skills/dragon-agent/SKILL.md`` |
| Guardian skill | `!`cat ${CLAUDE_PLUGIN_ROOT}/skills/guardian-agent/SKILL.md`` |

**Command text change:** All path references replaced with "the skill definitions provided at the end of this command". All three NPC skills are injected because the user's choice at runtime determines which agent is invoked. CLAUDE.md injected for campaign conventions (v0.2.6).

### `council.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |

**Command text change:** Step 7 transition references "the Gandalf skill definition provided at the end of this command" instead of a file path. CLAUDE.md injected for campaign conventions (v0.2.6).

### `campaign-setup.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |

**Command text change:** Step 2 references "the Campaign Mode CLAUDE.md content provided at the end of this command" instead of "this plugin's root directory".

---

## Context Window Impact

Each injection adds to the command's prompt size:

| Content | Approximate Size |
|---------|-----------------|
| CLAUDE.md | ~130 lines |
| Gandalf SKILL.md | ~310 lines |
| Dragon SKILL.md | ~260 lines |
| Guardian SKILL.md | ~210 lines |

| Command | Total Injected Content |
|---------|----------------------|
| `campaign-setup.md` | ~130 lines (CLAUDE.md only) |
| `start-quest.md` | ~440 lines (CLAUDE.md + Gandalf) |
| `council.md` | ~440 lines (CLAUDE.md + Gandalf) |
| `continue-quest.md` | ~910 lines (CLAUDE.md + all three NPCs) |

Worst case (`continue-quest.md` with CLAUDE.md and all three NPC skills): ~910 additional lines. This is within acceptable limits for command prompts and is offset by eliminating failed file reads and retry attempts.

---

## Clone-Path Impact

None. Clone-path users:

- Do not use `commands/` (plugin-only feature per SPEC-CM-007-A)
- Invoke skills directly via `.claude/skills/` auto-discovery
- Load CLAUDE.md from the repository root

No changes are made to `.claude/skills/`, `skills/`, or CLAUDE.md files.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-007-A](SPEC-CM-007-A-Plugin-Structure.md) | Plugin Structure | Defines command directory and plugin layout |
| [SPEC-CM-007-B](SPEC-CM-007-B-Campaign-Guidelines.md) | Campaign Guidelines | Defines CLAUDE.md content and `/campaign-setup` command |
| [SPEC-CM-007-D](SPEC-CM-007-D-Plugin-Guidelines-Injection.md) | Plugin Guidelines Injection | Extends this spec with CLAUDE.md injection and SKILL.md subset |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Added CLAUDE.md as injection point for start-quest, continue-quest, council. Updated context window impact table. Added SPEC-CM-007-D reference. |
