# ROADMAP-CM-002: Animal Campaign Extensions (v0.2.7)

| Field | Value |
|-------|-------|
| **Roadmap ID** | ROADMAP-CM-002 |
| **Version** | 0.2.7 |
| **Parent ADR** | [ADR-CM-014](../2_adrs/ADR-CM-014-Animal-Campaign-Extensions.md) |
| **Status** | Complete |
| **Date** | 2026-02-14 |

---

## Motivation

CLAUDE.md requires all agents to track campaign progress during Phase 3+, but animal agents (owned by Six Animals) have no campaign awareness. Additionally, Gandalf's SKILL.md has detailed write instructions for Phase 1 and Phase 2 but nothing mechanically specific for Phase 3, causing Gandalf to acknowledge milestones conversationally without updating `quest.md`.

## Approach

1. **Gandalf Phase 3 fix** — Add mechanical Phase 3 progress tracking instructions to Gandalf's SKILL.md Section 4
2. **Animal campaign extensions** — Campaign-owned extension file injected into quest commands via `!`cat`` pattern
3. **Six Animals stub** — Generic "Context Extensions" section in all animal SKILL.md files (separate repo, separate PR)

## Work Items

### Campaign Mode Repo

- [x] Add Phase 3 progress tracking to `skills/gandalf-agent/SKILL.md`
- [x] Mirror Phase 3 tracking to `.claude/skills/gandalf-agent/SKILL.md`
- [x] Create `extensions/animal-campaign-context.md`
- [x] Inject animal campaign extensions into `commands/continue-quest.md`
- [x] Inject animal campaign extensions into `commands/council.md`
- [x] Inject animal campaign extensions into `commands/start-quest.md`
- [x] Update animal invocation instructions in `continue-quest.md` and `start-quest.md`
- [x] Create ADR-CM-014
- [x] Create SPEC-CM-008-A
- [x] Create `docs/5_roadmap/ROADMAP-CM-002-Animal-Campaign-Extensions.md` (this file)
- [x] Bump `plugin.json` to v0.2.7
- [x] Update README with v0.2.7 roadmap section, ADR-CM-014, project structure
- [x] Create commits per commit strategy
- [x] Merge to main, tag v0.2.7, create GitHub release

### Six Animals Repo (Cross-Project)

- [x] Add Context Extensions stub to all 7 canonical SKILL.md files
- [x] Mirror to all 7 clone-path SKILL.md files
- [x] Create commits per commit strategy
- [x] Merge to main in six-animals repo

## Verification Checklist

- [x] Gandalf SKILL.md Section 4 has Phase 3 progress tracking with Read/Write tool instructions
- [x] Both Gandalf SKILL.md copies (canonical + clone-path) are identical
- [x] `extensions/animal-campaign-context.md` exists with progress tracking mechanics
- [x] Extension injection appears in continue-quest, council, and start-quest Injected Context sections
- [x] Animal invocation instructions in continue-quest and start-quest reference extensions
- [x] ADR-CM-014 follows WH(Y) format, documents cross-project dependency
- [x] SPEC-CM-008-A includes context window impact, stub text, maintenance checklist
- [x] ROADMAP-CM-002 lists all work items and verification checks
- [x] plugin.json bumped to v0.2.7
- [x] README has v0.2.7 roadmap entry, ADR-CM-014 in ADR table, `extensions/` in project structure
- [x] All 7 six-animals SKILL.md files have identical Context Extensions section at end
- [x] Context Extensions stub is generic (no campaign-mode references)
