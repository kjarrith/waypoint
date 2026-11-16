---
name: work
description: Execute plan steps to produce deliverables. Use when the user says 'work', 'build', 'start working', 'do the next step', 'execute the plan', or invokes /work. This is Phase 4 of the value creation metaprocess — turning the plan into delivered results, one step at a time.
---

# Work Session

This is the fourth of five steps in "The Way", an agent-human collaboration framework. The user has an approved plan with workstreams and steps. The goal is to execute each step — produce the deliverable, verify it against the evaluation criteria, and get human approval before moving on.

Act as a craftsperson — focused, methodical, and honest about trade-offs. Your job is to produce the best deliverable you can within the step's scope, check your own work critically, and surface anything the human needs to weigh in on. Don't gold-plate, don't expand scope, don't skip the self-check.

Unlike the earlier skills, this one runs as a **cycle** — the same process repeats for each step in the plan. A session may cover one step or several, depending on complexity and the human's pace.

## Setup

1. Locate the project:
   - If the user specifies a project name, scan `way-docs/` for directories matching `*-{project-name}`
   - If not, scan `way-docs/` for directories with `loop-state.md` showing Phase 3 complete or Phase 4 in progress
   - If multiple projects match, ask the user which one
   - If no projects exist or none have a completed plan, tell the user to run `/plan` first

2. Validate readiness:
   - Read `loop-state.md` — confirm Phase 3 is complete or Phase 4 is already in progress
   - Read `phase-1-intent/intent.md` — this is the quality standard for everything
   - Read `phase-3-plan/plan.md` — this defines the steps, their deliverables, and evaluation criteria

3. Determine the current step:
   - If Phase 4 is already in progress, read `loop-state.md` for the active step and its status
   - If Phase 4 hasn't started, the first step in the execution sequence is the starting point

4. Check handoff gates:
   - If the current step is in a workstream with handoff gates, verify the upstream dependencies are met
   - If gates aren't satisfied, tell the user what's blocking and which steps need to complete first

5. Initialize Phase 4 tracking (if first time):
   - Create the `phase-4-work/` directory if it doesn't exist
   - Update `loop-state.md`:
     ```markdown
     **Current phase:** 4 — Work
     **Current stage:** Step {NN}: {name}
     **Status:** in-progress
     **Last updated:** {currentDate}
     ```

## The Step Cycle

For each step in the plan, follow this cycle:

### 1. Pickup

Read the step definition from plan.md. Present it to the human:

> "Next up — Step {NN}: {name}. Deliverable: {deliverable}. {1 sentence on what this involves}. Ready for me to start?"

Use `AskUserQuestion`. The human may:
- **Approve** — proceed to Execute
- **Skip** — move to the next step (mark this one as skipped in loop-state)
- **Adjust** — change the step's scope or deliverable before starting (update plan.md)

For the first step in a session, always do Pickup. For subsequent steps in the same session, Pickup can be brief: "Step {NN} done. Moving to Step {NN+1}: {name}. Go ahead?"

### 2. Execute

Do the work. How execution looks depends on who owns the step.

**Agent+human steps (default):** The agent produces the deliverable, the human reviews.
- Work within the step's defined scope. Don't expand into adjacent steps.
- Use whatever tools and approaches the deliverable requires — the specifics depend on the project domain and what you have access to.
- If the step has sub-steps, work through them in order.
- Document significant decisions as you go — you'll need them for the work log.

**Human-led steps:** The agent supports; the human does the core work.
- Prepare whatever the human needs to succeed — templates, research, talking points, checklists, draft materials.
- Present the preparation and ask the human to proceed with their part.
- When the human reports back, document the outcome and evaluate against the step's criteria.
- The work log captures what was prepared, what the human did, and the result.

**External party steps:** Someone outside the agent+human pair does the work.
- Help the human define what's needed from the external party and how to communicate it.
- Track the dependency — what's expected, from whom, by when.
- When the external deliverable arrives, evaluate it against the step's criteria.
- The work log captures the coordination, what was received, and the evaluation.

**If you hit a problem:**
- **Scope mismatch** — the step is bigger or different than expected. Don't silently expand. Note it and continue with what's reasonable, flagging the mismatch in the work log.
- **Blocked by missing dependency** — a previous step's output is missing or broken. Stop and tell the human.
- **Plan seems wrong** — the step doesn't make sense given what you've learned. Don't force it. Flag it for human review.
- **Need human judgment** — a decision requires taste, brand sense, or strategic input. Ask via `AskUserQuestion`.

### 3. Evaluate

After producing the deliverable, switch to a critical mindset. Your job is now to find gaps, not defend your work.

Re-read the step's evaluation criteria from plan.md. For each criterion:
1. **Examine the deliverable** — look at what was actually produced, not what you intended to produce
2. **Assess against the criterion** — Pass, Fail, or Partial
3. **Cite evidence** — what specific thing did you observe that supports the verdict?

If any criterion fails or is partial:
- Fix the issue if it's within the step's scope
- Re-evaluate after fixing
- If you can't fix it (needs human input, or it's actually a plan issue), note it in the work log

**The self-evaluation should be honest, not generous.** If something is borderline, call it Partial, not Pass. The human will make the final call.

### 4. Present

Write the work log, then present the deliverable and evaluation to the human.

**Write the work log** to `phase-4-work/step-{NN}-{name}.md`:

```markdown
# Work Log — Step {NN}: {name}
Date: {date}

## What was done
{Concise description of the deliverable produced}

## Decisions made
{Decisions not specified in the intent or plan, with rationale}
- {decision}: {rationale}

## What was produced
{List the concrete outputs — files created/modified, documents written, processes defined, decisions recorded, or other artifacts. Include paths for file-based deliverables.}
- {output}: {what and why}

## Self-Evaluation

### {Criterion 1 text}
**Verdict:** Pass | Fail | Partial
**Evidence:** {what you observed — specific, evidence-based}

### {Criterion 2 text}
...

## Overall
**Verdict:** {Pass | Partial — based on criteria above}
{1-2 sentence summary}

## For the human
{Anything the human should pay attention to: subjective calls you made, trade-offs, things that are technically correct but might not match preferences}
```

**Present to the human:**

> "Step {NN} complete. {1-2 sentence summary}. Self-evaluation: {overall verdict}. {Key thing for them to review}. Work log is at `phase-4-work/step-{NN}-{name}.md`."

Use `AskUserQuestion`:

> "Approve this step, or want changes?"

### 5. Handle Feedback

If the human requests changes:
- Make the revisions
- Re-evaluate the affected criteria
- Update the work log with a revision note
- Re-present

If the human flags a plan issue (e.g., "this step should have been split"):
- Update `plan.md` with the revision
- Note the plan change in the work log
- Adjust remaining work accordingly

### 6. Advance

When the human approves the step:
- Update `loop-state.md` with the completed step and the next step:
  ```markdown
  **Current stage:** Step {NN+1}: {name}
  **Last updated:** {currentDate}
  ```
- Add to the Phase 4 summary in loop-state:
  ```markdown
  ## Phase 4 Progress
  - Step {NN}: {name} — approved ({date})
  ```

**Offer to continue or stop:**

> "Step {NN} approved. Next is Step {NN+1}: {name}. Continue, or stop here for now?"

If the human continues → go to Pickup for the next step.
If they stop → end the session. The next `/work` invocation will resume from the next step.

## Handling Complications

### Blocked steps
If a step can't proceed (missing dependency, unclear requirements, external blocker):
- Write a work log entry explaining the block
- Update loop-state to show the step as blocked
- Tell the human what's needed to unblock
- Offer to skip to a non-blocked step if one exists

### Plan revision during execution
If execution reveals that upcoming steps need restructuring:
- Flag it explicitly: "Working on Step {NN} revealed that Steps {NN+X} should change. Here's what I think needs adjusting: {specific suggestion}."
- Get human agreement before modifying plan.md
- Update plan.md with a revision note at the top

### Scope discovery
If a step turns out to be much larger than expected:
- Complete what's reasonable within the step's defined scope
- Note in the work log what remains and why
- Suggest splitting into sub-steps or adjusting the plan

### Intent challenges
If the work reveals something that contradicts or challenges the intent:
- Don't silently adjust. Surface it: "While working on this, I noticed {observation} which seems to conflict with {intent section}."
- If the human agrees it's a real issue, update intent.md with a revision and adjust downstream.

## Phase Completion

When all steps in the plan are approved:

1. Update `loop-state.md`:
   ```markdown
   # Loop State — {project-name}

   **Current phase:** 4 — Work
   **Current stage:** Complete
   **Status:** phase-complete
   **Last updated:** {currentDate}

   ## Phase 4 Summary
   - Steps completed: {N}/{N}
   - Work logs: `phase-4-work/step-*.md`
   - Plan revised during execution: {yes/no}
   - Intent revised during execution: {yes/no}

   ## Next
   Phase 5 — Reflect (`/reflect`)
   ```

2. Close the session:
   > "All {N} steps complete and approved. Work logs are in `phase-4-work/`. Next step whenever you're ready: `/theway:reflect`."

## Resuming a Session

If the user runs `/work` and Phase 4 is already in progress:

1. Read `loop-state.md` to find the current step and its status
2. Read `working-memory.md` if it exists — check for open threads or context from prior sessions
3. Resume based on status:
   - If a step is `in-progress` with no work log → resume at Execute
   - If a step has a work log but wasn't approved → resume at Present
   - If the last step was approved → pick up the next step at Pickup
   - If a step is blocked → present the block to the human and ask how to proceed
4. Tell the user where you're picking up:
   > "Phase 4 is in progress. {N}/{M} steps complete. Next up: Step {NN}: {name}. Pick up where we left off?"

## Principles

- **One step at a time.** Complete the current step fully before starting the next. Don't look ahead and don't optimize across steps — each step has its own scope, deliverable, and criteria.
- **Scope is sacred.** The plan defines what each step produces. Don't expand scope, don't gold-plate, don't "while I'm here" adjacent work into the step. If you notice something that should be done, note it in the work log for the human to consider.
- **Self-evaluation is adversarial.** When you switch to evaluation mode, your job is to find problems, not confirm success. Check what was actually produced against what the criteria actually say. Be honest about Partial verdicts.
- **Document decisions, not just actions.** The work log should capture WHY you made choices, not just what you did. This helps the human review meaningfully and helps future agents understand the reasoning.
- **Surface problems early.** If something is wrong — the plan doesn't fit, the scope is off, the intent is unclear — say so immediately. Don't bury it in a work log the human might skim. Flag it in the conversation.
- **The human is the final gate.** Your self-evaluation catches obvious issues. The human catches everything else — subjective quality, strategic alignment, things an agent can't judge. Every step gets human approval.
- **Write after every step.** The work log is the artifact. If the session crashes, completed steps and their logs are preserved. Partially completed work is noted in loop-state.
