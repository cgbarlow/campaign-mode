# ADR-CM-013: Plugin Guidelines Parity

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-013 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-012](ADR-CM-012-Plugin-Desktop-Compatibility.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** plugin users invoking NPC agents via commands (`/start-quest`, `/continue-quest`, `/council`) or direct skill invocation (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) without first running `/campaign-setup`,

**facing** the gap that CLAUDE.md cross-cutting conventions (agent identity blending rules, core vs flex framework, lifecycle overview, proactive elicitation meta-rule, debrief protocol) are not available unless the user has copied CLAUDE.md to their project root — and SPEC-CM-007-B line 99 incorrectly claimed plugin CLAUDE.md is auto-loaded,

**we decided for** a hybrid approach: inject full CLAUDE.md into command prompts via `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` (extending the ADR-CM-012 injection pattern), and add a condensed "Campaign Conventions" subset directly into each NPC SKILL.md file for direct skill invocations,

**and neglected** full CLAUDE.md injection into SKILL.md files (SKILL.md files cannot use `!`command`` syntax — only commands support dynamic injection), requiring `/campaign-setup` as a prerequisite for all paths (breaks standalone NPC invocation), and embedding full CLAUDE.md content as static text in SKILL.md files (duplicates ~130 lines per skill, breaks single-source-of-truth),

**to achieve** consistent campaign conventions across all invocation paths — both command-based and direct skill — without requiring users to run `/campaign-setup` first,

**accepting that** the SKILL.md condensed subset (~25-30 lines) is a curated summary rather than the full CLAUDE.md content, creating a maintenance surface where CLAUDE.md changes may need to be reflected in SKILL.md files, and the command path includes both CLAUDE.md and the SKILL.md subset (harmless redundancy — conventions are reinforced, not contradicted).

---

## Context

ADR-CM-012 established dynamic context injection (`!`command`` syntax with `${CLAUDE_PLUGIN_ROOT}`) to resolve plugin command failures in Claude Desktop. That decision focused on injecting NPC skill definitions into commands, and CLAUDE.md into `/campaign-setup`.

However, CLAUDE.md establishes cross-cutting conventions that all NPCs depend on:
- Agent identity rules (no blending, profile name overrides, selection menu guidance)
- Core vs flex archetype framework
- Campaign lifecycle overview (six phases)
- Proactive elicitation meta-rule (every phase transition must offer next steps)
- Campaign debrief protocol (Dragon-to-Simon handoff)

These conventions were assumed to be available in every session, but they are only present when:
1. The user runs `/campaign-setup` (which copies CLAUDE.md to the project root), or
2. The user clones the repo and works within it (CLAUDE.md at repo root)

Plugin users who skip setup and invoke agents directly operate without these conventions. SPEC-CM-007-B line 99 incorrectly stated "Claude Code loads it automatically at the start of every session when the plugin is installed" — this is not how plugin CLAUDE.md files work.

### Two Invocation Paths

| Path | How it works | Gap |
|------|-------------|-----|
| **Commands** (`/start-quest`, `/continue-quest`, `/council`) | Plugin command files processed by Claude Code | CLAUDE.md not injected (only skill definitions were) |
| **Direct skills** (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) | SKILL.md loaded by Claude Code skill auto-discovery | No injection mechanism available — SKILL.md cannot use `!`command`` syntax |

## Options Considered

### Option 1: Hybrid Injection + Condensed Subset (Selected)

Inject full CLAUDE.md into commands (extending ADR-CM-012 pattern), and add a condensed subset of conventions directly into SKILL.md files.

**Pros:**
- Both invocation paths covered
- Commands get full CLAUDE.md content
- SKILL.md subset covers only what SKILL.md files don't already contain
- No new prerequisites for users

**Cons:**
- Condensed subset is a curated summary — must be maintained alongside CLAUDE.md
- Commands receive both CLAUDE.md and SKILL.md subset (minor redundancy)

### Option 2: Full CLAUDE.md in SKILL.md Files (Rejected)

**Why rejected:** SKILL.md files cannot use `!`command`` syntax. Embedding the full ~130 lines as static text triples the size of each SKILL.md and creates a severe single-source-of-truth problem.

### Option 3: Require `/campaign-setup` for All Paths (Rejected)

**Why rejected:** NPC agents are designed to be invocable standalone. Requiring setup breaks the established contract and adds friction that discourages adoption.

### Option 4: CLAUDE.md Injection into Commands Only (Rejected)

**Why rejected:** Covers only the command path. Direct skill invocation (`/gandalf-agent` etc.) — a common usage pattern — would still lack conventions.

---

## Condensed Subset Content

The SKILL.md "Campaign Conventions" section covers conventions **not already present** in individual SKILL.md files:

| Convention | In CLAUDE.md | Already in SKILL.md | In Condensed Subset |
|-----------|-------------|--------------------|--------------------|
| Speaker identification format | Yes | Yes | No (already covered) |
| No identity blending | Yes | No | Yes |
| Profile name overrides for menus | Yes | No | Yes |
| Core vs flex framework | Yes | No | Yes |
| Six-phase lifecycle summary | Yes | No | Yes |
| Mode definitions | Yes | Yes (detailed) | No (already covered) |
| Context isolation levels | Yes | Yes (per-agent) | No (already covered) |
| Progress tracking triggers | Yes | No | Yes |
| Proactive elicitation meta-rule | Yes | Partially | Yes (reinforced) |
| Debrief protocol | Yes | No | Yes |

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-007-D](../3_specs/SPEC-CM-007-D-Plugin-Guidelines-Injection.md) | Plugin Guidelines Injection | Injection points, SKILL.md subset content, context window impact |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-012 | Plugin Desktop Compatibility | Extends injection pattern to include CLAUDE.md |
| Extends | ADR-CM-007 | Plugin-Based Distribution | Further addresses plugin user experience |
| Relates To | ADR-CM-009 | Quest Entry Commands | Commands modified to inject CLAUDE.md |
| Relates To | ADR-CM-011 | Council Feature | Council command modified to inject CLAUDE.md |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | SPEC-CM-007-B: Campaign Guidelines | Specification | [docs/3_specs/SPEC-CM-007-B](../3_specs/SPEC-CM-007-B-Campaign-Guidelines.md) |
| REF-002 | SPEC-CM-007-C: Plugin Path Resolution | Specification | [docs/3_specs/SPEC-CM-007-C](../3_specs/SPEC-CM-007-C-Plugin-Path-Resolution.md) |
| REF-003 | ADR-CM-012: Plugin Desktop Compatibility | Decision Record | [docs/2_adrs/ADR-CM-012](ADR-CM-012-Plugin-Desktop-Compatibility.md) |

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
