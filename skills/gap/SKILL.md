---
name: gap
description: "Phase 2 of Waypoint: research the distance between today and an approved intent, as a brief for the agent that will do the work. Use when the user invokes /waypoint:gap, or wants a gap analysis for a waypoint with an approved intent.md."
---

# Gap

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Gap is the homework of the agent that will execute the intent. You research what exists and write `gap.md`, a brief for whoever plans and does the work. The user doesn't review that brief. What they need from this phase is anything you found that could change the intent or the route, and the call on what happens next. Keep their time to the start and the end.

## 1. Orient

Read `intent.md`. Before the deep dive, find out from the user which sources are likely to be worth your time. Ask whatever this project calls for, such as where the relevant work, systems and documents live, who has context, or what has been tried before. Keep it brief: the user can skip it and let you find things yourself.

## 2. Research

Investigate on your own, scoped by the intent. Hand broad reading to subagents, so the raw material stays out of your context and you keep the conclusions. Back every claim with evidence you actually saw: a file path, URL, metric, document, or something the user said.

Save your questions for the end instead of interrupting. The one exception: if a finding undermines the intent's premise, stop and tell the user right away.

## 3. Write gap.md

```markdown
# Gap: {Project name}

## Summary
{Two or three sentences for the user: where things stand and how big the work is.}

## What this changes
{For the user. Each finding that could have a non-trivial impact on intent.md, each route choice that needs the user's call, and each question you couldn't answer, with its evidence and, once decided, the user's decision. If nothing came up, say so.}

---

## What exists
{What's already in place that matters, with evidence. Organize it in whatever way fits the domain.}

## Gaps
### {Short title}
- **Intent:** {the part of intent.md this serves}
- **Today:** {the current state, with evidence}
- **Needed:** {what closes the gap}
- **Size:** {small | medium | large}

## Already satisfied
- {An intent item that is already met, with evidence.}

## Risks
- {Risk, and what it could change.}

## Next steps
1. {What to do, in order, noting dependencies.} Closes: {gap titles}

**Recommendation:** {Go straight to /waypoint:work, or /waypoint:plan first, and why.}

## Sources
- {Path, URL, document or person.}
```

Everything below the rule is the brief for the executing agent. Recommend a plan only when the project meets the bar in `conventions.md`; otherwise the next steps are the plan.

## 4. Brief the user

This replaces approval. Give the summary, then go through What this changes. For a finding that affects the intent, the user decides, and if the intent changes, update `intent.md` as `conventions.md` describes. Record their decisions in `gap.md`.

End with your recommendation, plan first or straight to work and why, and wait for the user's go, even when nothing changed.
