# Waypoint

A Claude Code plugin for structured human-agent collaboration. It takes any project, whether software, hiring, content or operations, from a raw idea to delivered work through a few short phases, each ending in one document.

It's a thinking amplifier, not an automation shortcut: the agent researches, organizes and recommends; the human decides.

## Phases

| Phase | Skill | Output |
|-------|-------|--------|
| Intent | `/waypoint:intent` | `intent.md`: the outcome, success criteria, non-goals and constraints everything later is checked against |
| Gap | `/waypoint:gap` | `gap.md`: the executing agent's brief (what exists, what's missing, next steps), plus anything found that could change the intent |
| Plan (optional) | `/waypoint:plan` | `plan.md`: ordered steps, for projects with several workstreams or real dependencies |
| Work | `/waypoint:work` | `work.md`: one entry per approved step |
| Reflect | `/waypoint:reflect` | `reflection.md`: outcome against intent, and learnings |

Gap can be skipped when the current state is already clear, and plan is only for complex projects. Simple work reads its steps straight from the gap analysis.

## Projects

```
waypoints/
  index.md                   every project's ID and summary, plus parked ideas
  2026-11/
    014-onboarding-redesign/
      intent.md
      gap.md
      work.md
      reflection.md
```

IDs come from one counter across all of `waypoints/`. During a phase the conversation is the working memory; the phase's document is written when it's ready for review, so the documents themselves are the project's state. The full rules are in [`conventions.md`](conventions.md).

## Install

```bash
claude plugin marketplace add kjarrith/waypoint
claude plugin install waypoint@waypoint
```

To develop locally, run `claude --plugin-dir /path/to/waypoint`.

## License

MIT
