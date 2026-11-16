---
name: gap
description: "Phase 2 of The Way: map the distance between today and an approved intent, ending with next steps. Use when the user invokes /theway:gap, or wants a gap analysis for a Way project with an approved intent.md."
---

# Gap

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Map the distance between where things are today and what `intent.md` describes, concretely enough that the work can start.

## 1. Orient

Read `intent.md`. Before exploring, ask the user where the relevant things live: existing work, systems, documents, people, earlier attempts. They know things you can't see. Probe for what they didn't mention: "Is that the only place?", "Has this been tried before?", "Who else has context?"

## 2. Research

Investigate what exists, scoped by the intent. Hand broad reading to subagents, so the raw material stays out of your context and you keep the conclusions. Ask the user as soon as you hit something only they can answer, rather than saving questions up. Back every claim with evidence you actually saw: a file path, URL, metric, document, or something the user said.

## 3. Write gap.md

```markdown
# Gap: {Project name}

Status: Draft

## Summary
{Three to five sentences: where things stand, the biggest gaps, the overall size of the work.}

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

## Risks and unknowns
- {Risk or unknown, and what it could change.}

## Next steps
1. {What to do, in order, noting dependencies.} Closes: {gap titles}

**Recommendation:** {Go straight to /theway:work, or /theway:plan first, and why.}

## Sources
- {Path, URL, document or person.}
```

Recommend a plan only when the project meets the bar in `conventions.md`. Otherwise the next steps above are the plan.

## 4. Approve

Walk the user through the gaps and the recommendation. Revise until they approve, then set `Status: Approved` and name the next step.
