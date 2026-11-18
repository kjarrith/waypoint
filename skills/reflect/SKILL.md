---
name: reflect
description: "Phase 5 of The Way: review a finished project against its intent and capture learnings. Use when the user invokes /theway:reflect, or wants to close out a Way project whose work is done."
---

# Reflect

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Look back: did the project achieve its intent, what worked, what should change, and what comes next. You bring the facts and a first draft; the user brings the judgment. Write for a user who may come back cold.

## 1. Gather

Read `intent.md`, `gap.md` and `plan.md` if they exist, and `work.md`. Rate each success criterion as met, partly met or not met, with evidence, and check which gaps closed. Note how the plan and the intent changed along the way, and any themes that kept coming up. Collect what `work.md` logged as found but not fixed, and put each under Next or mark it dropped.

## 2. Write the draft

```markdown
# Reflection: {Project name}

Status: Draft

## Outcome
{Two or three sentences on whether the intent was achieved, including the user's view once you've talked.}

## Success criteria
- [x] {Criterion}: met. {Evidence.}
- [~] {Criterion}: partly met. {What's there and what's missing.}
- [ ] {Criterion}: not met. {Why.}

## Gaps
- [x] {Gap title}: closed. {By which step.}
- [ ] {Gap title}: still open. {Why, and what it would take.}

## What worked
- {Thing}: {why it worked}

## What to change
- {Thing}: {what to do differently next time}

## Learnings
- {About the process, the domain, or the user's preferences: anything a future project can use.}

## Next
- {Follow-ups, updates needed elsewhere, things work found but didn't fix, or new projects.}
- {Something work found that isn't worth doing: dropped, and why.}
```

Park new ideas in `index.md`.

## 3. Talk

Show the user the draft and talk it through, following their energy rather than a checklist, for as long as they want; one exchange can be enough. Does the assessment match their sense of how it went? What worked? What would they change? What ideas came up? Push for specifics: "it went well" isn't a learning.

Ask whether anything outside the project, such as docs, tools or processes, should be updated to reflect what was done. Do the small ones now and list the rest under Next. Revise the draft with what you hear.

## 4. Approve

Revise until the user approves, then set `Status: Approved`.
