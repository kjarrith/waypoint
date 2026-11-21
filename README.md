# Waypoint

**Think it through with your agent before it builds.** Waypoint is a Claude Code plugin that takes any project, whether code, hiring, content or operations, from a half-formed idea to delivered work, in a few short phases. Each phase ends in one plain markdown document.

Most agent workflows are about specs for code. Waypoint starts earlier, at what you actually want, and ends later, with whether you got it. The agent researches, organizes and recommends; you decide.

## Quick start

```bash
claude plugin marketplace add kjarrith/waypoint
claude plugin install waypoint@waypoint
```

Then, in any repo or folder:

```
/waypoint:intent
```

Tell it what you're thinking about. It takes it from there.

## The phases

| Phase | Command | You get |
|-------|---------|---------|
| Intent | `/waypoint:intent` | `intent.md`: the outcome, success criteria, non-goals and constraints that everything later is checked against |
| Gap | `/waypoint:gap` | `gap.md`: what exists today, what's missing, and the next steps, plus anything found that should change the intent |
| Plan (optional) | `/waypoint:plan` | `plan.md`: a short brief for you and the detailed steps for the agent |
| Work | `/waypoint:work` | the work itself, one approved step at a time, logged in `work.md` |
| Reflect | `/waypoint:reflect` | `reflection.md`: did it achieve the intent, and what to learn from how it went |

Small projects skip the plan, and sometimes the gap analysis too.

## What makes it different

- **Intent comes first, and it's a conversation.** The agent plays back what it thinks you want, specific enough to be wrong, then goes further: it names the deeper goal, the tension you haven't noticed, and a sharper version of the idea. Where a picture helps, it offers to sketch two or three options for you to choose between.
- **Your time goes where your judgment matters.** The gap analysis is the agent's homework, so you aren't asked to approve it, only to decide on what it found that changes the intent. Plans open with a short brief for you; the paths and detail sit underneath for the agent.
- **One-way doors are named.** Before a plan is written, the agent brings you every decision that's costly to reverse or that involves a real trade-off, with the alternatives. It never goes through a one-way door you haven't agreed to.
- **It closes the loop.** Reflect captures what the process taught you while it's fresh. When results take weeks to show, it writes an outcome check and can schedule an agent run to do it on the due date.
- **The documents are the state.** No database, no service, no hidden files: just markdown in your repo, written for the next person or agent who picks the project up cold.

## Where projects live

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

Each project folder is a waypoint. In a git repo, it's generally worth keeping `waypoints/` under version control. The full rules are in [`conventions.md`](conventions.md).

## Develop

Run `claude --plugin-dir /path/to/waypoint` to try local changes. Keep the skills short; [`CLAUDE.md`](CLAUDE.md) has the house rules.

## License

[MIT](LICENSE)

---

Built by Kjartan Thorisson. Waypoint is made better with [oSimian](https://osimian.com).
