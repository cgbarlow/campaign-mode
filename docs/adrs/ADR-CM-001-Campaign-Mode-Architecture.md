# ADR-CM-001: Campaign Mode Architecture

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-001 |
| **Type** | Master ADR |
| **Initiative** | Campaign Mode |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-14 |
| **Aggregate Status** | In Progress |

---

## WH(Y) Decision Statement

**In the context of** extending Six Animals with quest-based functionality,

**facing** the need for structured goal pursuit with adversarial testing and quality gates beyond what the animal roles alone provide,

**we decided for** a 3-NPC bolt-on architecture (Gandalf/Dragon/Guardian) delivered as Claude Code skills that complement the existing Six Animals framework,

**and neglected** a monolithic quest-agent (quest-council approach) and a tightly-coupled integration into six-animals core,

**to achieve** modular extensibility, clear separation of concerns between mentorship/adversarial/gatekeeping functions, and an installation pattern identical to Six Animals,

**accepting that** users must install two packages and understand the NPC/party distinction, and that context isolation between NPCs and party is advisory (instruction-based) rather than architecturally enforced.

---

## Strategic Context

Six Animals provides psychologically-grounded team roles (Bear, Cat, Owl, Puppy, Rabbit, Wolf) that reduce group friction, create psychological safety, and accelerate team formation. However, Six Animals answers "how should we work together?" without addressing "what are we working toward, and what stands in our way?"

Campaign Mode fills this gap by introducing:
- **Direction** — A quest framework channelling collaborative energy toward defined goals
- **Tension** — An adversarial Dragon agent that stress-tests whether the team has truly addressed their challenge
- **Gatekeeping** — A Guardian agent that enforces quality thresholds before the team can progress
- **Mentorship** — A Gandalf agent that coaches the party and helps them grow through the quest

The design draws from two source projects:
- **quest-council** — A monolithic quest-agent (674 lines) combining mentorship, adversarial challenge, gatekeeping, quest design, and platform architecture into a single skill
- **simon-agent** — A pedagogical framework grounded in Self Determination Theory, Zone of Proximal Development, and the "guide on the side" philosophy

Campaign Mode decomposes the monolithic quest-agent into three focused NPCs while preserving the pedagogical foundation from simon-agent.

## Scope Boundary

### In Scope
- Three NPC skill definitions (Gandalf, Dragon, Guardian)
- Campaign lifecycle (quest definition → checkpoint → confrontation → debrief)
- Campaign mode selection (Grow, Ship, Grow & Ship)
- Context isolation protocol for NPC independence
- Skill file structure and conventions aligned with Six Animals

### Out of Scope (Post-v1)
- Alternative cultural/thematic mappings
- Multi-quest campaign arcs
- Extended NPC roster
- Platform architecture (technical NPC implementation, mobile apps, voice API)

---

## Child ADR Registry

| ADR ID | Title | Status | Phase | Dependencies | Owner |
|--------|-------|--------|-------|--------------|-------|
| ADR-CM-002 | Quest Agent Decomposition | Proposed | 1 | — | Chris Barlow |
| ADR-CM-003 | NPC Context Isolation | Proposed | 1 | — | Chris Barlow |
| ADR-CM-004 | Skill-Based Implementation | Proposed | 1 | — | Chris Barlow |
| ADR-CM-005 | Campaign Mode Selection | Proposed | 1 | — | Chris Barlow |
| ADR-CM-006 | Character Generation | Proposed | 1 | — | Chris Barlow |

## Decision Sequencing

### Phase 1: All Decisions (Parallel)
All child ADRs can proceed in parallel as they address orthogonal concerns:
- ADR-CM-002: What NPCs exist and what they do
- ADR-CM-003: How NPCs maintain independence
- ADR-CM-004: How NPCs are technically delivered
- ADR-CM-005: How users choose their campaign orientation
- ADR-CM-006: How users customise animal and NPC presentation within campaigns

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-001-A](../specs/SPEC-CM-001-A-Skill-Architecture.md) | Campaign Mode Skill Architecture | Directory structure, file layout, dual-location convention, installation methods |
| [SPEC-CM-001-B](../specs/SPEC-CM-001-B-Campaign-Lifecycle.md) | Campaign Lifecycle | The 6-phase campaign flow, triggers, and transitions |
| [SPEC-CM-005-A](../specs/SPEC-CM-005-A-Campaign-Mode-Profiles.md) | Campaign Mode Profiles | Mode-agent interaction matrix for Grow, Ship, Grow & Ship |
| [SPEC-CM-006-A](../specs/SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format | Profile file structure, depths, themes, core vs flex |
| [SPEC-CM-006-B](../specs/SPEC-CM-006-B-Campaign-State-Directory.md) | Campaign State Directory | .campaign/ directory structure and export protocol |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Relates To | — | Six Animals Framework | Campaign Mode complements but does not depend on Six Animals |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Six Animals | External Project | [github.com/SimonMcCallum/six-animals](https://github.com/SimonMcCallum/six-animals) |
| REF-002 | Quest Council | Source Material | [github.com/cgbarlow/quest-council](https://github.com/cgbarlow/quest-council) |
| REF-003 | Campaign Mode North Star | Vision Document | [docs/north-star.md](../north-star.md) |
| REF-004 | ADR Reference Framework | ADR Standard | [docs/adrs/reference/](reference/) |

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
