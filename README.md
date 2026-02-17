# Are you ready for Campaign Mode?

**Six perspectives. Three challengers. One quest. Your blind spots, found.**

Inspired by Dr Simon McCallum's [Six Animals](https://github.com/SimonMcCallum/six-animals) collaboration framework, a psychologically-grounded model where six animal archetypes represent genuinely different ways of thinking. Campaign Mode gives you a structured quest to put all of them to work on your challenge.

![Campaign Mode agents gathered in a fantasy tavern — the six animal advisors (Bear, Cat, Owl, Puppy, Rabbit, Wolf) plan around a map table while Simon observes from by the hearth, Gandalf and the Guardian stand watch, and the Dragon peers in through the window](docs/campaign-mode-agents.jpg)

## You Deserve More Than a Single Perspective

You're working on something that matters. But working alone — or with a single AI perspective — you miss things. The risks you didn't think to check. The assumptions you didn't know you were making. The angle you never considered because it's not how you think.

Campaign Mode recruits a party of AI advisors who think differently from each other, and from you. You frame your work as a quest with clear success criteria, structured phases, and a defined endpoint. Your advisors challenge your assumptions, surface your blind spots, and stress-test your work before it matters. You confront your dragons in a safe environment — and you come out with something you're genuinely proud of.

Whether you're here to learn, to ship, or both — you drive the quest. The agents serve you; they don't drive it.

## Quick Start

### Claude Desktop

1. From the **Code** tab, select **+** → **Plugins** → **Add plugin**
2. **Add marketplace** — Select the **By Anthropic** dropdown, then select **Add marketplace from GitHub** and enter:
   ```
   https://github.com/cgbarlow/campaign-mode/
   ```
3. **Install plugins** — find and install both **Campaign Mode** and **Six Animals** from the marketplace
4. **Set up your project** — run:
   ```
   /campaign-setup
   ```
   This checks for pre-requisites, copies guidelines, and creates your `.campaign/` directory.
5. **Choose your path:**
   - `/council` — Have all six animal advisors analyse your project before deciding what to work on
   - `/start-quest` — Jump straight into quest framing with Gandalf

### Claude Code CLI

1. **Install Claude Code** ([full guide](https://code.claude.com/docs/en/quickstart)):
   ```bash
   curl -fsSL https://claude.ai/install.sh | bash
   ```
2. **Add the marketplace** — in a Claude Code session:
   ```
   /plugin marketplace add cgbarlow/campaign-mode
   ```
3. **Install the plugin:**
   ```
   /plugin install campaign-mode@campaign-mode-marketplace
   ```
4. **Set up your project:**
   ```
   /campaign-setup
   ```
   This checks for Six Animals, copies guidelines, and creates your `.campaign/` directory.
5. **Choose your path:**
   - `/council` — Have all six animal advisors analyse your project before deciding what to work on
   - `/start-quest` — Jump straight into quest framing with Gandalf

That's it. Every agent offers you structured next steps — you never need to memorise commands after setup.

## What You Get

| What you get | How it works |
|-------------|--------------|
| **Diverse perspectives** | Six animal advisors — each grounded in a different psychological profile — catch what you'd miss alone |
| **Direction** | A quest framework that channels your work toward defined success criteria |
| **Your choice of focus** | Grow (learn), Ship (deliver), or both — you decide before the quest begins |
| **Mentorship** | A Gandalf that guides without rescuing — a guide on the side, not a sage on the stage |
| **Quality gates** | A Guardian that ensures you're ready before advancing to harder challenges |
| **Adversarial testing** | A Dragon that stress-tests whether your work genuinely meets your success criteria |

## How It Works

### You Are the Protagonist

You drive the quest. You invoke agents. You produce the work. You face the challengers.

You shape the quest, choose which perspectives to consult, do the work, and present it for evaluation. The agents serve your quest; they don't drive it.

### Choose Your Mode

Before the quest begins, you choose how you want to approach it:

| Mode | Focus | Framing |
|------|-------|---------|
| **Grow** | Learning experience | "What will you learn? Who will you become?" |
| **Ship** | Get work done | "What will you deliver? What does done look like?" |
| **Grow & Ship** (Default) | Both | "What will you learn AND deliver?" |

Your mode tunes how every agent behaves — from how Gandalf frames the quest, to what the Dragon evaluates, to how fast the Guardian lets you progress.

### Your Advisory Council

Six animal agents — from the [Six Animals](https://github.com/SimonMcCallum/six-animals) framework — operate as your advisory council:

| Animal | How they help your quest |
|--------|------------------------|
| **Bear** | Vision and direction — what are you actually trying to achieve? |
| **Cat** | Risk assessment — what could go wrong? What are you not seeing? |
| **Owl** | Timeline and process — are you on track? What's the structure? |
| **Puppy** | Morale and momentum — what opportunities are you missing? |
| **Rabbit** | Resources and stakeholders — who and what do you need? |
| **Wolf** | Team cohesion — is everyone contributing? Are you balanced? |

During a quest, the animals actively hand off to each other — suggesting which perspective you should hear next based on what was just discussed.

### Your Guides and Challengers

Three NPC agents operate **outside the party's shared context** to maintain independent judgement:

| NPC | Role | What they do for you |
|-----|------|---------------------|
| **Gandalf** | Mentor | Frames your quest, establishes success criteria with you, and mentors without rescuing |
| **Guardian** | Gatekeeper | Evaluates your progress at checkpoints — approve, not yet (with feedback), or conditional approval |
| **Dragon** | Adversary | Tests whether your success criteria are genuinely met through rigorous, independent evaluation |

### The Supervisor (Simon)

Simon is the educator and meta-analyst — operating *above* the quest while Gandalf operates *within* it. Simon synthesises the Council's findings, offers mid-campaign reflection on how you're working, and provides the post-Dragon debrief scaled to your campaign mode.

### Campaign Flow

   Council (optional)     Your animals analyse the project; Simon synthesises findings
        |
1. Quest Definition       You choose your mode. Gandalf frames the challenge.
        |                 Success criteria, narrative, and party assignments written to .campaign/quest.md
2. Character Setup        Optionally assign character profiles to your animals and NPCs
        |
3. Campaign Execution     You work the quest with proactive animal engagement
        |                 Simon available for mid-campaign reflection at any time
4. Guardian Checkpoint    Guardian evaluates your readiness (repeats at key stages)
        |
5. Dragon Confrontation   Dragon tests your work against your success criteria
        |
6. Debrief                Simon reflects on your journey (depth varies by mode)


Your campaign state is persisted in `.campaign/quest.md` — so you can leave and return between sessions. Use `/continue-quest` to pick up where you left off.

## What a Quest Looks Like

> You're redesigning your app's onboarding flow. You run `/start-quest` and Gandalf helps you frame three success criteria. Cat immediately flags that you haven't considered accessibility. Owl structures a timeline. You build the prototype, then call for a Guardian checkpoint — the Guardian says "not yet" because criterion two isn't evidenced. You iterate. When you're ready, you face the Dragon. The Dragon probes your weakest criterion, finds it holds, and the Dragon is slain. Simon debriefs you on what you learned about your own blind spots.

That's one quest. Yours will be different — but the structure holds whether you're writing code, planning a project, drafting a document, or working through a personal challenge.

## Commands

| Command | What it does |
|---------|-------------|
| `/campaign-setup` | Set up Campaign Mode in your project |
| `/council` | All six animals analyse your project; Simon synthesises their findings |
| `/start-quest` | Begin a new quest with Gandalf |
| `/continue-quest` | Re-enter an active campaign where you left off |
| `/gandalf-agent` | Consult the mentor |
| `/dragon-agent` | Challenge your work against success criteria |
| `/guardian-agent` | Request a checkpoint evaluation |

These work alongside the Six Animals commands (`/bear-agent`, `/cat-agent`, `/owl-agent`, `/puppy-agent`, `/rabbit-agent`, `/wolf-agent`, `/simon-agent`).

## Examples

| Example | Description |
|---------|-------------|
| [Council Report](docs/4_examples/council-report.md) | Multi-perspective project diagnostic from all six animals with Simon synthesis |
| [Bear — The Paladin](docs/4_examples/profiles/bear-paladin.md) | Fantasy character profile for Bear |
| [Cat — The Rogue](docs/4_examples/profiles/cat-rogue.md) | Fantasy character profile for Cat (with behavioural modifiers) |
| [Wolf — The Warden](docs/4_examples/profiles/wolf-warden.md) | Fantasy character profile for Wolf |

Three built-in profile packs are available: **Fantasy** (D&D-inspired), **Hundred Acre Wood** (Pooh-inspired), and **Family & Parenting**. You can also create your own.

## More Information

- [Changelog](CHANGELOG.md) — version history and release notes
- [Architecture](docs/ARCHITECTURE.md) — design principles, architecture decision records, and project structure
- [North Star](docs/north-star.md) — vision and open questions

## Relationship to Six Animals

[Six Animals](https://github.com/SimonMcCallum/six-animals) provides the foundational team dynamics framework — six psychologically-grounded animal archetypes plus Simon as educator. Campaign Mode provides quest structure, mentorship, and adversarial challenge. Together they create a complete system for guided collaborative work.

| Project | Focus | Agents |
|---------|-------|--------|
| [Six Animals](https://github.com/SimonMcCallum/six-animals) | Team roles and collaboration dynamics | Bear, Cat, Owl, Puppy, Rabbit, Wolf + Simon |
| Campaign Mode | Quest structure, mentorship, and adversarial challenge | Gandalf, Dragon, Guardian |

## Contributing

Contributions are welcome — bug reports, feature ideas, character profiles, campaign experiences, and documentation improvements. See [CONTRIBUTING.md](CONTRIBUTING.md) for guidelines.

## Acknowledgements

Campaign Mode is built on Dr Simon McCallum's Six Animals framework, which has been used in university courses at Victoria University of Wellington and NTNU Norway since approximately 2011.

"Gandalf" is a trademark of Middle-earth Enterprises, used here as a cultural reference to describe an archetypal mentor role. Campaign Mode is not affiliated with or endorsed by the Tolkien Estate or Middle-earth Enterprises.

## License

CC-BY-SA-4.0

## Authors

- **Chris Barlow** — Campaign Mode design and implementation
- **Dr. Simon McCallum** — Six Animals framework, pedagogical foundation, Simon agent design
