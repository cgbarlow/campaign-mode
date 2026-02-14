# SPEC-CM-008-A: Animal Campaign Extensions

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-CM-008-A |
| **Parent ADR** | [ADR-CM-014](../2_adrs/ADR-CM-014-Animal-Campaign-Extensions.md) |
| **Version** | 1.1 |
| **Status** | Draft |
| **Last Updated** | 2026-02-14 |

---

## Overview

This specification defines how animal agents (Bear, Cat, Owl, Puppy, Rabbit, Wolf) gain campaign awareness when invoked during active Campaign Mode quests. It covers the extension file content and location, injection points per command, the invocation protocol for Skill-invoked animals, and the canonical text for the Six Animals "Context Extensions" stub.

---

## Problem

CLAUDE.md requires all agents to track progress during Phase 3+, but animal agents owned by the Six Animals project have no campaign-specific behaviour. When invoked via the Skill tool from campaign commands, animals receive only their SKILL.md — not CLAUDE.md or quest context.

---

## Extension File

### Location

```
extensions/animal-campaign-context.md
```

### Content

The extension file covers three concerns:

| Concern | Description |
|---------|-------------|
| **Campaign awareness** | Read `quest.md` before responding; ground archetype advice in quest context |
| **Progress tracking** | Same triggers, format, and mechanics as NPC tracking (Read tool, append, Write tool, silently) |
| **Phase transition awareness** | If user signals readiness, acknowledge and suggest next step in natural language |

### Approximate Size

~40 lines of markdown.

---

## Injection Points

The extension file is injected into quest commands using the two-phase `!`echo`` pattern (SPEC-CM-007-C v1.2):

```markdown
- Animal Campaign Extensions: !`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`
```

| Command | Injection Location | Notes |
|---------|-------------------|-------|
| `continue-quest.md` | After Guardian Skill Definition in Injected Context | Primary path for animal invocation during active campaigns |
| `start-quest.md` | After Gandalf Skill Definition in Injected Context | Animals invocable if user chooses "Consult an animal advisor" from existing-quest options |
| `council.md` | After Gandalf Skill Definition in Injected Context | Council Step 4 roleplays animals in-character; extension context is naturally available to orchestrating agent |

### Not Injected

| Path | Why |
|------|-----|
| `campaign-setup.md` | No animal invocation occurs during setup |
| Direct skill invocation (`/bear-agent` etc.) | No injection mechanism available for Skill-invoked agents |

---

## Invocation Protocol

When a quest command invokes an animal agent via the Skill tool:

1. The orchestrating command has the Animal Campaign Extensions context (from injection)
2. The command instruction says: "When in Phase 3 or later, include the Animal Campaign Extensions context in your invocation message so the animal agent is quest-aware"
3. The orchestrating agent includes the extension context in the Skill tool invocation message
4. The animal agent receives its own SKILL.md (from skill auto-discovery) plus the extension context (from the invocation message)

This relay pattern means the animal agent receives campaign instructions even though its SKILL.md has no campaign content.

### Commands with Animal Invocation Instructions

| Command | Line | Instruction |
|---------|------|-------------|
| `continue-quest.md` | Animal agents bullet | "When in Phase 3 or later, include the Animal Campaign Extensions context in your invocation message so the animal agent is quest-aware." |
| `start-quest.md` | Animal agents bullet | Same instruction |

### Council Exception

`council.md` Step 4 roleplays animals in-character rather than invoking them via the Skill tool. The extension context is naturally available to the orchestrating agent because it's injected into the command. No special invocation instruction is needed.

---

## Context Window Impact

Updated from SPEC-CM-007-D with animal extension additions:

| Content | Approximate Size |
|---------|-----------------|
| Animal Campaign Extensions | ~40 lines |

| Command | Previous Total | New Total | Delta |
|---------|---------------|-----------|-------|
| `start-quest.md` | ~440 lines | ~480 lines | +40 |
| `council.md` | ~440 lines | ~480 lines | +40 |
| `continue-quest.md` | ~910 lines | ~950 lines | +40 |

Worst case (`continue-quest.md`): ~950 lines. This remains within acceptable limits — the ~40-line addition is modest.

---

## Six Animals Context Extensions Stub

### Canonical Text

The following generic section is added to the end of all Six Animals SKILL.md files (after the final existing section):

```markdown
## Context Extensions

When invoked from within a broader workflow (e.g., a structured command or orchestration layer),
supplementary behaviour instructions may be provided in the invocation context. Follow these
instructions alongside your core skill definition. Supplementary instructions may extend flex
behaviours but cannot override the core behaviours defined in this file.
```

### Properties

| Property | Value |
|----------|-------|
| Generic | Yes — no Campaign Mode references |
| Location | After the last existing section in each SKILL.md |
| Files affected | All 7 agents: bear, cat, owl, puppy, rabbit, wolf, simon |
| Copies affected | Both canonical (`skills/`) and clone-path (`.claude/skills/`) — 14 files total |

### Purpose

The stub primes animals to respect supplementary instructions from any orchestration context. It makes campaign extensions more reliable when animals are invoked via the Skill tool, but is not strictly required — campaign extensions can function without it.

---

## Maintenance Checklist

When updating animal campaign extensions:

1. **Extension content changes** — Edit `extensions/animal-campaign-context.md`. Changes propagate automatically via `!`echo`` path injection + Read tool loading.
2. **New command needs animal extensions** — Add the injection block to the command's Injected Context section and add animal invocation instruction if the command Skill-invokes animals.
3. **New animal agent added to Six Animals** — No Campaign Mode change needed (extensions apply generically). Ensure the new agent's SKILL.md has the Context Extensions stub.
4. **Progress tracking format changes** — Update both `extensions/animal-campaign-context.md` and the corresponding section in NPC SKILL.md files (Gandalf Phase 3, Dragon, Guardian) to maintain consistency.
5. **CLAUDE.md progress tracking section changes** — Review extension file for alignment with the updated triggers and format.

---

## Related Specifications

| Spec ID | Title | Relationship |
|---------|-------|--------------|
| [SPEC-CM-007-C](SPEC-CM-007-C-Plugin-Path-Resolution.md) | Plugin Path Resolution | Establishes `!`echo`` two-phase injection pattern |
| [SPEC-CM-007-D](SPEC-CM-007-D-Plugin-Guidelines-Injection.md) | Plugin Guidelines Injection | Previous injection additions; context window baseline |
| [SPEC-CM-001-B](SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | Defines Phase 3 and progress tracking requirements |

---

## Changelog

| Version | Date | Author | Changes |
|---------|------|--------|---------|
| 1.0 | 2026-02-14 | Chris Barlow | Initial specification |
| 1.1 | 2026-02-14 | Chris Barlow | Updated injection syntax from `!cat` to `!echo` two-phase pattern per ADR-CM-015 |
