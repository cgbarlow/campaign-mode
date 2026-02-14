# ADR-CM-012: Plugin Desktop Compatibility

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-012 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-007](ADR-CM-007-Plugin-Based-Distribution.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode plugin commands failing in Claude Desktop — commands appear in the Plugins menu but invoking them does nothing,

**facing** the root cause that commands reference skill files using relative paths (e.g., `skills/gandalf-agent/SKILL.md`) that resolve against the user's project directory rather than the plugin cache, and `campaign-setup.md` references "this plugin's root directory" without a mechanism to locate it,

**we decided for** using Claude Code's `!`command`` dynamic context injection syntax with `${CLAUDE_PLUGIN_ROOT}` to inject skill and CLAUDE.md content directly into command prompts at invocation time, eliminating runtime path resolution entirely,

**and neglected** absolute path construction at runtime (fragile, depends on knowing cache location), embedding skill content directly in commands (duplicates content, breaks single-source-of-truth), and accepting CLI-only support (excludes Desktop users unnecessarily),

**to achieve** commands that work identically in both Claude Code CLI and Claude Desktop, with no runtime file reads required for skill or guideline content,

**accepting that** injected content increases command prompt size (each skill adds ~200-400 lines to context), commands that invoke multiple NPCs (e.g., `continue-quest`) inject all potentially needed skills upfront, and the `!`command`` syntax is a Claude Code-specific feature that may evolve.

---

## Context

ADR-CM-007 established plugin-based distribution with a "Claude Code only" target interface constraint. This was appropriate when the plugin ecosystem was CLI-only, but Claude Desktop now supports plugins — installing them and listing their commands in the Plugins menu.

However, commands fail silently in Desktop because they contain instructions like "load the skill from `skills/gandalf-agent/SKILL.md`" — a relative path that only resolves correctly when the working directory is the plugin's own directory. In Claude Desktop (and Claude Code when the user is in their project directory), the path resolves against the user's project, where no `skills/` directory exists.

A separate Claude Code bug (fixed in v2.1.29) hid plugin skills from the `/` autocomplete menu, but even with that fix, the path resolution issue prevents commands from functioning.

### The Injection Mechanism

Claude Code supports dynamic context injection in command files using the syntax:

```
!`command`
```

When a command file contains this syntax, Claude Code executes the shell command at invocation time and injects the output directly into the prompt. Combined with the `${CLAUDE_PLUGIN_ROOT}` environment variable (which points to the plugin's installation directory), this provides a reliable way to inject file content:

```
!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
```

This replaces the runtime instruction "load the skill from path X" with the actual skill content, pre-resolved at invocation time.

## Options Considered

### Option 1: Dynamic Context Injection via `!`command`` (Selected)

Replace path-based skill loading instructions with `!`cat ${CLAUDE_PLUGIN_ROOT}/path`` directives that inject content at invocation time.

**Pros:**
- Works in both CLI and Desktop — no runtime file resolution needed
- Single-source-of-truth preserved — skills are still authored once in `skills/`
- Clean separation — commands describe behaviour, injected content provides definitions
- No changes to skill files themselves

**Cons:**
- Increases command prompt size (skill content injected into every invocation)
- Commands that may invoke multiple NPCs must inject all potentially needed skills
- Depends on `${CLAUDE_PLUGIN_ROOT}` environment variable and `!`command`` syntax

### Option 2: Absolute Path Construction at Runtime (Rejected)

**Why rejected:** Requires knowing the plugin cache location, which varies by platform and installation method. Fragile and not future-proof.

### Option 3: Embed Skill Content Directly in Commands (Rejected)

**Why rejected:** Duplicates skill content across commands and skill files, breaking single-source-of-truth. Any skill update requires updating every command that references it.

### Option 4: Accept CLI-Only Support (Rejected)

**Why rejected:** Claude Desktop supports plugins and users reasonably expect commands to work. Excluding Desktop users is unnecessary given the injection mechanism is available.

---

## Impact on Clone-Path Users

None. Clone-path users do not use commands (per SPEC-CM-007-A). They invoke skills directly via `.claude/skills/` auto-discovery and interact with CLAUDE.md from the repository root. The `!`command`` syntax only appears in `commands/` files, which are a plugin-only feature.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-007-C](../3_specs/SPEC-CM-007-C-Plugin-Path-Resolution.md) | Plugin Path Resolution | Injection mechanism, injection points, and context window impact |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-007 | Plugin-Based Distribution | Supersedes "Claude Code only" target interface constraint |
| Relates To | ADR-CM-009 | Quest Entry Commands | Commands modified to use injection |
| Relates To | ADR-CM-011 | Council Feature | Council command modified to use injection |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Claude Code Plugin Documentation | Technical Reference | [docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-code) |
| REF-002 | ADR-CM-007: Plugin-Based Distribution | Decision Record | [docs/2_adrs/ADR-CM-007](ADR-CM-007-Plugin-Based-Distribution.md) |
| REF-003 | SPEC-CM-007-A: Plugin Structure | Specification | [docs/3_specs/SPEC-CM-007-A](../3_specs/SPEC-CM-007-A-Plugin-Structure.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
| Accepted | Chris Barlow | 2026-02-14 |
