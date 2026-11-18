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

`plan.md` has two readers. The top is for the user: plain narrative they can sanity-check in a minute, with no file paths and no tables. Below the rule is the detail for the agent that does the work, with every path, link and decision it needs. Match the depth of the detail to the project; a simple plan is a short checklist.

```markdown
# Plan: {Project name}

Status: Draft

## The plan in brief
{One short paragraph per stage or workstream, in plain words: what happens, who does what, and why it comes in this order. No status here: this section changes only when the plan changes.}

**What you're agreeing to:** {the ordering and the decisions the user is signing off on.}

**If things slip:** {the risks most likely to change the plan, and the fallback for each.}

## Where it stands
{A few sentences in the same plain words: what's done, who or what we're waiting on, and what comes next.}

---

## For the executing agent

### Steps
- [ ] **1. {Step name}**
  - Deliverable: {a specific, nameable output}
  - Closes: {gap titles from gap.md}
  - Done when: {yes/no checks, traced to the success criteria in intent.md}
  - Owner: {only when it isn't the agent with the user: the user alone, or someone else}
  - Needs: {earlier steps or outside inputs, if any}

### Risks
- {Risk, and what you'd do about it.}
```

Group the steps under `### Workstream: {name}` headings only when there is more than one workstream. Size each step for one focused session with a deliverable you can name and checks you can verify. The same change across many targets is one step with a checklist, not many steps. Mark later steps as provisional when they are.

## 3. Approve

Walk the user through the plan in brief; they approve that, not the agent's detail. Revise until they approve, then set `Status: Approved` and point to `/theway:work`.
