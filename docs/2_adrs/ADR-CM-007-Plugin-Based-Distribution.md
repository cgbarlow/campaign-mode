# ADR-CM-007: Plugin-Based Distribution

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-007 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** distributing Campaign Mode to Claude Code users,

**facing** the limitation that clone-and-copy installation creates friction (requires git knowledge, no update path, no marketplace discoverability) and the absence of per-session campaign guidelines that establish cross-cutting conventions,

**we decided for** packaging Campaign Mode as a Claude Code plugin distributed via the marketplace, with a CLAUDE.md guidelines file auto-copied to the user's project via a `/campaign-setup` command, while retaining `.claude/skills/` for clone-and-use fallback,

**and neglected** plugin-only distribution (breaks existing clone users), embedding guidelines in skill files only (duplicated across three skills, loaded per invocation instead of per session), MCP-based distribution (wrong abstraction — NPCs are instruction-based personas, not tool providers), and the status quo (does not resolve installation friction or convention enforcement),

**to achieve** frictionless installation via marketplace, automatic skill discovery through plugin infrastructure, per-session convention establishment via CLAUDE.md, and backwards compatibility for clone users,

**accepting that** maintaining two distribution paths increases maintenance surface, CLAUDE.md adds to every session's context window, and marketplace publishing introduces a dependency on Anthropic's plugin ecosystem.

---

## Context

Campaign Mode currently distributes three NPC skills (Gandalf, Dragon, Guardian) via clone-and-copy. Users must `git clone` the repo or manually copy `.claude/skills/` to their project. This creates friction: requires git knowledge, no update mechanism, no marketplace discoverability.

ADR-CM-004 chose skills over plugins because the plugin ecosystem was immature. That ecosystem has since matured — Claude Code now supports plugins with marketplace distribution, auto-discovery, commands, and hooks.

Additionally, there is no CLAUDE.md establishing cross-cutting campaign conventions. Individual SKILL.md files define NPC behaviour, but nothing ensures Claude follows campaign-wide rules (context isolation, archetype constraints, user-as-protagonist) consistently across sessions.

### Design Decisions

| Decision | Answer |
|----------|--------|
| **Target interface** | Claude Code only (no Desktop, no Claude.ai Projects) |
| **Packaging** | Claude Code plugin, distributed via marketplace |
| **CLAUDE.md** | Include in plugin, auto-copy to user's project via `/campaign-setup` command |
| **Install paths** | Plugin-first (primary), clone-as-fallback (secondary) |

---

## Options Considered

### Option 1: Plugin-Based Distribution with CLAUDE.md Guidelines (Selected)

Package Campaign Mode as a Claude Code plugin. Skills are auto-discovered via the plugin's `skills/` directory. A CLAUDE.md file establishes per-session campaign conventions. A `/campaign-setup` command copies guidelines to the user's project.

**Pros:**
- Frictionless installation via marketplace (no git knowledge required)
- Automatic updates through plugin infrastructure
- Marketplace discoverability exposes Campaign Mode to new users
- CLAUDE.md loaded every session ensures consistent convention enforcement
- `/campaign-setup` command provides guided onboarding
- Backwards compatible — clone path still works via `.claude/skills/`

**Cons:**
- Two distribution paths increase maintenance surface
- CLAUDE.md adds to every session's context window
- Dependency on Anthropic's plugin ecosystem maturity and stability

### Option 2: Plugin-Only Distribution (Rejected)

**Why rejected:** Breaks existing clone users. The `.claude/skills/` directory pattern is already documented and in use. Removing it forces a migration with no fallback.

### Option 3: Guidelines Embedded in Skill Files Only (Rejected)

**Why rejected:** Cross-cutting conventions (context isolation, archetype constraints, user-as-protagonist) would need to be duplicated across three SKILL.md files. Guidelines are loaded per invocation instead of per session, so conventions are not established until an NPC is invoked.

### Option 4: MCP-Based Distribution (Rejected)

**Why rejected:** MCP servers are designed for tool integration (file access, API calls, database queries). NPC agents are instruction-based personas, not tool providers. An MCP server would be a poor architectural fit.

### Option 5: Status Quo — Clone-and-Copy Only (Rejected)

**Why rejected:** Does not resolve installation friction (requires git knowledge), provides no update mechanism, and does not address the absence of per-session campaign guidelines.

---

## Dual Distribution Model

| Path | How skills are discovered | CLAUDE.md | Who uses this |
|------|--------------------------|-----------|---------------|
| **Plugin install** | `skills/` auto-discovered by plugin infrastructure | Loaded per session from plugin | Users adopting campaign-mode in their projects |
| **Clone repo** | `.claude/skills/` auto-discovered by Claude Code | Loaded per session from repo root | Contributors developing campaign-mode itself |

Both paths coexist. `skills/` serves plugin users, `.claude/skills/` serves clone users. No duplication conflict because a user does one or the other.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-007-A](../3_specs/SPEC-CM-007-A-Plugin-Structure.md) | Plugin Structure | Plugin manifest, directory layout, installation methods |
| [SPEC-CM-007-B](../3_specs/SPEC-CM-007-B-Campaign-Guidelines.md) | Campaign Guidelines | CLAUDE.md content spec, auto-copy mechanism, `/campaign-setup` command |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Extends | ADR-CM-004 | Skill-Based Implementation | Adds distribution layer, does not replace skills |
| Relates To | ADR-CM-003 | NPC Context Isolation | CLAUDE.md reinforces isolation conventions |
| Relates To | ADR-CM-005 | Campaign Mode Selection | CLAUDE.md codifies mode-aware conventions |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Claude Code Plugin Documentation | Technical Reference | [docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-code) |
| REF-002 | ADR-CM-004: Skill-Based Implementation | Decision Record | [docs/2_adrs/ADR-CM-004](ADR-CM-004-Skill-Based-Implementation.md) |
| REF-003 | Campaign Mode North Star | Vision Document | [docs/north-star.md](../north-star.md) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| — | — | — | — | Quarterly | — |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-14 |
| Accepted | Chris Barlow | 2026-02-14 |
