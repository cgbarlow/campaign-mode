# ROADMAP-CM-001: Plugin Guidelines Parity (v0.2.6)

| Field | Value |
|-------|-------|
| **Roadmap ID** | ROADMAP-CM-001 |
| **Version** | 0.2.6 |
| **Parent ADR** | [ADR-CM-013](../2_adrs/ADR-CM-013-Plugin-Guidelines-Parity.md) |
| **Status** | In Progress |
| **Date** | 2026-02-14 |

---

## Motivation

CLAUDE.md establishes cross-cutting campaign conventions (agent identity, context isolation, lifecycle, user-as-protagonist, proactive elicitation) that all NPCs depend on. However, CLAUDE.md is **not auto-loaded** by the plugin infrastructure — it only takes effect when present in the user's project root.

Plugin users who invoke NPC agents without first running `/campaign-setup` operate without these conventions. v0.2.4/v0.2.5 fixed skill path resolution in commands but did not address the missing CLAUDE.md content.

## Approach

Hybrid injection + condensed subset:

| Invocation Path | Mechanism | Content |
|----------------|-----------|---------|
| **Commands** (`/start-quest`, `/continue-quest`, `/council`) | `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` injection | Full CLAUDE.md (~130 lines) |
| **Direct skills** (`/gandalf-agent`, `/dragon-agent`, `/guardian-agent`) | Inline "Campaign Conventions" section in SKILL.md | Condensed subset (~25 lines) |
| `/campaign-setup` | Already injects CLAUDE.md | No change needed |

## Work Items

- [x] Create ADR-CM-013 documenting the hybrid approach
- [x] Create SPEC-CM-007-D specifying injection points and SKILL.md subset content
- [x] Correct SPEC-CM-007-B: plugin CLAUDE.md is NOT auto-loaded (line 99)
- [x] Add CLAUDE.md injection to `start-quest.md`
- [x] Add CLAUDE.md injection to `continue-quest.md`
- [x] Add CLAUDE.md injection to `council.md`
- [x] Update SPEC-CM-007-C with new injection points and context window table
- [x] Add Campaign Conventions section to `skills/gandalf-agent/SKILL.md`
- [x] Add Campaign Conventions section to `skills/dragon-agent/SKILL.md`
- [x] Add Campaign Conventions section to `skills/guardian-agent/SKILL.md`
- [x] Mirror Campaign Conventions to `.claude/skills/` clone-path copies
- [x] Create `docs/5_roadmap/ROADMAP-CM-001-Guidelines-Parity.md` (this file)
- [x] Bump `plugin.json` to v0.2.6
- [x] Update README with v0.2.6 roadmap section, ADR-CM-013, project structure
- [ ] Create GitHub issue for tracking
- [ ] Create commits per commit strategy
- [ ] Merge to main, tag v0.2.6, create GitHub release

## Verification Checklist

- [ ] `!`cat ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`` appears in start-quest, continue-quest, council injected context sections
- [ ] All 6 SKILL.md files (3 canonical + 3 clone-path) contain identical Campaign Conventions sections
- [ ] SPEC-CM-007-B no longer claims plugin CLAUDE.md is auto-loaded
- [ ] SPEC-CM-007-C context window table is updated with CLAUDE.md additions
- [ ] ADR/spec numbering is sequential (013, 007-D)
- [ ] README has v0.2.6 roadmap entry, ADR-CM-013 in table, project structure updated
- [ ] GitHub issue exists and is referenced in release notes
