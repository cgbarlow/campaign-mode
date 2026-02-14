# ADR-CM-014: Animal Campaign Extensions

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-014 |
| **Type** | Standard ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode requiring all agents — including Six Animals agents (Bear, Cat, Owl, Puppy, Rabbit, Wolf) — to track progress and operate with quest awareness during active campaigns,

**facing** the gap that animal agents are owned by the separate Six Animals project and have no campaign-specific behaviour, meaning they cannot read `quest.md`, track progress, or respond to phase transition signals when invoked during a campaign,

**we decided for** a campaign-owned extension file (`extensions/animal-campaign-context.md`) injected into quest commands via the established `!`cat`` pattern, with a generic "Context Extensions" stub added to Six Animals SKILL.md files to prime animals to respect supplementary instructions,

**and neglected** modifying Six Animals SKILL.md files with campaign content (violates project separation), relying on CLAUDE.md conversation context alone (unreliable across Skill tool boundaries), and maintaining campaign-mode copies of animal SKILL.md files (duplication nightmare),

**to achieve** quest-aware animal agent behaviour during campaigns — including progress tracking, quest context grounding, and phase transition awareness — without coupling the Six Animals project to Campaign Mode,

**accepting that** the extension context adds ~40 lines per command invocation, animal agents invoked directly (not through campaign commands) will not receive campaign extensions, and the Six Animals "Context Extensions" stub is a cross-project dependency that requires a separate PR in that repository.

---

## Context

CLAUDE.md Section "Campaign Progress Tracking" states that when `.campaign/quest.md` exists and the campaign is in Phase 3, **all agents** must track meaningful progress. However, animal agents are owned by the Six Animals project and have no awareness of Campaign Mode concepts (quest.md, progress logs, success criteria, phase transitions).

When animal agents are invoked via the Skill tool from campaign commands (`/continue-quest`, `/start-quest`), they receive only their own SKILL.md context. Campaign conventions from CLAUDE.md do not cross the Skill tool boundary reliably.

Two related issues:
1. Animal agents cannot track progress because they have no instructions to do so
2. Animal agents cannot ground their advice in quest context because they don't know to read `quest.md`

### Constraint: Project Separation

Campaign Mode and Six Animals are independent projects. Campaign Mode complements Six Animals but must not inject campaign-specific content into Six Animals' codebase. Any solution must respect this boundary.

## Options Considered

### Option 1: Campaign-Owned Extension File with Command Injection (Selected)

Create `extensions/animal-campaign-context.md` in the Campaign Mode repo containing campaign-specific behaviour extensions for animal agents. Inject this into quest commands alongside existing skill and CLAUDE.md injections. Add a generic "Context Extensions" stub to Six Animals SKILL.md files to prime animals to respect supplementary instructions.

**Pros:**
- Campaign Mode owns all campaign-specific content
- Follows established `!`cat`` injection pattern (ADR-CM-012, ADR-CM-013)
- Six Animals stub is generic — no campaign references, useful for any orchestration context
- Extension content is available when animals are invoked through campaign commands

**Cons:**
- Animals invoked directly (`/bear-agent`) without campaign commands don't receive extensions
- Cross-project dependency on Six Animals stub (separate PR)
- Adds ~40 lines to command context window

### Option 2: Modify Six Animals SKILL.md Files with Campaign Content (Rejected)

**Why rejected:** Violates project separation. Campaign Mode concepts (quest.md, progress logs, Dragon, Guardian) do not belong in Six Animals' codebase. Would create a hard dependency in the wrong direction.

### Option 3: Rely on CLAUDE.md Conversation Context (Rejected)

**Why rejected:** CLAUDE.md content does not reliably cross Skill tool invocation boundaries. When an animal agent is invoked via the Skill tool, it receives its SKILL.md and the invocation message — not the calling context's CLAUDE.md. Testing confirms animals do not follow CLAUDE.md progress tracking instructions when Skill-invoked.

### Option 4: Campaign-Mode Copies of Animal SKILL.md Files (Rejected)

**Why rejected:** Maintaining 7 duplicate SKILL.md files (one per animal) creates a severe maintenance burden. Any Six Animals update would need to be mirrored. The duplication nightmare outweighs the benefit.

---

## Cross-Project Dependency

The "Context Extensions" stub added to Six Animals SKILL.md files is a separate change in a separate repository:

| Item | Detail |
|------|--------|
| **Repository** | six-animals |
| **Change** | Add generic "Context Extensions" section to all 7 SKILL.md files |
| **Branch** | `feature/context-extensions` |
| **Content** | Generic stub — no Campaign Mode references |
| **Purpose** | Primes animals to respect supplementary instructions from any orchestration context |

The stub is not required for campaign extensions to function — it makes them more reliable by explicitly telling animals to follow supplementary instructions. Campaign extensions work without the stub but may be less consistently followed.

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-008-A](../3_specs/SPEC-CM-008-A-Animal-Campaign-Extensions.md) | Animal Campaign Extensions | Extension file content, injection points, invocation protocol, stub text |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Extends | ADR-CM-013 | Plugin Guidelines Parity | Extends injection pattern to include animal extensions |
| Extends | ADR-CM-012 | Plugin Desktop Compatibility | Uses established `!`cat`` injection mechanism |
| Relates To | ADR-CM-010 | Quest State Tracking | Progress tracking in quest.md |
| Relates To | ADR-CM-009 | Quest Entry Commands | Commands modified to inject extensions |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | CLAUDE.md Campaign Progress Tracking | Guidelines | [CLAUDE.md](../../CLAUDE.md) |
| REF-002 | SPEC-CM-007-D: Plugin Guidelines Injection | Specification | [docs/3_specs/SPEC-CM-007-D](../3_specs/SPEC-CM-007-D-Plugin-Guidelines-Injection.md) |
| REF-003 | Six Animals Repository | External | [github.com/SimonMcCallum/six-animals](https://github.com/SimonMcCallum/six-animals) |

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
