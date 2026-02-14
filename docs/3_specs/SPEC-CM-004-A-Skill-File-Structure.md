# SPEC-CM-004-A: Skill File Structure and Conventions

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-004-A |
| **Parent ADR** | [ADR-CM-004](../adrs/ADR-CM-004-Skill-Based-Implementation.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines the structure and conventions for Campaign Mode SKILL.md files. These conventions ensure consistency with Six Animals skills and compatibility with Claude Code's skill discovery mechanism.

---

## YAML Frontmatter

Every SKILL.md must begin with YAML frontmatter between `---` delimiters:

```yaml
---
name: {agent-name}
description: {Comprehensive one-line description. Must include invocation pattern.}
license: CC-BY-SA-4.0
metadata:
  author: {Author name}
  framework: Campaign Mode
  archetype: {Archetype name}
  role: {Brief role description}
  source: {Source material attribution}
---
```

### Required Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `name` | Skill identifier, used for invocation | `gandalf-agent` |
| `description` | Shown in skill discovery and help. Must include `/name` invocation pattern | `Campaign Mode Mentor NPC. ... Invoke with /gandalf-agent [topic].` |
| `license` | Content license | `CC-BY-SA-4.0` |

### Metadata Fields

| Field | Purpose | Example |
|-------|---------|---------|
| `author` | Primary author | `Chris Barlow` |
| `framework` | Parent framework | `Campaign Mode` |
| `archetype` | Character archetype | `Mentor`, `Adversary`, `Gatekeeper` |
| `role` | Functional role description | `Quest Framer / Strategic Counsel` |
| `source` | Source material attribution | `quest-agent (Quest Definition Framework) + simon-agent (Guide on the Side)` |

### Compatibility with Six Animals

Six Animals skills use these metadata fields that Campaign Mode extends:

| Six Animals Field | Campaign Mode Equivalent |
|-------------------|-------------------------|
| `framework: Six-Animal Model` | `framework: Campaign Mode` |
| `archetype: Visionary/Leader` | `archetype: Mentor` |
| `primary-need: Achievement (nAch)` | `role: Quest Framer / Strategic Counsel` |
| `sdt-focus: Competence` | `source: quest-agent + simon-agent` |

Campaign Mode uses `archetype`, `role`, and `source` instead of McClelland's needs and SDT focus, since NPCs are not modelled on motivation theory.

---

## Body Structure

### Required Sections (in order)

1. **Title** — `# {Agent Name} - The {Archetype}`
2. **Overview** — What this NPC is, its core role, when to use it
3. **Foundation** — The philosophical or pedagogical grounding (equivalent to Six Animals' "Psychological Foundation")
4. **Core Capabilities** — 3-5 capabilities, each with Process, Key Behaviours, and optionally Example Output
5. **Interaction Patterns** — How the NPC engages in different scenarios
6. **Integration with Animals** — How this NPC works with each of the six animal agents
7. **Integration with NPCs** — Relationship to the other two NPCs
8. **Context Isolation** — Statement of isolation level and what the NPC can/cannot access (for Dragon and Guardian)
9. **Usage Guidelines** — When and how to invoke, key mindset

### Progressive Disclosure

Following the Claude Skills Guide principle of progressive disclosure:
- **Overview** should be readable in 30 seconds and tell the user whether this is the right NPC
- **Core Capabilities** provide the "how" for users who invoke the skill
- **Foundation** and **Integration** sections provide depth for users who want to understand the design
- **Context Isolation** is operational guidance for maintaining independence

### Section Depth Guidelines

| Section | Target Length | Priority |
|---------|-------------|----------|
| Overview | 5-10 lines | Essential — this is what Claude reads first |
| Foundation | 15-30 lines | Important — grounds the NPC's behaviour |
| Core Capabilities | 40-80 lines | Essential — defines what the NPC does |
| Interaction Patterns | 20-40 lines | Important — scenario-specific guidance |
| Integration with Animals | 10-20 lines | Useful — table format recommended |
| Integration with NPCs | 5-15 lines | Useful — table format recommended |
| Context Isolation | 5-15 lines | Essential for Dragon/Guardian |
| Usage Guidelines | 5-10 lines | Essential — practical invocation guidance |

---

## Naming Conventions

| Element | Convention | Example |
|---------|-----------|---------|
| Skill name | kebab-case, ends with `-agent` | `gandalf-agent` |
| Directory | matches skill name | `gandalf-agent/` |
| File | Always `SKILL.md` (uppercase) | `SKILL.md` |
| Invocation | `/` + skill name | `/gandalf-agent` |

### Consistency with Six Animals

| Six Animals | Campaign Mode |
|-------------|---------------|
| `bear-agent` | `gandalf-agent` |
| `cat-agent` | `dragon-agent` |
| `simon-agent` | `guardian-agent` |

The `-agent` suffix is consistent across both frameworks.

---

## Cross-Surface Compatibility

Skills should work across all Claude surfaces:

| Surface | How Skills Are Used |
|---------|-------------------|
| **Claude Code (CLI)** | Auto-discovered from `.claude/skills/`. Invoked via `/skill-name`. |
| **Claude.ai** | Copy SKILL.md content into project knowledge or system prompt. |
| **Claude API** | Include SKILL.md content in the system prompt. |

To ensure cross-surface compatibility:
- Do not rely on Claude Code-specific features (file access, bash commands) in skill instructions
- Write skill instructions that work as standalone behavioural guidance
- Avoid references to specific tool names or features that may not exist on all surfaces

---

## Quality Checklist

Before publishing a Campaign Mode skill:

- [ ] YAML frontmatter has all required fields
- [ ] `description` includes invocation pattern
- [ ] All required sections are present in correct order
- [ ] File exists in both `skills/` and `.claude/skills/` locations
- [ ] Skill name is kebab-case and ends with `-agent`
- [ ] Integration sections reference all six animals and both other NPCs
- [ ] Context isolation section is present (for Dragon and Guardian)
- [ ] No cross-surface incompatibilities (no tool-specific references)
- [ ] License is CC-BY-SA-4.0

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-001-A](SPEC-CM-001-A-Skill-Architecture.md) | Skill Architecture | Directory structure and installation |
| [SPEC-CM-002-A](SPEC-CM-002-A-Gandalf-Agent.md) | Gandalf Agent | Gandalf skill design |
| [SPEC-CM-002-B](SPEC-CM-002-B-Dragon-Agent.md) | Dragon Agent | Dragon skill design |
| [SPEC-CM-002-C](SPEC-CM-002-C-Guardian-Agent.md) | Guardian Agent | Guardian skill design |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
