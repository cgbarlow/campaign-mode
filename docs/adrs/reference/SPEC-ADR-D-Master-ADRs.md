# SPEC-ADR-D: Master ADRs

| Field | Value |
|-------|-------|
| **Specification ID** | SPEC-ADR-D |
| **Parent ADR** | [ADR-REF-001](ADR-FORMAT.md) |
| **Version** | 1.0 |
| **Status** | Draft |
| **Last Updated** | 2026-01-08 |

---

## Overview

A Master ADR (also called "Epic ADR" or "Parent ADR") is an overarching decision record that encompasses multiple related child ADRs. It captures strategic direction while delegating specific implementation details to subordinate records.

---

## When to Use Master ADRs

| Condition | Example |
|-----------|---------|
| Multiple interdependent decisions | Cloud migration requiring provider, network, identity, and data decisions |
| Single entry point needed | Stakeholders need overview of complete architectural change |
| Multi-team coordination | Initiative spans multiple teams or domains |
| Governance visibility | Major programme requires complete decision landscape |
| Aggregate status tracking | Track overall progress while child decisions advance independently |

---

## Master ADR Structure

```mermaid
flowchart TB
    subgraph Master["MADR-001: Cloud Migration Strategy"]
        direction TB
        ADR101["ADR-101<br/>Cloud Provider"]
        ADR102["ADR-102<br/>Landing Zone"]
        ADR103["ADR-103<br/>Network Model"]
        ADR104["ADR-104<br/>Identity Strategy"]
        ADR105["ADR-105<br/>Data Migration"]

        ADR101 --> ADR102
        ADR102 --> ADR103
        ADR102 --> ADR104
        ADR101 --> ADR105
    end
```

---

## Master ADR Elements

| Element | Description | Required |
|---------|-------------|----------|
| Strategic Context | The overarching business or technical driver | Yes |
| Scope Boundary | What decisions are in/out of scope | Yes |
| Child ADR Registry | List of all subordinate ADRs with status | Yes |
| Decision Sequencing | Order or phases for child decisions | Recommended |
| Aggregate Status | Overall status derived from children | Auto-calculated |

---

## Child ADR Registry

The registry tracks all subordinate decisions and their progress:

| ADR ID | Title | Status | Phase | Dependencies | Owner |
|--------|-------|--------|-------|--------------|-------|
| ADR-101 | Target Cloud Provider | Approved | 1 | - | Platform Team |
| ADR-102 | Landing Zone Architecture | Approved | 1 | ADR-101 | Platform Team |
| ADR-103 | Network Connectivity Model | Under Review | 2 | ADR-102 | Network Team |
| ADR-104 | Identity & Access Strategy | Under Review | 2 | ADR-102 | Security Team |
| ADR-105 | Data Migration Approach | Proposed | 3 | ADR-101 | Data Team |

---

## Decision Sequencing

Child ADRs should be organized into phases reflecting their logical ordering and dependencies.

**Phase 1: Foundation (Prerequisites)**
- ADR-101: Cloud Provider Selection
- ADR-102: Landing Zone Architecture

**Phase 2: Infrastructure (Parallel)**
- ADR-103: Network Connectivity
- ADR-104: Identity & Access

**Phase 3: Migration (After Phase 1 & 2)**
- ADR-105: Data Migration Approach
- ADR-106: Application Migration Pattern

```mermaid
gantt
    title Decision Sequencing
    dateFormat  YYYY-MM-DD
    section Phase 1
    Cloud Provider Selection     :done, p1a, 2026-01-01, 30d
    Landing Zone Architecture    :done, p1b, after p1a, 30d
    section Phase 2
    Network Connectivity         :active, p2a, after p1b, 30d
    Identity & Access            :active, p2b, after p1b, 30d
    section Phase 3
    Data Migration               :p3a, after p2a, 30d
    Application Migration        :p3b, after p2a, 30d
```

---

## Aggregate Status Rules

| Status | Condition |
|--------|-----------|
| **Proposed** | No child ADRs approved yet |
| **In Progress** | At least one child approved, others pending |
| **Approved** | All required child ADRs approved |
| **Partially Implemented** | Some child ADRs implemented |
| **Completed** | All child ADRs implemented or retired |
| **Blocked** | Any child ADR rejected or has unresolved conflict |

### Status Calculation Logic

```python
def calculate_aggregate_status(child_adrs):
    statuses = [adr.status for adr in child_adrs]

    if any(s == 'Rejected' for s in statuses):
        return 'Blocked'
    if all(s in ['Implemented', 'Retired'] for s in statuses):
        return 'Completed'
    if any(s == 'Implemented' for s in statuses):
        return 'Partially Implemented'
    if all(s == 'Approved' for s in statuses):
        return 'Approved'
    if any(s == 'Approved' for s in statuses):
        return 'In Progress'
    return 'Proposed'
```

---

## Master ADR Template

```markdown
# MADR-{ID}: {Strategic Initiative Title}

| Field | Value |
|-------|-------|
| **Decision ID** | MADR-{ID} |
| **Type** | Master ADR |
| **Initiative** | {Programme/Project Name} |
| **Proposed By** | {Author} |
| **Date** | {Date} |
| **Aggregate Status** | {Calculated} |

---

## WH(Y) Decision Statement

**In the context of** {strategic context},

**facing** {overarching challenge or opportunity},

**we decided for** {strategic direction},

**and neglected** {alternative strategies},

**to achieve** {strategic benefits},

**accepting that** {strategic trade-offs and complexity}.

---

## Strategic Context

{Detailed description of business or technical drivers}

## Scope Boundary

### In Scope
- {Decision area 1}
- {Decision area 2}

### Out of Scope
- {Excluded area 1}
- {Excluded area 2}

---

## Child ADR Registry

| ADR ID | Title | Status | Phase | Dependencies | Owner |
|--------|-------|--------|-------|--------------|-------|
| ADR-xxx | {Title} | {Status} | {Phase} | {Dependencies} | {Team} |

---

## Decision Sequencing

### Phase 1: {Phase Name}
{Description and included ADRs}

### Phase 2: {Phase Name}
{Description and included ADRs}

---

## Aggregate Status History

| Status | Date | Notes |
|--------|------|-------|
| Proposed | {Date} | Initial creation |
| In Progress | {Date} | First child ADR approved |

---

## Governance

| Review Board | Date | Outcome | Next Review |
|--------------|------|---------|-------------|
| {Board} | {Date} | {Outcome} | {Date} |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
```

---

## Validation Rules

| Rule | Description | Severity |
|------|-------------|----------|
| `MADR-001` | Master ADR must have at least one child ADR | Warning |
| `MADR-002` | All child ADRs must have PART_OF relationship | Error |
| `MADR-003` | Phase numbers must be sequential | Warning |
| `MADR-004` | Dependencies must respect phase ordering | Warning |
| `MADR-005` | Scope boundary must be defined | Info |

---

## Source Reference

Based on Master ADR concepts from Recording Architecture Decisions (Expanded).
