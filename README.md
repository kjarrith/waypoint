# The Way

A Claude plugin for structured human-agent collaboration. Takes any project — software, hiring, fundraising, content, migration, or anything else — from raw idea to real, delivered progress through five phases.

## Why

AI can't one-shot complex work. The missing piece is a structured path from fuzzy intent to clear specification to real deliverables. The Way provides that path: five phases that work for any domain, carried by a conversational experience that makes thinking feel natural rather than bureaucratic.

It's a thinking amplifier, not an automation shortcut.

## The Five Phases

| Phase | Skill | What happens |
|-------|-------|-------------|
| **Intent** | `/theway:intent` | Braindump your idea, organize it, clarify the gaps, crystallize into an evaluable contract |
| **Gap** | `/theway:gap` | Map the distance between where you are and where the intent says you want to be |
| **Plan** | `/theway:plan` | Decompose the gaps into workstreams with concrete steps, evaluation criteria, and handoff gates |
| **Work** | `/theway:work` | Execute each step, self-evaluate against criteria, get human approval before moving on |
| **Reflect** | `/theway:reflect` | Assess outcomes against intent, capture learnings, close the loop |

Each phase produces a document that the next phase reads. If something goes wrong, you can trace back through the chain.

## How It Works

**Start with intent.** Tell Claude about your project. The intent skill guides a structured conversation that ends with `intent.md` — an evaluable contract that everything downstream references.

**Map the gap.** The gap skill researches what exists today, compares it against the intent, and produces a gap analysis that makes the delta concrete and plannable.

**Plan the work.** The plan skill decomposes gaps into workstreams with agent-sized steps, evaluation criteria, handoff gates, and a clear execution sequence.

**Do the work.** The work skill executes each step, self-evaluates against the plan's criteria, and presents the result for human approval. Steps can be owned by the agent, the human, or external parties.

**Reflect.** The reflect skill assesses outcomes against the original intent, captures what went well and what to change, and closes the project cleanly.

## Key Patterns

**Human decides, agent informs.** Every phase has an explicit approval gate. Agents research, organize, synthesize, and recommend. Humans approve.

**Write after every exchange.** All skills write to disk after each interaction. If a session crashes, all prior work is preserved and the skill can resume where it left off.

**Filesystem as state.** Projects live in `way-docs/` as structured markdown files. No database, no external service. Works in both Claude Code and Claude Desktop.

**Working memory.** Agents maintain external memory in structured files so they don't depend on context window retention across long sessions.

## Project Structure

Each project creates a date-prefixed directory under `way-docs/`:

```
way-docs/
  backlog.md                # Cross-project idea backlog
  {date}-{project-name}/
    loop-state.md           # Current phase, stage, and status
    working-memory.md       # Agent's external brain
    phase-1-intent/
      braindump.md          # Raw conversation with the human
      clarifications.md     # Targeted Q&A on gaps and tensions
      intent.md             # THE CONTRACT for everything downstream
    phase-2-gap/
      gap-analysis.md       # Delta between current state and intent
    phase-3-plan/
      plan.md               # Workstreams, steps, evaluation criteria
    phase-4-work/
      step-{NN}-{name}.md   # Work log per step
    phase-5-reflect/
      reflection.md         # Outcomes, learnings, next actions
```

## Installation

### From a marketplace

```bash
# Add the marketplace source
claude plugin marketplace add https://github.com/kjarrith/theway-plugin

# Install the plugin
claude plugin install theway
```

### Local development

```bash
claude --plugin-dir /path/to/theway-plugin
```

## Getting Started

```
> /theway:intent
```

Tell Claude about your project. The rest follows naturally.

## License

MIT
