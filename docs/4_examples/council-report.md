---
created: 2026-02-14
council-type: standalone
---

# Council Report

## Animal Perspectives

### Bear — Vision & Direction

1. **The vision is well-articulated and architecturally sound.** The three-NPC decomposition (Gandalf/Dragon/Guardian) maps cleanly to mentorship, adversarial testing, and quality gates. The context isolation model (advisory/independent/maximum) is a genuinely original contribution that prevents the AI from gaming its own evaluations — the project's most defensible innovation.

2. **The "User as Protagonist" principle is the strategic anchor.** Every design choice — mode selection, agent invocation, proactive elicitation — flows from SDT's autonomy construct. This isn't flavour; it's architectural backbone.

3. **The v0.2 scope is disciplined.** Council, quest lifecycle, three NPCs, plugin distribution. Open questions (Simon's dual role, multi-user campaigns, cultural adaptability) are properly deferred. The roadmap shows restraint.

4. **The gap between vision and validation is the strategic risk.** 11 ADRs, 12 specs, 51KB of skill definitions — but no evidence of user campaigns having been run. The architecture is well-designed in theory; the question is whether the quest flow works in practice, particularly whether Dragon's maximum isolation produces genuinely independent evaluation.

### Cat — Risk & Scope

1. **Context isolation is enforced by instruction, not architecture.** ADR-CM-003 acknowledges this — the Dragon receives "only success criteria + work product" because the SKILL.md says so, not because there's a technical boundary. When Claude plays all roles in the same session, the model has seen everything. "Maximum isolation" is aspirational. This is the single biggest integrity risk.

2. **The documentation-to-implementation ratio is inverted.** 11 ADRs, 12 specs, a north-star, and a detailed README — for three SKILL.md files, four command files, and no runtime code. Design documentation outweighs implementation by roughly 4:1. This signals over-planning relative to what's been built and tested.

3. **Several ADRs are still "Proposed" status.** The master ADR (001) and others haven't been formally accepted. Fifteen open questions remain in the north-star, some resolved but not all cleaned up. This creates ambiguity about which decisions are final.

4. **The Tolkien naming carries IP risk.** "Gandalf" is a trademarked name. Using it in a distributed marketplace plugin is a non-trivial legal exposure that should be resolved before wider distribution.

5. **No tests, no validation harness.** There's no way to verify that agents behave as specified. When a SKILL.md is 21KB of behavioural instructions, how do you catch regressions?

### Owl — Process & Structure

1. **File organisation is clean and well-documented.** Canonical skills in `skills/`, auto-discovery in `.claude/skills/`, commands in `commands/`, docs with numbered subdirectories. The README's project structure section matches reality. Well-organised.

2. **Duplication between `skills/` and `.claude/skills/` creates maintenance burden.** Any change must be made in both locations with no automated sync. Plugin distribution may reduce relevance, but for clone-path users, drift is a process risk.

3. **Campaign lifecycle has clear phase transitions but no enforced ordering.** Six phases are documented, but nothing prevents invoking the Dragon before the Guardian or skipping quest definition. Guardrails are advisory.

4. **Version management is informal.** Plugin.json says v0.2.0, README has milestones, but there are no git tags for releases. Changelog is embedded in README. For marketplace distribution, formalising versioning would help.

### Puppy — Opportunities & Momentum

1. **The quest metaphor is genuinely powerful.** Framing work as a quest with mentors, adversaries, and checkpoints creates emotional engagement. The three campaign modes let users choose their relationship with the work. "Dragon Confrontation" is memorable and motivating in a way "acceptance testing" never will be.

2. **Proactive elicitation is a major UX win.** Agents offer next steps at every phase transition — users never remember slash commands. "Ending a phase without a next-step question is a bug" shows real commitment to user experience.

3. **Character profiles are an untapped opportunity.** The generation system (flavour + modifier, theme-agnostic) is built but not exercised. Example profiles in the README would show people what's possible — a quick win for adoption.

4. **The Council feature is already valuable.** Multi-perspective project diagnostic with synthesis — a powerful tool even outside quest context. Could be the gateway feature that gets people to try Campaign Mode.

### Rabbit — Resources & Stakeholders

1. **Dependency chain is minimal but critical.** Claude Code (platform) and Six Animals (recommended). Six Animals detection via five paths is robust engineering. Both are external dependencies — Claude Code's skill system could change, Six Animals has a separate maintainer.

2. **Distribution has four paths but uneven maturity.** Plugin (recommended), clone, copy-to-project, and personal skills. Different installation methods create different user experiences. Pragmatic but creates support surface area.

3. **Bus factor of 1.** Two listed authors but single-author git history. For a project with this scope of ambition, the sole-implementer risk is worth noting.

4. **No community infrastructure.** No CONTRIBUTING.md, issue templates, discussion forum, or examples directory. For marketplace distribution, community scaffolding would help adoption.

### Wolf — Cohesion & Balance

1. **Design documentation dominates; practical guidance is thin.** Extensive ADRs and specs — but no example campaigns, sample profiles, or end-to-end walkthrough. A new user understands the concept but doesn't see what it feels like. The intellectual framework is strong; experiential onboarding needs warmth.

2. **NPC agents are thoroughly specified; animal integration is assumed.** Gandalf, Dragon, and Guardian have 14-21KB SKILL.md files. But animal agents' campaign-aware behaviour is listed as "future." The animals don't know they're in a campaign. Council bridges this partially.

3. **Progress tracking asks all agents to log, but animals aren't campaign-aware.** CLAUDE.md says "all agents — including animal agents — must track meaningful progress," but animal SKILL.md files (in Six Animals) contain no campaign-mode instructions. Specification-reality mismatch.

4. **Grow mode is richer than Ship mode in design attention.** Character profiles, transformation criteria, deep debrief, and ZPD assessment all lean toward Grow. Ship mode is "streamlined" but has fewer unique features. For broad appeal, delivery-focused mode should feel equally compelling, not reduced.

## Consensus

**Common themes:** The design is mature but validation is not — the project has been deeply thought and now needs to be deeply used. Context isolation is both the core innovation and the core risk (conceptually strong, instruction-enforced). The animal-NPC integration gap creates a specification-reality mismatch around campaign-aware behaviour.

**Key tensions:** Depth vs. breadth (Grow mode richer than Ship, but Ship users likely broader audience). Documentation vs. validation (4:1 spec-to-implementation ratio). Independence vs. integration (designed as complementary but Council assumes animals are present).

**Overall assessment:** Campaign Mode is a well-architected quest framework at the transition point from design to adoption. The NPC decomposition, context isolation model, and user-as-protagonist principle are genuine contributions. The project now needs the shift from designing the system to experiencing the system — running campaigns, collecting feedback, and letting practice inform the next iteration.

## Recommended Next Steps

1. **Run a real campaign end-to-end.** Complete a full quest lifecycle (Council through Debrief) on a real project challenge. This will surface whether phase transitions, proactive elicitation, and context isolation work in practice.
2. **Create example content.** Sample character profiles and a campaign walkthrough would transform the README from "how it works" to "what it feels like" — a quick win for adoption.
3. **Address the Gandalf naming risk.** Resolve the Tolkien IP question before wider marketplace distribution. Decide whether to keep, rename, or disclaim.
4. **Add git tags for releases.** Tag v0.1.0 and v0.2.0 in git to establish release points — a 2-minute task that improves project professionalism.
5. **Bridge the animal integration gap.** Either add campaign-awareness to Six Animals skill definitions (upstream contribution) or adjust CLAUDE.md's progress-tracking expectation to match what animals can actually do.
