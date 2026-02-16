# ADR-CM-016: Profile Packs

| Field | Value |
|-------|-------|
| **Decision ID** | ADR-CM-016 |
| **Type** | Feature ADR |
| **Initiative** | Campaign Mode |
| **Parent ADR** | [ADR-CM-006](ADR-CM-006-Character-Generation.md) |
| **Proposed By** | Chris Barlow |
| **Date** | 2026-02-16 |
| **Status** | Accepted |

---

## WH(Y) Decision Statement

**In the context of** Campaign Mode's Phase 2 (Character Setup) where users can assign character profiles to animal and NPC agents,

**facing** the friction of creating 9 individual profiles from scratch during every campaign, and the desire to bundle community-contributed theme sets as selectable templates,

**we decided for** a convention-based profile pack system where complete profile sets are stored in `profile-packs/{theme-name}/` and selectable during Gandalf's Phase 2 flow, with pack installation copying all 9 profiles to `.campaign/profiles/`,

**and neglected** git-repo-based distribution (over-engineered for current need — packs are small markdown sets, not complex dependencies), and plugin-based packs (too heavyweight — packs are content, not code),

**to achieve** instant theme installation during Phase 2, a clear contribution path for community theme sets via PR, and a growing library of ready-to-use profile collections that lower the barrier to rich campaign experiences,

**accepting that** packs are bundled in the repo (increasing repo size modestly), all packs must be maintained in-tree (no external registry), and pack profiles must follow the unified format defined in SPEC-CM-006-A v1.1.

---

## Strategic Context

Campaign Mode's character profile system (ADR-CM-006, SPEC-CM-006-A) defines how users customise animal and NPC agent presentation and behaviour. The spec defines a theme system with suggested names (Neutral, Fantasy) but no actual profile files exist — users must create every profile from scratch through Gandalf's Socratic dialogue.

This works well for custom themes but creates unnecessary friction for users who want a known theme. The Fantasy theme has 3 example profiles (Paladin, Rogue, Warden) but is missing 6 of 9. Community members have created complete profile sets (e.g., Hundred Acre Wood) that others would benefit from.

Profile packs solve this by bundling complete, ready-to-install profile sets within the Campaign Mode repository.

## Scope Boundary

### In Scope
- Convention-based directory structure for profile packs (`profile-packs/{theme-name}/`)
- Pack selection integrated into Gandalf's Phase 2 flow
- Two initial packs: Fantasy (complete 9-profile set) and Hundred Acre Wood
- Contribution guidelines for submitting new packs via PR
- Unified profile frontmatter format (SPEC-CM-006-A v1.1)

### Out of Scope (Post-v1)
- External pack distribution (registry, marketplace)
- Partial packs (all packs must include all 9 profiles)
- Pack versioning or dependency management
- Automated pack validation tooling

---

## Specifications

| Spec ID | Title | Description |
|---------|-------|-------------|
| [SPEC-CM-006-A](../3_specs/SPEC-CM-006-A-Character-Profile-Format.md) | Character Profile Format (v1.1) | Unified frontmatter format used by all pack profiles |
| [SPEC-CM-009-A](../3_specs/SPEC-CM-009-A-Profile-Pack-Format.md) | Profile Pack Format | Directory structure, file requirements, contribution process |

---

## Dependencies

| Relationship | ADR ID | Title | Notes |
|--------------|--------|-------|-------|
| Parent Of | — | SPEC-CM-009-A | Pack format specification |
| Updates | ADR-CM-006 | Character Generation | Extends with pack-based installation |
| Updates | — | SPEC-CM-006-A v1.1 | Unified frontmatter format |

---

## References

| Reference ID | Title | Type | Location |
|--------------|-------|------|----------|
| REF-001 | SPEC-CM-006-A | Specification | [Character Profile Format](../3_specs/SPEC-CM-006-A-Character-Profile-Format.md) |
| REF-002 | Gandalf Agent Skill | Skill Definition | [skills/gandalf-agent/SKILL.md](../../skills/gandalf-agent/SKILL.md) |

---

## Status History

| Status | Approver | Date |
|--------|----------|------|
| Proposed | Chris Barlow | 2026-02-16 |
| Accepted | Chris Barlow | 2026-02-16 |
