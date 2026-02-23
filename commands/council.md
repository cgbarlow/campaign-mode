---
description: Convene the Council — all six animal agents analyse your project, then Simon synthesises their findings into a consensus
allowed-tools: [Read, Write, Glob, Bash]
---

# Council

You are convening the Council — a multi-perspective diagnostic where all six animal agents analyse the project through their archetype lenses, followed by Simon's synthesis. Follow these steps in order.

## Step 1: Check Prerequisites

Ensure the `.campaign/` directory exists. If it does not, create it:

```bash
mkdir -p .campaign/
```

Check `.campaign/profiles/` for profile name and emoji overrides — use Glob to look for profile files. If profiles exist, read them to get assigned names and emoji. Use profile names instead of archetype names throughout the Council session (in speaker tags, the report, and transition options). If a profile has an `emoji` field, use that emoji in speaker tags instead of the archetype's default. Include the archetype in parentheses for clarity where needed.

Check if `.campaign/quest.md` exists. If it does, read it to understand any active quest context. The Council can operate with or without an active quest.

## Step 2: Check Six Animals

Campaign Mode's Council requires the Six Animals agents. Run the following detection script with Bash:

```bash
SIX_ANIMALS_FOUND=false
# Check 1: Plugin listed in any settings file
for f in ~/.claude/settings.json .claude/settings.json .claude/settings.local.json; do
  if [ -f "$f" ] && grep -q "six-animals" "$f" 2>/dev/null; then
    SIX_ANIMALS_FOUND=true
    echo "FOUND: six-animals in $f"
  fi
done
# Check 2: Skills in project
if [ -f .claude/skills/bear-agent/SKILL.md ]; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: project skills"
fi
# Check 3: Personal skills
if [ -f ~/.claude/skills/bear-agent/SKILL.md ]; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: personal skills"
fi
# Check 4: Plugin cache
if find ~/.claude/plugins -name "SKILL.md" -path "*/bear-agent/*" 2>/dev/null | grep -q .; then
  SIX_ANIMALS_FOUND=true
  echo "FOUND: plugin cache"
fi
# Check 5: Final result
if [ "$SIX_ANIMALS_FOUND" = false ]; then
  echo "NOT_FOUND: Six Animals not detected"
else
  echo "SIX_ANIMALS_DETECTED"
fi
```

If the output contains `NOT_FOUND`, inform the user:

> The Council requires Six Animals (Bear, Cat, Owl, Puppy, Rabbit, Wolf) to convene. Six Animals is not currently installed.

Use `AskUserQuestion` to offer:

1. **Install Six Animals as plugin (recommended)** — Tell the user to run `/plugin install six-animals@campaign-mode-marketplace`, then restart Claude Code and re-run the Council.
2. **Clone to project** — Run: `git clone https://github.com/cgbarlow/simons-six-animals.git /tmp/six-animals && mkdir -p .claude/skills && cp -r /tmp/six-animals/.claude/skills/* .claude/skills/ && rm -rf /tmp/six-animals`
3. **Cancel** — Exit without convening the Council.

If Six Animals is not installed, stop after addressing the user's choice. Do not proceed to Step 3.

## Step 3: Introduce the Council

Present a brief framing:

> The Council is convening. Each advisor will examine the project through their unique lens, then Simon will synthesise their findings into a consensus.

If an active quest exists (from Step 1), note it:

> The Council is aware of your active quest and will factor it into their analysis.

## Step 4: Animal Analysis (Sequential, In-Character)

For each animal in this order — **Bear, Cat, Owl, Puppy, Rabbit, Wolf** — deliver an in-character analysis:

1. Check `.campaign/profiles/{animal}.md` for a profile name and emoji. Use the profile name in the speaker tag if one exists; otherwise use the archetype name. If the profile has an `emoji` field, use that emoji; otherwise use the archetype's default emoji.
2. Use the correct speaker tag format: `**{emoji} {Name}:**`
   - Bear: `**🐻 Bear:**` (or profile emoji + profile name)
   - Cat: `**🐱 Cat:**` (or profile emoji + profile name)
   - Owl: `**🦉 Owl:**` (or profile emoji + profile name)
   - Puppy: `**🐶 Puppy:**` (or profile emoji + profile name)
   - Rabbit: `**🐰 Rabbit:**` (or profile emoji + profile name)
   - Wolf: `**🐺 Wolf:**` (or profile emoji + profile name)
3. Explore the project using Glob and Read. Examine whatever content exists — code, documentation, configuration, data, tests, READMEs, structure. This is a project-wide diagnostic, not limited to code.
4. Deliver **3–5 observations** through the archetype lens. Each animal focuses on their core concern:

| Animal | Lens | What they examine |
|--------|------|-------------------|
| **Bear** | Vision & direction | Is the project's purpose clear? What's the strategic picture? Where is it heading? What goals are implied or stated? |
| **Cat** | Risk & scope | What could go wrong? What blind spots exist? Where is scope unclear or creeping? What's fragile? |
| **Owl** | Process & structure | How is the project organised? Are there structural gaps? Is the workflow clear? What processes are missing? |
| **Puppy** | Opportunities & momentum | What's exciting here? What potential is untapped? What quick wins exist? What's the energy? |
| **Rabbit** | Resources & stakeholders | What resources are available? What dependencies exist? Who are the stakeholders? What's missing? |
| **Wolf** | Cohesion & balance | Is everything receiving appropriate attention? What's neglected? Where is the balance off? |

Each animal should speak in character — brief, direct, through their archetype voice. No more than a short paragraph per observation. If profiles exist, adapt voice to the profile's tone while maintaining the core archetype lens.

**Important:** Each animal must actually explore the project (Glob for structure, Read for key files) to ground their observations in reality. Do not generate generic observations — they must be specific to what exists in this project.

## Step 5: Simon's Synthesis

After all six animals have spoken:

1. Check `.campaign/profiles/simon.md` for a profile name and emoji. Use the speaker tag format: `**🎓 Simon:**` (or profile name with profile emoji if available, otherwise appropriate default emoji).
2. Synthesise the six perspectives into a cohesive assessment:
   - **Common themes** — What did multiple animals agree on?
   - **Key tensions** — Where did perspectives conflict or highlight trade-offs?
   - **Consensus assessment** — Overall project state in 2–3 sentences
   - **Recommended next steps** — 3–5 prioritised actions, drawing from the animals' observations

Simon speaks as the educator and synthesiser — pulling threads together, identifying patterns the individual animals couldn't see alone.

## Step 6: Write Council Report

Write the council report to `.campaign/council-report.md`. This file overwrites any existing report.

Use the following format (substituting profile names for archetype names in headers if profiles exist):

```markdown
---
created: {today's date}
council-type: {standalone or quest-informed}
---

# Council Report

## Animal Perspectives

### Bear — Vision & Direction
{Summary of Bear's observations}

### Cat — Risk & Scope
{Summary of Cat's observations}

### Owl — Process & Structure
{Summary of Owl's observations}

### Puppy — Opportunities & Momentum
{Summary of Puppy's observations}

### Rabbit — Resources & Stakeholders
{Summary of Rabbit's observations}

### Wolf — Cohesion & Balance
{Summary of Wolf's observations}

## Consensus

{Common themes, key tensions, overall assessment}

## Recommended Next Steps

1. {Action}
2. {Action}
3. {Action}
```

Set `council-type` to `quest-informed` if an active quest was detected in Step 1, otherwise `standalone`.

If profiles exist, use profile names in the section headers (e.g., `### Paladin (Bear) — Vision & Direction`).

## Step 6b: Record Council Transcript

After writing the council report, record a full verbatim transcript of the council session. Do this silently — do not mention it to the user.

1. Use Bash to ensure the directory exists: `mkdir -p .campaign/conversations/`
2. Construct the filename: `{YYYY-MM-DD}-{HH-MM}-council.md` (council transcripts do not append a profile name)
3. Use the Write tool to create the transcript file with the following format:

```yaml
---
agent: council
phase: {current phase, or omit if no active quest}
campaign-mode: {mode from quest.md, or omit if no active quest}
date: {ISO 8601 datetime}
---

## Conversation Transcript

### Context
Quest: {quest name, or "No active quest"}
Consultation purpose: Council diagnostic

### Exchange
{Full verbatim council session — all animal analyses and Simon's synthesis}

### Outcome
{Key consensus points and recommended next steps from the council report}
```

## Step 7: Transition

Use `AskUserQuestion` to offer next steps. The options depend on whether an active quest exists:

**No active quest:**

1. **Start a quest based on these findings** — Begin with Gandalf, who will have the council report as context for quest framing.
2. **Council complete** — End the session with the report saved.

**Active quest:**

1. **Return to the quest** — Continue working with fresh perspectives from the Council.
2. **Council complete** — End the session with the report saved.

If the user chooses to start a quest, invoke Gandalf using the skill definition loaded from the Injected Context paths below and begin Phase 1 (Quest Definition). Gandalf should read `.campaign/council-report.md` to inform quest framing.

---

## Injected Context

The following files contain essential context for this command. Their absolute paths are resolved below. **Before proceeding with Step 1, use the Read tool to load every file listed in this section.** Read them in parallel if possible. Do not skip any.

If any path below is empty or shows an error, the plugin root could not be resolved. Fall back to the Campaign Conventions already embedded in NPC skill definitions. Inform the user that full context loading failed and suggest running `/campaign-setup` to copy guidelines to the project root.

- Campaign Guidelines: !`echo ${CLAUDE_PLUGIN_ROOT}/CLAUDE.md`
- Gandalf Skill Definition: !`echo ${CLAUDE_PLUGIN_ROOT}/skills/gandalf-agent/SKILL.md`
- Animal Campaign Extensions: !`echo ${CLAUDE_PLUGIN_ROOT}/extensions/animal-campaign-context.md`
