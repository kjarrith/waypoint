---
name: plan
description: "Optional phase 3 of Waypoint: break a complex project into ordered, checkable steps. Use when the user invokes /waypoint:plan, or when a waypoint's gap.md recommends a plan."
---

# Plan

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

A plan is only worth writing for projects that meet the bar in `conventions.md`. If this one doesn't, say so and suggest `/waypoint:work`.

## 1. Align before writing

Read `intent.md` and `gap.md`. Before writing any detail, agree two things with the user in chat, because changing a sketch is cheap and changing a written plan isn't:

- **The shape:** the workstreams if there is more than one, what each needs from the others, and the order.
- **The decisions the plan rests on.** Ask two questions of each: is it a one-way door (see `conventions.md`), and is there a real choice between options? If either answer is yes, bring it to the user. For a real choice, give the options, their trade-offs and your recommendation. For a one-way door, say what it commits us to, even when the choice seems obvious. Make the rest yourself and note them in the detail. Don't re-ask what the user already settled in `gap.md`.

If writing the detail turns up another decision of this kind, stop and settle it in chat before going on.

## 2. Write plan.md

`plan.md` has two readers. The top is for the user: plain narrative they can sanity-check in a minute, with no file paths and no tables. Below the rule is the detail for the agent that does the work, with every path, link and decision it needs. Match the depth of the detail to the project; a simple plan is a short checklist.

```markdown
# Plan: {Project name}

Status: Draft

## The plan in brief
{One short paragraph per stage or workstream, in plain words: what happens, who does what, and why it comes in this order. No status here: this section changes only when the plan changes.}

**Decisions:**
- {Each decision settled with the user. For a real choice: the alternatives, and why they lost. For a one-way door: mark it "One-way door" and say what it commits us to.}
- {If there are none: "One-way doors: none."}

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

Walk the user through the plan in brief; they approve that, not the agent's detail. Since the decisions were settled before writing, approval checks that the write-up matches what you agreed; it shouldn't bring up anything new. Revise until they approve, then set `Status: Approved` and point to `/waypoint:work`.
