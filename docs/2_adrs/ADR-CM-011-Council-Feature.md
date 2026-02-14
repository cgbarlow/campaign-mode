# ADR-CM-011: Council Feature

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-011 |
| **Type** | Child ADR |
| **Parent ADR** | [ADR-CM-001](ADR-CM-001-Campaign-Mode-Architecture.md) |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** the gap between campaign setup and quest commitment — after `/campaign-setup` creates infrastructure, the user's only option is to immediately start a quest, with no way to first understand the project from multiple perspectives,

**facing** users needing to understand their project's state, strengths, and gaps before choosing a quest direction — particularly in unfamiliar codebases or when the right next step is unclear,

**we decided for** a `/council` command that sequentially invokes all six animal agents to independently analyse the project through their archetype lenses, followed by Simon synthesising findings into a consensus with prioritised next steps, persisted as `.campaign/council-report.md`,

**and neglected** parallel Task sub-agents (analysis invisible to user, loses the conversational feel), Gandalf-only analysis (loses diverse perspectives from six archetypes), and mandatory pre-quest Council (violates user agency — the Council must be optional),

**to achieve** a visible multi-perspective diagnostic where each animal speaks in character, a persistent synthesis artefact that can inform quest definition, and seamless integration with campaign setup as an on-ramp to quest commitment,

**accepting that** sequential animal invocation produces long output, the feature requires Six Animals to be installed, and the council report is overwritten on re-invocation (no history).

---

## Context

Campaign Mode has a gap between setup and quest commitment. After `/campaign-setup` creates infrastructure (CLAUDE.md, `.campaign/` directory), the user's only transition is to start a quest — which immediately commits to a direction via Gandalf's quest framing. There is no way to first survey the project from multiple perspectives before choosing what to work on.

The Council fills this gap: all six animal agents independently analyse the project repository through their archetype lenses (Bear: vision, Cat: risk, Owl: process, Puppy: opportunities, Rabbit: resources, Wolf: cohesion), then Simon synthesises their findings into a consensus with recommended next steps. The user can then optionally transition into quest definition with Gandalf, or take the analysis standalone.

This also addresses a bug in `campaign-setup.md`: Step 4 ends with a slash command reference (`Run /start-quest`) rather than proactive elicitation via `AskUserQuestion`, violating the pattern established in ADR-CM-008.

## Options Considered

### Option 1: Sequential In-Character Analysis (Selected)

Each animal speaks in the main conversation with speaker tags, followed by Simon's synthesis. User sees the full diagnostic unfold.

**Pros:** Visible, engaging, conversational; user sees each perspective as it's delivered; consistent with agent identity conventions
**Cons:** Long sequential output; user must wait for all six analyses

### Option 2: Parallel Sub-Agent Analysis (Rejected)

Launch six Task sub-agents in parallel, collect results, present a summary.

**Why rejected:** The analysis is invisible to the user. They see only the final summary, losing the engaging multi-perspective conversation. The Council's value is partly in watching diverse viewpoints emerge.

### Option 3: Gandalf-Only Analysis (Rejected)

Gandalf surveys the project and frames potential quest directions.

**Why rejected:** Gandalf is a mentor, not a diagnostic tool. The Council's value comes from six distinct archetype lenses — Bear sees vision gaps that Cat sees as risks, Puppy sees opportunities that Owl structures. A single perspective, however wise, misses this diversity.

### Option 4: Mandatory Pre-Quest Council (Rejected)

Require a Council session before any quest can begin.

**Why rejected:** Violates the User as Protagonist principle. The Council must be optional — some users know exactly what they want to work on and shouldn't be forced through a diagnostic step.

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-008 | Proactive Elicitation | Council uses `AskUserQuestion` for transitions; fixes campaign-setup elicitation gap |
| Extends | ADR-CM-009 | Quest Entry Commands | Council provides an additional on-ramp between setup and quest commitment |
| Relates To | ADR-CM-001 | Campaign Mode Architecture | Adds optional pre-quest diagnostic to campaign lifecycle |
| Relates To | ADR-CM-010 | Quest State Tracking | Council report stored in `.campaign/` alongside quest state |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Campaign Lifecycle Spec | Internal Spec | [SPEC-CM-001-B](../3_specs/SPEC-CM-001-B-Campaign-Lifecycle.md) |
| REF-002 | Campaign State Directory Spec | Internal Spec | [SPEC-CM-006-B](../3_specs/SPEC-CM-006-B-Campaign-State-Directory.md) |
| REF-003 | Proactive Elicitation ADR | Internal ADR | [ADR-CM-008](ADR-CM-008-Proactive-Elicitation.md) |
| REF-004 | Quest Entry Commands ADR | Internal ADR | [ADR-CM-009](ADR-CM-009-Quest-Entry-Commands.md) |

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
