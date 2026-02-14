# SPEC-CM-007-A: Plugin Structure

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-007-A |
| **Parent ADR** | [ADR-CM-007](../2_adrs/ADR-CM-007-Plugin-Based-Distribution.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the plugin manifest, directory layout, and installation methods for distributing Campaign Mode as a Claude Code plugin. The plugin packaging supplements (not replaces) the existing clone-and-copy distribution path.

---

## Plugin Manifest

The plugin manifest lives at `.claude-plugin/plugin.json` in the repository root:

```json
{
  "name": "campaign-mode",
  "description": "Quest-based extension for AI-assisted work. Three NPC agents (Gandalf, Dragon, Guardian) provide mentorship, adversarial testing, and quality gates for structured campaigns.",
  "version": "1.0.0",
  "author": "Chris Barlow"
}
```

Claude Code auto-discovers skills from the plugin's `skills/` directory and commands from `commands/`. No explicit registration is required in the manifest.

---

## Directory Layout

### Plugin Distribution Structure

```
campaign-mode/
├── .claude-plugin/
│   └── plugin.json                     # Plugin manifest (required)
├── skills/                             # Plugin skills (auto-discovered)
│   ├── gandalf-agent/
│   │   └── SKILL.md
│   ├── dragon-agent/
│   │   └── SKILL.md
│   └── guardian-agent/
│       └── SKILL.md
├── commands/                           # Plugin commands (auto-discovered)
│   ├── campaign-setup.md              # /campaign-setup slash command
│   ├── start-quest.md                 # /start-quest slash command
│   └── continue-quest.md             # /continue-quest slash command
├── CLAUDE.md                           # Campaign guidelines (loaded per session)
└── README.md
```

### Clone Distribution Structure (Unchanged)

```
campaign-mode/
├── .claude/
│   └── skills/                         # Claude Code auto-discovery directory
│       ├── gandalf-agent/
│       │   └── SKILL.md
│       ├── dragon-agent/
│       │   └── SKILL.md
│       └── guardian-agent/
│           └── SKILL.md
├── skills/                             # Canonical skill definitions
│   ├── gandalf-agent/
│   │   └── SKILL.md
│   ├── dragon-agent/
│   │   └── SKILL.md
│   └── guardian-agent/
│       └── SKILL.md
├── CLAUDE.md                           # Campaign guidelines (loaded per session)
└── README.md
```

### How Each Path Discovers Skills

| Distribution | Skills Directory | Discovery Mechanism |
|-------------|-----------------|---------------------|
| Plugin install | `skills/` | Plugin infrastructure auto-discovers `skills/*/SKILL.md` |
| Clone repo | `.claude/skills/` | Claude Code auto-discovers `.claude/skills/*/SKILL.md` |

Both paths reference the same canonical `skills/` files. The `.claude/skills/` copies exist only for clone-path auto-discovery.

---

## Installation Methods

### Method 1: Plugin Install (Primary)

Install from the Claude Code marketplace:

```
/install campaign-mode
```

This installs the plugin, making skills and commands available immediately. CLAUDE.md is loaded per session. Run `/campaign-setup` to copy guidelines to your project.

### Method 2: Clone Repository (Fallback)

```bash
git clone https://github.com/cgbarlow/campaign-mode.git
cd campaign-mode
# Skills auto-discovered via .claude/skills/
# CLAUDE.md loaded per session from repo root
```

### Method 3: Copy to Existing Project

```bash
cp -r campaign-mode/.claude/skills/ your-project/.claude/skills/
cp campaign-mode/CLAUDE.md your-project/CLAUDE.md
```

### Method 4: Personal Skills (All Projects)

```bash
cp -r campaign-mode/.claude/skills/ ~/.claude/skills/
```

Note: Personal skills do not include CLAUDE.md or commands. Use the plugin install for the full experience.

---

## Plugin vs Clone Feature Comparison

| Feature | Plugin Install | Clone Repo |
|---------|---------------|------------|
| Skill auto-discovery | Yes (plugin infrastructure) | Yes (.claude/skills/) |
| CLAUDE.md per session | Yes | Yes |
| `/campaign-setup`, `/start-quest`, `/continue-quest` commands | Yes | No |
| Marketplace updates | Yes | Manual (git pull) |
| Marketplace discoverability | Yes | No |
| Contribution workflow | No (install is read-only) | Yes (full repo access) |

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-001-A](SPEC-CM-001-A-Skill-Architecture.md) | Campaign Mode Skill Architecture | Defines skill file structure used by both paths |
| [SPEC-CM-004-A](SPEC-CM-004-A-Skill-File-Structure.md) | Skill File Structure and Conventions | Detailed skill authoring conventions |
| [SPEC-CM-007-B](SPEC-CM-007-B-Campaign-Guidelines.md) | Campaign Guidelines | CLAUDE.md content and `/campaign-setup` command |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Added `/start-quest` and `/continue-quest` commands to plugin structure and feature comparison |
