# Recording Architecture Decisions

*"We will keep a collection of records for "architecturally significant" decisions: those that affect the structure,
non-functional characteristics, dependencies, interfaces, or construction techniques."* — **Michael Nygard**

## What is an ADR?

An architecture decision record (ADR) captures an important architectural decision with its context and consequences. Related concepts include:

- **Architecture decision (AD)**: A design choice addressing a significant requirement
- **Architecture decision log (ADL)**: Collection of all ADRs for a project or organization
- **Architecturally-significant requirement (ASR)**: A requirement with measurable effect on system architecture
- **Architecture knowledge management (AKM)**: The overarching topic

## Why Write ADRs

*"Architecture decision records, also known as ADRs, are a great way to document how and why a
decision was reached."* ADRs serve multiple audiences:

- Future versions of yourself
- Current peers and colleagues
- Future team members

## ADR Minimalism: Keeping Decisions Lean

ADRs should capture **decision** and **rationale**, not detailed implementation. They answer "what and why?" rather than "how?"

### What Belongs in an ADR

- Decision statement
- Context and problem
- Options considered and rejected alternatives
- Expected benefits and trade-offs
- Governance and status metadata
- References to specifications

### What Belongs in Specifications

- Technical designs and diagrams
- API contracts and interfaces
- Data models and schemas
- Configuration standards
- Implementation patterns
- Step-by-step procedures

### Benefits of Separation

| Concern | ADR | Specification |
|---------|-----|---------------|
| **Stability** | Rarely changes once approved | Evolves with implementation |
| **Audience** | Decision-makers, architects | Implementers, developers |
| **Versioning** | Immutable record | Living document |
| **Review cycle** | Architecture governance boards | Technical team reviews |
| **Granularity** | One decision per ADR | Multiple specs per ADR |

## WH(Y) Statement Format

The **WH(Y) statement** uses six interconnected elements forming a single sentence:

1. **Context**: Functional requirement or architecture component
2. **Facing**: Non-functional requirement or quality concern
3. **We decided for**: Decision outcome (most important element)
4. **And neglected**: Alternatives not chosen
5. **To achieve**: Benefits or satisfied requirements
6. **Accepting that**: Drawbacks and costs

**Example**: *"In the context of the Web shop service, facing the need to keep user session
data consistent across shop instances, we decided for the Database Session State Pattern and
neglected Client or Server Session State to achieve cloud elasticity, accepting that a session
database needs design, implementation, and replication."*

## Extended ADR Template

### Architecture Decision Record (ADR) Components

| Field | Description |
|-------|-------------|
| **Decision** | Unique identifier |
| **Initiative ID** | Project reference |
| **Proposed by** | Author |
| **Context** | Functional requirement or use case |
| **Facing** | Non-functional requirement |
| **We decided for** | Decision outcome |
| **And neglected** | Rejected alternatives |
| **To achieve** | Benefits |
| **Accepting that** | Drawbacks and costs |

### Supporting Metadata

**Dependencies**

| Relationship | Related ADR | Title | Notes |
|--------------|-------------|-------|-------|
| Depends On/Supersedes/Relates To/Refines/Part Of | ADR identifier | Title | Explanation |

**References**

| Reference ID | Title | Type | Location | Version |
|--------------|-------|------|----------|---------|
| Spec identifier | Document title | Specification/Design/Policy/Standard | Path/URL | Version |

**Governance**

| Board | Date | Outcome | Action | Cadence | Next Review |
|-------|------|---------|--------|---------|-------------|
| Name (e.g., TDC, AC) | Presentation date | Endorsed/Rejected | Resulting action | Frequency | Date |

**Status**

| Status | Approver | Date |
|--------|----------|------|
| Approved/Under Review/Expired/Retired/Rejected/Superseded | Usually Product Owner | Change date |

## ADR Dependencies and Relationships

### Types of Relationships

**Depends On**: An ADR requires another decision to be in place first.

**Supersedes**: An ADR replaces a previous decision, changing its status to "Superseded."

**Relates To**: ADRs share context or concerns but neither strictly depends on the other.

**Refines**: An ADR provides specific guidance within boundaries of a broader decision.

### Master ADRs

A **Master ADR** encompasses multiple related child ADRs, capturing high-level strategic decision while delegating specific implementation decisions to subordinate records.

#### When to Use Master ADRs

- Multiple interdependent decisions requiring cohesive understanding
- Single entry point needed for stakeholders
- Initiative spans multiple teams or domains
- Governance requires visibility of complete decision landscape
- Tracking overall status of complex initiative

#### Master ADR Structure

| Element | Description |
|---------|-------------|
| **Strategic Context** | Overarching business or technical driver |
| **Scope Boundary** | In/out of scope decisions |
| **Child ADR Registry** | All subordinate ADRs with status |
| **Decision Sequencing** | Order or phases for child decisions |
| **Aggregate Status** | Overall initiative status |

#### Child ADR Registry Example

| ADR ID | Title | Status | Phase | Dependencies |
|--------|-------|--------|-------|--------------|
| ADR-101 | Target Cloud Provider | Approved | 1 | — |
| ADR-102 | Landing Zone Architecture | Approved | 1 | ADR-101 |
| ADR-103 | Network Connectivity Model | Under Review | 2 | ADR-102 |
| ADR-104 | Identity & Access Strategy | Under Review | 2 | ADR-102 |
| ADR-105 | Data Migration Approach | Proposed | 3 | ADR-101 |

#### Aggregate Status Rules

- **Proposed**: No child ADRs approved yet
- **In Progress**: At least one child approved, others pending
- **Approved**: All required child ADRs approved
- **Partially Implemented**: Some child ADRs implemented
- **Completed**: All child ADRs implemented or retired
- **Blocked**: Any child ADR rejected or conflicting

## Definition of Done for Architectural Decision Making

A comprehensive checklist ensuring architectural decisions are thoroughly evaluated:

1. **Evidence (E)**: Are we confident this design will work?
2. **Criteria (C)**: Have we decided between at least two options systematically?
3. **Agreement (A)**: Have we discussed sufficiently and reached common understanding?
4. **Documentation (D)**: Have we captured and shared the decision record?
5. **Realization & Review (R)**: Do we know when to realize, review, and revise?

### Extended Definition of Done

Additional criteria for comprehensive decision management:

6. **Dependencies (Dp)**: Have we identified and documented relationships to other ADRs?
7. **References (Rf)**: Have we separated detailed specifications into referenced artefacts?
8. **Master ADR (M)**: If part of larger initiative, have we linked to the Master ADR?

## Simple ADR Template (Michael Nygard)

**Title**: Short noun phrase

**Status**: Proposed, accepted, rejected, deprecated, superseded, etc.

**Context**: Issue motivating decision or change

**Decision**: Proposed change and justification

**Consequences**: What becomes easier or more difficult

**Metadata**: Approver, approval date, notes

**Measurements for Compliance**: How compliance is measured (automated or manual)

## Business Case ADR Template

**Title**
**Status**
**Evaluation criteria**
**Candidates to consider**
**Research and analysis of each candidate**
**Does/doesn't meet criteria and why**
**Cost analysis**
**SWOT analysis**
**Opinions and feedback**
**Recommendation**

## ADR Dependency Visualization Tools

When managing large ADR portfolios, consider tooling that:

- Parses dependency metadata and generates relationship graphs
- Highlights orphaned ADRs with no defined relationships
- Identifies circular dependencies
- Shows impact paths for change analysis
- Automatically aggregates status for Master ADRs

Common approaches include:

- Custom scripts parsing ADR markdown files
- Graph databases (Neo4j) for complex queries
- Architecture tools with ADR plugins (Structurizr, ADR-tools)
- Wiki platforms with linking capabilities (Confluence, Notion)

---

**Sources Referenced**:
- Michael Nygard: "Documenting Architecture Decisions"
- Joel Parker Henderson: "Architecture Decision Record" (GitHub)
- GitHub Blog: "Why Write ADRs?" (2020)
- Oliver Zimmer: "Architecture Decision Making" and "A Definition of Done for Architectural Decision Making"
