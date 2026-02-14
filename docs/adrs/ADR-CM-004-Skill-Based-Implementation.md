# ADR-CM-004: Skill-Based Implementation

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-004 |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Proposed |

---

## WH(Y) Decision Statement

**In the context of** choosing an implementation mechanism for campaign-mode NPCs,

**facing** the need for portability, ease of installation, and alignment with the existing Six Animals delivery model,

**we decided for** Claude Code skills (SKILL.md files) as the implementation format, following the same patterns established by Six Animals,

**and neglected** Claude plugins (immature ecosystem, harder to develop), MCP servers (overkill for instruction-based agents), and custom API integrations (not portable across surfaces),

**to achieve** identical installation patterns to Six Animals, cross-surface compatibility (Claude.ai, Claude Code, API), community accessibility, and low barrier to contribution,

**accepting that** skills are instruction-only and cannot enforce hard architectural constraints like context isolation, and that complex orchestration (multi-step campaigns with state) requires the user or an orchestrating agent to manage flow.

---

## Context

Campaign Mode needs a delivery mechanism for its three NPC agents. The mechanism must:

1. **Match Six Animals** — Users already install Six Animals as Claude Code skills. Campaign Mode should feel like a natural extension, not a different technology.
2. **Be portable** — Work across Claude.ai, Claude Code CLI, and direct API usage.
3. **Be accessible** — Contributors should be able to create and modify NPC agents by editing markdown files, not writing code.
4. **Support independent invocation** — Each NPC should be invocable as a standalone skill (/gandalf-agent, /dragon-agent, /guardian-agent).
5. **Enable context isolation** — At least at an advisory level, via sub-agent invocation.

## Options Considered

### Option 1: Claude Code Skills — SKILL.md Files (Selected)

Implement NPCs as SKILL.md files following the Claude Code skill format:
- YAML frontmatter (name, description, metadata)
- Structured markdown body defining behaviour
- Auto-discovered via `.claude/skills/` directory
- Invocable as slash commands

**Pros:**
- Identical to Six Animals delivery mechanism
- Cross-surface compatible (Claude.ai, Claude Code, API)
- Easy to create, modify, and contribute (just markdown)
- Auto-discovery via `.claude/skills/` directory
- Community-accessible (no programming required)
- Version-controllable (git-friendly)

**Cons:**
- Instruction-only — cannot enforce architectural constraints
- No state management — campaign state doesn't persist between sessions
- No orchestration — multi-phase campaigns require manual flow management
- Limited to what Claude can interpret from instructions

### Option 2: Claude Plugins (Rejected)

Implement NPCs as Claude plugins with dedicated API endpoints and session management.

**Why rejected:** The Claude plugin ecosystem is immature. Developing plugins requires significantly more infrastructure than skills. The overhead is not justified for v1, where the NPC agents are instruction-based and don't require custom API endpoints. This may be appropriate for future evolution, particularly for hard context isolation.

### Option 3: MCP Servers (Rejected)

Implement NPCs as Model Context Protocol servers providing tools.

**Why rejected:** MCP servers are designed for tool integration (file access, API calls, database queries). NPC agents are instruction-based personas, not tool providers. An MCP server would be a poor fit architecturally — we'd be using a tool-serving mechanism to deliver behavioural instructions.

### Option 4: Custom API Integration (Rejected)

Build a custom application that orchestrates NPC agents via the Claude API directly.

**Why rejected:** Not portable. Would require users to run a custom application instead of using Claude Code directly. Breaks the "install skills, use Claude" model that Six Animals established. May be appropriate for a future platform but not for v1 bolt-on delivery.

---

## Skill File Conventions

Campaign Mode skills follow these conventions (detailed in SPEC-CM-004-A):

| Convention | Detail |
|------------|--------|
| **File name** | Always `SKILL.md` |
| **Directory** | kebab-case agent name: `gandalf-agent/`, `dragon-agent/`, `guardian-agent/` |
| **Dual location** | Canonical in `skills/`, auto-discovery copy in `.claude/skills/` |
| **Frontmatter** | YAML with name, description, license, metadata |
| **License** | CC-BY-SA-4.0 (matching Six Animals content license) |
| **Body structure** | Overview → Foundation → Core Capabilities → Interaction Patterns → Integration → Usage Guidelines |

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-004-A](../specs/SPEC-CM-004-A-Skill-File-Structure.md) | Skill File Structure and Conventions | YAML frontmatter requirements, naming, progressive disclosure, compatibility with Six Animals |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Part Of | ADR-CM-001 | Campaign Mode Architecture | Parent initiative |
| Relates To | ADR-CM-002 | Quest Agent Decomposition | Skills are the delivery mechanism for the three NPCs |
| Relates To | ADR-CM-003 | NPC Context Isolation | Skills enforce isolation through instructions |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Claude Code Skills Documentation | Technical Reference | [docs.anthropic.com](https://docs.anthropic.com/en/docs/claude-code) |
| REF-002 | The Complete Guide to Building Skills for Claude | Reference Guide | docs/reference/ |
| REF-003 | Six Animals Skills | Pattern Reference | six-animals/skills/*/SKILL.md |

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
