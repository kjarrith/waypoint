---
name: reflect
description: "Phase 5 of The Way: review a finished project against its intent and capture learnings. Use when the user invokes /theway:reflect, or wants to close out a Way project whose work is done."
---

# Reflect

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Look back: did the project achieve its intent, what worked, what should change, and what comes next. You bring the facts and a first draft; the user brings the judgment. Write for a user who may come back cold.

Reflect can run in two stages, because outcomes often take days or weeks to show. Stage 1 runs right after work, in the session that did it, while the detail of how the project ran is still at hand. Anything that needs time goes into an Outcome check that stage 2 carries out later. If `reflection.md` already has a pending Outcome check, go straight to Stage 2 below.

## 1. Gather

Read `intent.md`, `gap.md` and `plan.md` if they exist, and `work.md`. Rate each success criterion as met, partly met, not met, or not yet measurable when the result needs time to show, with evidence, and check which gaps closed. Note how the plan and the intent changed along the way, and any themes that kept coming up. Collect what `work.md` logged as found but not fixed, and put each under Next or mark it dropped.

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
- [ ] {Criterion}: not yet measurable. See Outcome check.

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

## Outcome check
### {YYYY-MM-DD}: {early check | full measurement} · pending
- {Criterion}: {what to measure, where the data lives and how to read it, and what counts as met.}
```

Park new ideas in `index.md`. Include the Outcome check only if some criterion isn't measurable yet, and write it for an agent that has nothing but the repo and its connectors. Give it dated checkpoints: usually an early one that only checks the mechanism fired at all, so a dead one is caught in days rather than weeks, then the full measurement once the result can show.

## 3. Talk

Show the user the draft and talk it through, following their energy rather than a checklist, for as long as they want; one exchange can be enough. Does the assessment match their sense of how it went? What worked? What would they change? What ideas came up? Push for specifics: "it went well" isn't a learning.

Ask whether anything outside the project, such as docs, tools or processes, should be updated to reflect what was done. Do the small ones now and list the rest under Next. Revise the draft with what you hear.

## 4. Approve

Revise until the user approves, then set `Status: Approved`.

If there is an Outcome check, check that `way-docs/` is committed and pushed. If you can schedule one-off agent runs here, offer one per checkpoint, each with a prompt that only points to this file's Outcome check. A scheduled run reaches only what's pushed and the connectors it has. If some evidence needs access only a local session has, such as credentials on the user's machine, schedule the run anyway for what it can reach, and have it end by messaging the user its findings and a ready-to-paste prompt for a local session that does the rest. Never move credentials into a scheduled run's environment to make it work. If you can't schedule runs, or the user declines, tell them when to run `/theway:reflect` again.

## Stage 2: Outcome check

Carry out the earliest pending checkpoint in the Outcome check in `reflection.md`: measure each item and append a `## Outcomes ({YYYY-MM-DD})` section with each result, its evidence, and whether the criterion is now met, partly met or not met. If part of it needs access you don't have, do the rest, and give the user your findings with a ready-to-paste prompt for a local session that finishes it. Leave stage 1 as it is, apart from marking that checkpoint done. Park new ideas in `index.md`, commit the way the repo's conventions say, and tell the user what you found. This stage needs no approval. If something still can't be measured, say why and propose a new due date rather than guessing.
