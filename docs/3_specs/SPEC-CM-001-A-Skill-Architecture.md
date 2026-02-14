# SPEC-CM-001-A: Campaign Mode Skill Architecture

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-001-A |
| **Parent ADR** | [ADR-CM-001](../adrs/ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the directory structure, file layout, and installation conventions for Campaign Mode skills. The architecture follows the same patterns established by Six Animals to ensure consistency and ease of adoption.

---

## Directory Structure

Campaign Mode uses a dual-location convention for skill files:

```
campaign-mode/
├── .claude/
│   └── skills/                    # Auto-discovery directory (clone path)
│       ├── gandalf-agent/
│       │   └── SKILL.md
│       ├── dragon-agent/
│       │   └── SKILL.md
│       └── guardian-agent/
│           └── SKILL.md
├── .claude-plugin/
│   └── plugin.json                # Plugin manifest (plugin path)
├── skills/                        # Canonical skill definitions
│   ├── gandalf-agent/
│   │   └── SKILL.md
│   ├── dragon-agent/
│   │   └── SKILL.md
│   └── guardian-agent/
│       └── SKILL.md
├── commands/                      # Slash commands (plugin path)
│   └── campaign-setup.md
├── docs/
│   ├── 2_adrs/                    # Architecture Decision Records
│   │   ├── reference/             # ADR framework reference docs
│   │   ├── ADR-CM-001-*.md
│   │   └── ...
│   ├── 3_specs/                   # Detailed specifications
│   │   ├── SPEC-CM-001-*.md
│   │   └── ...
│   └── north-star.md              # Vision document
├── CLAUDE.md                      # Campaign guidelines (loaded per session)
└── README.md
```

### Dual-Location Convention

Skills exist in two locations:

| Location | Purpose |
|----------|---------|
| `skills/{agent}/SKILL.md` | **Canonical** — the authoritative source file, version-controlled and reviewed |
| `.claude/skills/{agent}/SKILL.md` | **Auto-discovery** — enables Claude Code to automatically detect and offer the skill |

The `.claude/skills/` copy is identical to the canonical copy. When editing, always edit the canonical version and copy to `.claude/skills/`.

### Naming Conventions

| Convention | Rule | Example |
|------------|------|---------|
| Agent directories | kebab-case | `gandalf-agent/` |
| Skill files | Always `SKILL.md` (uppercase) | `skills/gandalf-agent/SKILL.md` |
| ADR files | `ADR-CM-{NNN}-{Title}.md` | `ADR-CM-001-Campaign-Mode-Architecture.md` |
| Spec files | `SPEC-CM-{NNN}-{Letter}-{Title}.md` | `SPEC-CM-001-A-Skill-Architecture.md` |

---

## Skill File Structure

Each SKILL.md follows the Claude Code skill format with YAML frontmatter:

```yaml
---
name: {agent-name}
description: {One-line description. Include invocation pattern.}
license: CC-BY-SA-4.0
metadata:
  author: {Author}
  framework: Campaign Mode
  archetype: {Archetype name}
  role: {NPC role}
---
```

### Required Sections

Every NPC skill must include:

1. **Overview** — What this NPC is, when to invoke it
2. **Core Philosophy / Foundation** — The psychological or pedagogical grounding
3. **Core Capabilities** — What the NPC does (3-5 capabilities with process, behaviours, examples)
4. **Interaction Patterns** — How the NPC engages in different scenarios
5. **Integration with Animals** — How this NPC works with each of the six animal agents
6. **Integration with NPCs** — Relationship to the other two NPCs
7. **Context Isolation** — Statement of independent operation (for Dragon and Guardian)
8. **Usage Guidelines** — When and how to invoke

---

## Installation Methods

### Method 1: Plugin Install (Primary)

Install from the Claude Code marketplace:

```
/install campaign-mode
```

Skills are auto-discovered by the plugin infrastructure. CLAUDE.md guidelines are loaded per session. Run `/campaign-setup` to copy guidelines to your project. See [SPEC-CM-007-A](SPEC-CM-007-A-Plugin-Structure.md) for full plugin structure.

### Method 2: Clone Repository (Project-Level)

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills auto-discovered via .claude/skills/
```

### Method 3: Copy to Existing Project

```bash
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
```

### Method 4: Personal Skills (All Projects)

```bash
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

### Prerequisites

Campaign Mode is designed to complement [Six Animals](https://github.com/SimonMcCallum/six-animals). While NPC skills can function independently, the full campaign experience requires the Six Animals skills to be installed.

---

## Compatibility

| Surface | Supported | Notes |
|---------|-----------|-------|
| Claude Code (CLI) | Yes | Primary target — skills auto-discovered |
| Claude.ai | Yes | Skills can be pasted into project knowledge |
| Claude API | Yes | Skills can be included in system prompts |

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Defines the flow that these skills participate in |
| [SPEC-CM-004-A](SPEC-CM-004-A-Skill-File-Structure.md) | Skill File Structure and Conventions | Detailed skill authoring conventions |
| [SPEC-CM-007-A](SPEC-CM-007-A-Plugin-Structure.md) | Plugin Structure | Plugin manifest, directory layout, plugin installation method |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
