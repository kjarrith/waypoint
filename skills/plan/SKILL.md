---
name: plan
description: "Optional phase 3 of The Way: break a complex project into ordered, checkable steps. Use when the user invokes /theway:plan, or when a Way project's gap.md recommends a plan."
---

# Plan

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

A plan is only worth writing for projects that meet the bar in `conventions.md`. If this one doesn't, say so and suggest `/theway:work`.

## 1. Propose the shape

Read `intent.md` and `gap.md`. Before writing any detail, propose the structure in chat: the workstreams if there is more than one, what each needs from the others, and the order. Get the user's agreement first, because reshaping a sketch is cheap and reshaping a detailed plan isn't.

## 2. Write plan.md

Match the depth to the project. A simple plan is just a checklist of steps.

```markdown
# Plan: {Project name}

Status: Draft

## Approach
{Two to four sentences: the shape of the work and the key ordering decisions.}

## Steps
- [ ] **1. {Step name}**
  - Deliverable: {a specific, nameable output}
  - Closes: {gap titles from gap.md}
  - Done when: {yes/no checks, traced to the success criteria in intent.md}
  - Owner: {only when it isn't the agent with the user: the user alone, or someone else}
  - Needs: {earlier steps or outside inputs, if any}

## Risks
- {Risk, and what you'd do about it.}
```

Group the steps under `## Workstream: {name}` headings only when there is more than one workstream. Size each step for one focused session with a deliverable you can name and checks you can verify. The same change across many targets is one step with a checklist, not many steps. Mark later steps as provisional when they are.

## 3. Approve

Walk the user through the shape and the key decisions. Revise until they approve, then set `Status: Approved` and point to `/theway:work`.
