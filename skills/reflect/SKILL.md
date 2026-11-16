---
name: reflect
description: "Phase 5 of The Way: review a finished project against its intent and capture learnings. Use when the user invokes /theway:reflect, or wants to close out a Way project whose work is done."
---

# Reflect

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Look back together: did the project achieve its intent, what worked, what should change, and what comes next. You bring the facts; the user brings the judgment.

## 1. Gather

Read `intent.md`, `plan.md` if there is one, and `work.md`. Rate each success criterion as met, partly met or not met, with evidence. Note how the plan and the intent changed along the way, and any themes that kept coming up. Share a short summary in chat.

## 2. Talk

Have a short conversation, two to five exchanges, following the user's energy rather than a checklist. Does the assessment match their sense of how it went? What worked? What would they change? What surprised them? What ideas came up? Push for specifics: "it went well" isn't a learning.

Ask whether anything outside the project, such as docs, tools or processes, should be updated to reflect what was done. Do the small ones now and list the rest under Next.

## 3. Write reflection.md

```markdown
# Reflection: {Project name}

Status: Draft

## Outcome
{Two or three sentences, including the user's view.}

## Success criteria
- [x] {Criterion}: met. {Evidence.}
- [~] {Criterion}: partly met. {What's there and what's missing.}
- [ ] {Criterion}: not met. {Why.}

## What worked
- {Thing}: {why it worked}

## What to change
- {Thing}: {what to do differently next time}

## Learnings
- {About the process, the domain, or the user's preferences: anything a future project can use.}

## Next
- {Follow-ups, updates needed elsewhere, or new projects.}
```

Park new ideas in `index.md`.

## 4. Approve

Revise until the user approves, then set `Status: Approved`.
