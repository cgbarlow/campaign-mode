# ADR-CM-009: Quest Entry Commands

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-009 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-001](ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** extending Campaign Mode with ergonomic entry-point commands,

**facing** users needing to remember agent-specific slash commands to start or resume campaigns — creating unnecessary cognitive load and breaking the proactive elicitation principle established in ADR-CM-008,

**we decided for** two dedicated commands (`/start-quest` and `/continue-quest`) that delegate to NPC agents and present natural-language options via `AskUserQuestion`,

**and neglected** a single overloaded `/quest` command (ambiguous intent — start vs continue?) and auto-routing without user input (violates the User as Protagonist principle),

**to achieve** zero-knowledge campaign entry where users can begin or resume quests without memorising agent-specific commands, natural re-entry after breaks with context-aware next-step options, and consistency with the proactive elicitation pattern,

**accepting that** two additional commands must be maintained alongside the existing agent commands, and direct agent invocation (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) remains valid for users who prefer it.

---

## Context

After `/campaign-setup` completes, users are told to invoke `/gandalf-agent` to begin a quest. Mid-campaign, users returning after a break must remember which agent to invoke next. Both scenarios require command vocabulary knowledge that the proactive elicitation principle (ADR-CM-008) was designed to eliminate within agent interactions — but the gap remains at campaign entry and re-entry points.

Two new commands address this:
- **`/start-quest`** — Invoked after `/campaign-setup`. Checks for an active quest, then delegates to Gandalf to begin Phase 1 quest framing.
- **`/continue-quest`** — Re-entry point for active campaigns. Reads `.campaign/quest.md` to detect campaign state, then presents context-aware next-step options.

Both commands follow the proactive elicitation pattern: natural language options via `AskUserQuestion`, no slash command references in user-facing text.

## Options Considered

### Option 1: Two Dedicated Commands (Selected)

Separate `/start-quest` and `/continue-quest` commands with clear, distinct purposes.

**Pros:** Unambiguous intent, each command does one thing well, consistent with proactive elicitation
**Cons:** Two more commands to maintain

### Option 2: Single `/quest` Command (Rejected)

One overloaded command that auto-detects whether to start or continue.

**Why rejected:** Ambiguous — when a quest exists, should it start a new one or continue? Forces the command to guess intent, which undermines user agency.

### Option 3: Auto-Routing (Rejected)

Automatically detect campaign state and invoke the appropriate agent without user input.

**Why rejected:** Violates the User as Protagonist principle. The user should choose what to do next, not have the system decide for them.

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-008 | Proactive Elicitation | Applies proactive elicitation to campaign entry/re-entry points |
| Refines | ADR-CM-001 | Campaign Mode Architecture | Adds ergonomic entry commands to the campaign lifecycle |
| Relates To | ADR-CM-007 | Plugin-Based Distribution | New commands distributed as part of the plugin |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Campaign Lifecycle Spec | Internal Spec | [SPEC-CM-001-B](../3_specs/SPEC-CM-001-B-Campaign-Lifecycle.md) |
| REF-002 | Campaign Guidelines Spec | Internal Spec | [SPEC-CM-007-B](../3_specs/SPEC-CM-007-B-Campaign-Guidelines.md) |
| REF-003 | Proactive Elicitation ADR | Internal ADR | [ADR-CM-008](ADR-CM-008-Proactive-Elicitation.md) |

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
