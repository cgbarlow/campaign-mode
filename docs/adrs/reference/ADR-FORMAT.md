# ADR-REF-001: Enhanced ADR Format

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-REF-001 |
| **Initiative** | Project Architecture |
| **Proposed By** | Architecture Team |
| **Date** | 2026-01-08 |
| **Status** | Proposed |

---

## WH(Y) Decision Statement

**In the context of** a project's need to record and maintain architecture decisions consistently,

**facing** inconsistent ADR structure, conflation of decision rationale with implementation details, living documents that obscure original decisions, and missing infrastructure for tracking dependencies and governance,

**we decided for** an enhanced WH(Y) ADR format that separates decision rationale from implementation specifications,

**and neglected** extending typical ad-hoc formats (perpetuates conflation), TOGAF frameworks (excessive ceremony), and maintaining the status quo (missed governance opportunity),

**to achieve** clear separation of decision rationale from implementation specs, structured dependency tracking between ADRs, embedded governance metadata with review cadence and approval workflows, and support for Master ADRs in complex initiatives,

**accepting that** teams must learn the WH(Y) syntax, manage separate specification files, and adopt new conventions adding initial overhead.

---

## Context

Architecture Decision Records in many projects exhibit several problems:

1. **Inconsistent structure** -- Different ADRs follow different formats, making them hard to navigate and compare
2. **Conflation of concerns** -- Implementation code and configuration embedded within decision records
3. **Living documents** -- Appended updates obscure original decisions and their rationale
4. **Missing infrastructure** -- No tracking for dependencies, alternatives, or governance

The root cause: when decision rationale and implementation details are combined, decisions become unmaintainable, and implementation docs lack the detail developers need.

## Options Considered

### Option 1: Enhanced WH(Y) ADR Format (Selected)

Introduce an enhanced format that:
- Employs a 6-part WH(Y) statement (context, facing, decided for, neglected, achieve, accepting)
- Separates specifications into dedicated files while keeping ADRs lean
- Tracks dependencies between decisions with relationship types
- Embeds governance metadata including review cadence and approval workflows
- Supports Master ADRs for complex, multi-decision initiatives

**Pros:** Structured rationale capture, clean separation, dependency tracking, governance support
**Cons:** Learning curve for WH(Y) syntax, additional file management, convention overhead

### Option 2: Extend Current Format (Rejected)

Add optional fields to the existing ADR format.

**Why rejected:** Perpetuates the conflation problem. Optional fields tend to be ignored, and the fundamental issue of mixing decisions with implementation remains.

### Option 3: TOGAF Architecture Framework (Rejected)

Adopt a full TOGAF-style decision framework.

**Why rejected:** Excessive ceremony for most project contexts. Most teams would find the overhead prohibitive and abandon the practice.

### Option 4: Status Quo (Rejected)

Keep the current approach.

**Why rejected:** Misses the opportunity to address the four identified problems during active architecture development.

---

## Specifications

This ADR is supported by the following detailed specifications:

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-ADR-A](SPEC-ADR-A-WHY-Format.md) | WH(Y) Statement Format | Defines the 6-part structured decision statement |
| [SPEC-ADR-B](SPEC-ADR-B-Minimalism.md) | ADR Minimalism & Separation | Defines content boundaries between ADRs and specs |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| -- | -- | -- | No existing dependencies (foundational reference) |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | Michael Nygard - Documenting Architecture Decisions | External Reference | [cognitect.com](https://www.cognitect.com/blog/2011/11/15/documenting-architecture-decisions) |
| REF-002 | Olaf Zimmermann - Sustainable Architectural Design Decisions | External Reference | [ozimmer.ch](https://www.ozimmer.ch/practices/2020/04/27/ArchitectureDecisionMaking.html) |
| REF-003 | Olaf Zimmermann - Definition of Done for AD Making | External Reference | [ozimmer.ch](https://www.ozimmer.ch/practices/2020/05/22/ADDefinitionOfDone.html) |

---

## Governance

| Review Board | Date | Outcome | Action | Review Cadence | Next Review |
|--------------|------|---------|--------|----------------|-------------|
| -- | -- | -- | -- | Quarterly | -- |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Architecture Team | 2026-01-08 |
