# ROADMAP-CM-003: Plugin Injection Fix + UX Improvements (v0.2.8)

| Field | Value |
|-------|-------|
| **Roadmap ID** | ROADMAP-CM-003 |
| **Version** | 0.2.8 |
| **Parent ADR** | [ADR-CM-015](../2_adrs/ADR-CM-015-Plugin-Injection-Sandbox-Fix.md) |
| **Status** | Complete |
| **Date** | 2026-02-14 |

---

## Motivation

Three issues drive v0.2.8:

1. **Broken plugin injection (critical):** The `!`cat ${CLAUDE_PLUGIN_ROOT}/...`` pattern is blocked by Claude Code's sandbox for plugin installations. `cat` cannot read files outside the working directory, silently failing all 12 injection points across 4 command files.

2. **No onboarding experience:** `/campaign-setup` jumps straight into technical checks. Users don't know what Campaign Mode is, what the agents do, or what to expect.

3. **Simon is invisible:** Simon is defined in docs but never offered as a mid-campaign option. Users don't know he exists or how he differs from Gandalf.

Additionally, six-animals agents need an `AskUserQuestion` interaction pattern for structured user choices.

## Approach

1. **Injection fix:** Replace `!`cat`` with `!`echo`` to inject resolved file paths, then instruct agents to Read the files at runtime
2. **Onboarding:** Add Gandalf welcome greeting (Step 0) to campaign-setup with role introductions
3. **Simon visibility:** Add Simon as mid-campaign option in continue-quest and start-quest; expand README section
4. **Six-animals interaction mechanics:** Add `AskUserQuestion` pattern to all SKILL.md files

## Work Items

### Campaign Mode Repo

- [x] Replace `!cat` with `!echo` in campaign-setup.md (1 injection point)
- [x] Replace `!cat` with `!echo` in start-quest.md (3 injection points)
- [x] Replace `!cat` with `!echo` in continue-quest.md (5 injection points)
- [x] Replace `!cat` with `!echo` in council.md (3 injection points)
- [x] Update Injected Context sections with Read tool instruction and fallback text
- [x] Update 6 inline references ("provided at the end" → "loaded from Injected Context paths")
- [x] Add Gandalf welcome greeting as Step 0 in campaign-setup.md
- [x] Renumber existing campaign-setup steps
- [x] Add Simon as mid-campaign option in continue-quest.md
- [x] Add Simon as mid-campaign option in start-quest.md
- [x] Expand "The Supervisor (Simon)" section in README.md
- [x] Add Simon to campaign flow diagram in README.md
- [x] Create ADR-CM-015
- [x] Update SPEC-CM-007-C to v1.2
- [x] Update SPEC-CM-007-D to v1.1
- [x] Update SPEC-CM-008-A to v1.1
- [x] Create ROADMAP-CM-003 (this file)
- [x] Bump plugin.json to v0.2.8
- [x] Update README with v0.2.8 roadmap section and ADR-CM-015 in ADR table
- [x] Create commits per commit strategy
- [x] Merge to main, tag v0.2.8

### Six Animals Repo (Cross-Project)

- [x] Add Interaction Mechanics section to all 7 canonical SKILL.md files
- [x] Mirror to all 7 clone-path SKILL.md files
- [x] Bump plugin.json to v0.1.2
- [x] Create commits per commit strategy
- [x] Merge to main in six-animals repo

## Verification Checklist

- [ ] All 12 `!cat` directives replaced with `!echo` across 4 command files
- [ ] Each command's Injected Context section has Read tool instruction + fallback text
- [ ] All 6 inline "provided at the end of this command" references updated
- [ ] No `!cat ${CLAUDE_PLUGIN_ROOT}` references remain in codebase
- [ ] campaign-setup has Gandalf greeting as Step 0 explaining all roles including Simon
- [ ] Existing campaign-setup steps renumbered correctly
- [ ] Simon appears as mid-campaign option in continue-quest and start-quest
- [ ] README "The Supervisor (Simon)" section expanded with clear Gandalf/Simon distinction
- [ ] All 14 six-animals SKILL.md files have identical Interaction Mechanics section
- [ ] Six-animals plugin.json bumped to 0.1.2
- [ ] ADR-CM-015 follows WH(Y) format
- [ ] Spec files updated (SPEC-CM-007-C/D, SPEC-CM-008-A)
- [ ] Campaign-mode plugin.json bumped to 0.2.8
- [ ] README has v0.2.8 entry and ADR-CM-015 in ADR table
