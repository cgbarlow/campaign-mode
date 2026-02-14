# SPEC-CM-007-C: Plugin Path Resolution

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-007-C |
| **Parent ADR** | [ADR-CM-012](../2_adrs/ADR-CM-012-Plugin-Desktop-Compatibility.md) |
| **Version** | 1.2 |
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

Claude Code supports injecting shell command output into command prompts at invocation time:

```
!`shell-command`
```

The shell command is executed when the command is invoked, and its output replaces the directive in the prompt.

### Two-Phase Injection Pattern (v1.2)

The original approach used `!`cat`` to inject file contents directly. However, Claude Code's sandbox blocks `cat` from reading files outside the working directory, causing silent failures for plugin installations (see [ADR-CM-015](../2_adrs/ADR-CM-015-Plugin-Injection-Sandbox-Fix.md)).

The current approach uses a two-phase pattern:

1. **Phase 1 (invocation time):** `!`echo`` injects the resolved absolute file path
2. **Phase 2 (runtime):** The agent uses the Read tool to load file contents from the resolved path

```markdown
# Command Title

[Command instructions reference "the skill definition loaded from
the Injected Context paths below" rather than file paths]

---

## Injected Context

The following files contain essential context for this command. Their absolute
paths are resolved below. **Before proceeding with Step 1, use the Read tool
to load every file listed in this section.** Read them in parallel if possible.
Do not skip any.

If any path below is empty or shows an error, the plugin root could not be
resolved. Fall back to the Campaign Conventions already embedded in NPC skill
definitions. Inform the user that full context loading failed and suggest
running `/campaign-setup` to copy guidelines to the project root.

- Gandalf Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
```

### Fallback Behaviour

If path resolution fails (empty output or error), the agent should:

1. Fall back to Campaign Conventions embedded in NPC SKILL.md files (added in SPEC-CM-007-D)
2. Inform the user that full context loading failed
3. Suggest running `/campaign-setup` to copy guidelines to the project root

---

## Injection Points

### `start-quest.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |
| Animal extensions | `!`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`` |

**Command text change:** References updated to "loaded from the Injected Context paths below". CLAUDE.md injected for campaign conventions (v0.2.6). Animal extensions injected (v0.2.7).

### `continue-quest.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |
| Dragon skill | `!`echo ${CLAUDE_PLUGIN_ROOT}/skills/dragon-agent/SKILL.md`` |
| Guardian skill | `!`echo ${CLAUDE_PLUGIN_ROOT}/skills/guardian-agent/SKILL.md`` |
| Animal extensions | `!`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`` |

**Command text change:** All path references replaced with "loaded from the Injected Context paths below". All three NPC skills injected because the user's choice at runtime determines which agent is invoked. CLAUDE.md injected (v0.2.6). Animal extensions injected (v0.2.7).

### `council.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |
| Gandalf skill | `!`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`` |
| Animal extensions | `!`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`` |

**Command text change:** Step 7 transition references "loaded from the Injected Context paths below". CLAUDE.md injected (v0.2.6). Animal extensions injected (v0.2.7).

### `campaign-setup.md`

| What | Injection |
|------|-----------|
| CLAUDE.md | `!`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` |

**Command text change:** Step 2 references "loaded from the Injected Context path below" instead of "provided at the end of this command".

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
| 1.2 | 2026-02-14 | Chris Barlow | Replaced `!cat` with `!echo` + Read tool two-phase pattern (ADR-CM-015). Updated all injection point tables. Added fallback section. Updated injection points to include animal extensions. |
