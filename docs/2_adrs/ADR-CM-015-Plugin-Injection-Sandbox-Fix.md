# ADR-CM-015: Plugin Injection Sandbox Fix

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-015 |
| **Type** | Standard ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode plugin commands using `!`cat ${CLAUDE_PLUGIN_ROOT}/...`` to inject skill definitions and guidelines into command prompts at invocation time,

**facing** Claude Code's sandbox blocking `cat` from reading files outside the working directory when the plugin is installed (not cloned), causing all 12 injection points across 4 command files to fail silently — returning empty content instead of skill definitions and guidelines,

**we decided for** replacing `!`cat`` with `!`echo`` to inject resolved absolute file paths, combined with an instruction for agents to use the Read tool to load the listed files before proceeding,

**and neglected** embedding content statically into command files (breaks single-source-of-truth and maintenance), waiting for an upstream Claude Code fix to the sandbox restriction (GitHub #9354, unknown timeline), and removing injection entirely (regresses the dynamic context approach established in ADR-CM-012 and ADR-CM-013),

**to achieve** working plugin injection across all installation methods — `echo` bypasses the sandbox because it does not read files, while the Read tool has broader file access and can load plugin cache files at runtime,

**accepting that** this introduces a two-phase injection pattern (path resolution at invocation time, content loading at runtime) which is slightly more complex than the original single-phase approach, and that agents must follow the Read instruction before proceeding.

---

## Context

Campaign Mode plugin commands inject skill definitions and CLAUDE.md guidelines using Claude Code's dynamic context injection syntax (`!`shell-command``). The original approach used `cat` to read file contents:

```
!`cat ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
```

This worked during development (where the repo is the working directory) but fails for plugin installations. Claude Code's sandbox restricts `cat` to the working directory, and `${CLAUDE_PLUGIN_ROOT}` resolves to the plugin cache directory (e.g., `~/.claude/plugins/...`), which is outside the sandbox boundary.

The failure is silent — the injection directive produces empty output, and the agent proceeds without the skill definition or guidelines. This affects all 12 injection points across all 4 command files.

### Evidence

Error messages from plugin users confirm `${CLAUDE_PLUGIN_ROOT}` resolves correctly (the full path appears in error output), but `cat` is denied access by the sandbox.

### Confirmed Behaviours

- `echo ${CLAUDE_PLUGIN_ROOT}/path` — works, outputs the resolved absolute path
- Read tool with absolute path — works, can access plugin cache files
- `cat ${CLAUDE_PLUGIN_ROOT}/path` — blocked by sandbox

## Options Considered

### Option 1: `!echo` Path Injection + Read Tool Loading (Selected)

Replace `!`cat`` with `!`echo`` in all injection directives. This injects the resolved absolute path (not the file content) into the command prompt. Add an instruction in the Injected Context section for the agent to Read all listed files before proceeding.

**Pros:**
- `echo` does not read files, so it bypasses the sandbox restriction
- Read tool has broader file access and can read plugin cache files
- `${CLAUDE_PLUGIN_ROOT}` resolution is preserved
- Minimal change to command file structure
- Includes fallback instructions if path resolution fails

**Cons:**
- Two-phase approach (path injection → content loading) is slightly more complex
- Agents must follow the Read instruction — if they skip it, they proceed without context
- Adds a small amount of latency as agents Read files at runtime

### Option 2: Embed Content Statically (Rejected)

**Why rejected:** Would require copying the full content of CLAUDE.md and all SKILL.md files into each command file. Breaks single-source-of-truth — any change to a skill definition would need to be mirrored into every command that references it. Maintenance burden is severe for `continue-quest.md` which references 5 files.

### Option 3: Wait for Upstream Fix (Rejected)

**Why rejected:** GitHub Issue #9354 tracks the sandbox restriction but has no timeline for resolution. Plugin injection is broken for all users now, and the workaround is straightforward.

### Option 4: Remove Injection Entirely (Rejected)

**Why rejected:** Regresses the dynamic context injection approach established in ADR-CM-012 and extended in ADR-CM-013. Without injection, plugin users would need to run `/campaign-setup` and copy all files to their project root before any command works — losing the zero-setup experience that plugins are meant to provide.

---

## Injection Pattern Change

### Before (Broken)

```markdown
## Injected Context

The following content is injected at invocation time from the plugin's source files.

### Campaign Guidelines

!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
```

### After (Fixed)

```markdown
## Injected Context

The following files contain essential context for this command. Their absolute paths
are resolved below. **Before proceeding with Step 1, use the Read tool to load every
file listed in this section.** Read them in parallel if possible. Do not skip any.

If any path below is empty or shows an error, the plugin root could not be resolved.
Fall back to the Campaign Conventions already embedded in NPC skill definitions.
Inform the user that full context loading failed and suggest running `/campaign-setup`
to copy guidelines to the project root.

- Campaign Guidelines: !`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
```

---

## Affected Files

| Command | Injection Points | Inline References Updated |
|---------|-----------------|---------------------------|
| `campaign-setup.md` | 1 (CLAUDE.md) | 1 |
| `start-quest.md` | 3 (CLAUDE.md, Gandalf, Extensions) | 2 |
| `continue-quest.md` | 5 (CLAUDE.md, Gandalf, Dragon, Guardian, Extensions) | 2 |
| `council.md` | 3 (CLAUDE.md, Gandalf, Extensions) | 1 |
| **Total** | **12** | **6** |

---

## Specifications

| Spec ID | Title | Changes |
|---------|-------|---------|
| [SPEC-CM-007-C](../3_specs/SPEC-CM-007-C-Plugin-Path-Resolution.md) | Plugin Path Resolution | Updated injection syntax, two-phase pattern, fallback section (v1.2) |
| [SPEC-CM-007-D](../3_specs/SPEC-CM-007-D-Plugin-Guidelines-Injection.md) | Plugin Guidelines Injection | Updated injection syntax references (v1.1) |
| [SPEC-CM-008-A](../3_specs/SPEC-CM-008-A-Animal-Campaign-Extensions.md) | Animal Campaign Extensions | Updated injection syntax reference (v1.1) |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-012 | Plugin Desktop Compatibility | Modifies the injection mechanism introduced here |
| Extends | ADR-CM-013 | Plugin Guidelines Parity | Modifies the CLAUDE.md injection introduced here |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Claude Code Sandbox Restriction | Issue | GitHub #9354 |
| REF-002 | SPEC-CM-007-C: Plugin Path Resolution | Specification | [docs/3_specs/SPEC-CM-007-C](../3_specs/SPEC-CM-007-C-Plugin-Path-Resolution.md) |

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
