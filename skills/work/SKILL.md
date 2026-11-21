---
name: work
description: "Phase 4 of Waypoint: carry out a project's steps one at a time, checking each and getting approval before moving on. Use when the user invokes /waypoint:work, or asks to continue the work on a waypoint."
---

# Work

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Carry out the project one step at a time: do it, check it honestly, get the user's approval, log it. `intent.md` is the quality bar for everything.

## Start

Take the steps from `plan.md`, otherwise the Next steps in `gap.md`, otherwise `intent.md`. Read `work.md`, if it exists, to see what is already done; otherwise create it:

```markdown
# Work: {Project name}

Status: In progress
```

Tell the user which step is next, and agree how often to check in: after every step (the default), or running through several before showing them.

## Each step

1. **Do it.** Stay inside the step. If it turns out bigger or different than expected, or the plan or intent looks wrong, stop and say so rather than expanding silently. If someone else owns the step, prepare what they need and follow up on what comes back. If the step depends on work outside the project, check its current state first; if it changed, say so before going on.
2. **Check it.** Switch to looking for problems. Compare what you actually produced with the step's checks and with `intent.md`, and fix what you can. For a substantial deliverable, have a subagent that didn't write it check it against the step's checks and `intent.md`. Call borderline results partial, not passed.
3. **Show it.** Write it for a user who comes back cold, so they can approve without scrolling back:
   - **The step and its definition of done**, in a line or two: what the step was for and what had to be true at the end.
   - **Where it stands**, checked in this turn: the artifact's link, its state (draft, CI result, open comments) and what is still open.
   - **What you did**, the decisions they didn't specify, and anything they should look at closely.

   End with the ask: approve it, or ask for changes.
4. **Log it.** Once it's approved, add an entry to `work.md`. If there is a `plan.md`, tick the step and rewrite its Where it stands section in the same edit, so the two never disagree. If the plan itself changed, update The plan in brief too.

```markdown
## {N}. {Step name} ({YYYY-MM-DD})
Gaps: {gap titles this step closed or moved forward; omit if the project skipped gap}
{What was produced, with paths or links. Decisions made and why. Anything left open, or found outside the step and not fixed.}
```

If you notice something worth doing outside the step, mention it and log it in the step's entry rather than doing it.

## Finish

A step that can't finish inside the project can be handed off, with the user's agreement: log where it went and the check that will prove it. Reflect rates the criteria it serves as not met.

When every step is approved or handed off, set `work.md` to `Status: Done` and offer `/waypoint:reflect`.
