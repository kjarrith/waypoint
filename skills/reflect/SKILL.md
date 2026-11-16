---
name: reflect
description: Post-project reflection on outcomes, process, and learnings. Use when the user says 'reflect', 'what did we learn', 'wrap up', 'close the project', or invokes /reflect. This is Phase 5 of the value creation metaprocess — looking back at what happened, capturing learnings, and closing the loop.
---

# Reflect Session

This is the fifth and final step in "The Way", an agent-human collaboration framework. All work is done. The goal is to look back together — assess outcomes against the intent, capture what went well and what to change, and close the project cleanly.

Act as a thoughtful collaborator. Your job in this phase is to steer the conversation, not monologue. You bring the data (what happened, what the intent said, how criteria landed). The human brings the judgment (what mattered, what surprised them, what they'd do differently). Together you produce a reflection that's useful for future projects.

## Setup

1. Locate the project:
   - If the user specifies a project name, scan `way-docs/` for directories matching `*-{project-name}`
   - If not, scan `way-docs/` for directories with `loop-state.md` showing Phase 4 complete
   - If multiple projects match, ask the user which one
   - If no projects exist or none have completed Phase 4, tell the user Phase 4 must be complete first

2. Validate readiness:
   - Read `loop-state.md` — confirm Phase 4 status is `phase-complete`
   - Read `phase-1-intent/intent.md` — the success criteria you'll assess against
   - Read `phase-3-plan/plan.md` — the planned approach
   - Read all work logs in `phase-4-work/step-*.md`
   - Read `working-memory.md` if it exists — check for open threads or noted issues

3. Initialize Phase 5:
   - Create `phase-5-reflect/` directory if it doesn't exist
   - Update `loop-state.md`:
     ```markdown
     **Current phase:** 5 — Reflect
     **Current stage:** Gather
     **Status:** in-progress
     **Last updated:** {currentDate}
     ```

## Stage 1: Gather (agent-driven)

Build the factual picture before involving the human. This stage is your homework.

1. **Check each success criterion** — Read every success criterion from `intent.md`. For each one, trace through the work logs and deliverables to determine: Met, Partially Met, or Not Met. Cite the evidence (which step, what was produced, what the self-evaluation said).

2. **Trace the plan's evolution** — Did the plan change during execution? Were steps added, removed, reordered, or scoped differently? Were there intent revisions? Note these.

3. **Identify patterns** — Scan work logs for recurring themes: repeated blockers, scope discoveries, decisions that came up multiple times, things flagged "for the human" that turned out to matter.

4. **Write the initial reflection** to `phase-5-reflect/reflection.md`:

```markdown
# Reflection — {project-name}
Date: {currentDate}
Status: Draft

## Outcome Summary
{2-3 sentences: did we hit the target? Overall assessment.}

## Success Criteria Results
- [x] {criterion 1} — Met. {brief evidence}
- [ ] {criterion 2} — Not met. {what happened}
- [~] {criterion 3} — Partially met. {what's there, what's missing}

## Plan Evolution
{Did the plan change during execution? How and why?}

## Patterns Observed
- {pattern}: {evidence from work logs}
```

5. **Update loop-state** stage to `Reflect`.

6. **Present the assessment to the human:**

> "I've reviewed the project artifacts. Here's where we landed against the intent: {1-2 sentence summary}. {N}/{M} success criteria fully met. I've written the initial assessment to `reflection.md`. Ready to talk through it?"

## Stage 2: Reflect (collaborative, 2-5 exchanges)

This is the core of the phase — a structured conversation. You steer, the human reflects, and you capture what emerges.

### The conversation arc

Start by presenting your assessment summary, then ask the first question. Each exchange should cover one topic. After each human response, append what you learned to `reflection.md` in the conversation log section, then steer to the next topic.

**Topics to cover** (adjust order based on what feels natural):

1. **Outcome reaction** — "The success criteria landed like this: {summary}. Does that match your sense of how it went? Anything I'm reading wrong?"

2. **What went well** — "What parts of the process worked for you? Any steps or patterns you'd want to keep for future projects?"

3. **What to change** — "What felt off, slow, or frustrating? If you could change one thing about how this went, what would it be?"

4. **Surprises** — "Did anything surprise you — about the project, the process, or the results?"

5. **Next steps and new ideas** — "Any ideas that came up during this project that we should capture? Things to build on, or entirely new directions?"

You don't need to ask all five as separate questions. If the human is flowing, let them talk and cover multiple topics in one exchange. If they're brief, ask targeted follow-ups. The goal is 2-5 exchanges total, not a rigid interview.

### After each exchange

Append to `reflection.md`:

```markdown
## Conversation Log

### Exchange {N}
**Topic:** {what was discussed}
**Human said:** {key points, in their words where possible}
**Takeaway:** {what this means for the reflection}
```

### Wrapping up the conversation

When you've covered enough ground (or the human signals they're done), summarize what you heard:

> "Here's what I'm taking away: {2-3 key points}. Anything I'm missing before I write up the final reflection?"

## Stage 3: Close (collaborative)

Finalize the reflection, handle any loose ends, and close the project.

### 1. Write the final reflection

Update `reflection.md` — replace the Draft sections with the full picture, incorporating both your assessment and the human's input:

```markdown
# Reflection — {project-name}
Date: {currentDate}
Status: Final

## Outcome Summary
{Updated with human's perspective}

## Success Criteria Results
{Same as Gather, refined if the human corrected anything}

## What Went Well
- {thing}: {why it worked}

## What Would Change
- {thing}: {specific suggestion for next time}

## Learnings

### Process
- {insight about how the lifecycle worked — useful for future projects}

### Domain
- {insight about the project domain — useful for future work in this space}

### Preferences
- {insight about what the human values — useful for future intent capture}

## Plan Evolution
{Kept from Gather stage}

## Suggested Next Actions
- {what to do next — new project? iteration? nothing?}
```

Keep the Conversation Log section at the bottom as an appendix — it's valuable context but not the primary output.

### 2. Documentation check

Ask the human:

> "Quick check — is there anything related to this project (documents, tools, processes, or external resources) that should be updated to reflect what we accomplished?"

If yes, note the items. If they're small and within reach, offer to do them now. If they're external or require other people, note them in Suggested Next Actions.

### 3. Capture new ideas

If new ideas or next steps emerged during the conversation:
- Write them to `way-docs/backlog.md` with date, source project, description, and status `parked`
- Tell the human what you added

### 4. Handle intent revision proposals

If the reflection revealed that the original intent should change for future work (not retroactively — the project is done):
- Write proposed revisions to `phase-5-reflect/intent-revisions.md`:
  ```markdown
  # Intent Revision Proposals — {project-name}
  Date: {currentDate}

  ## Proposed Revisions
  - {section of intent.md}: {what should change and why}

  ## Rationale
  {Why this project's experience suggests the intent should evolve}
  ```
- Only create this file if there are actual proposals. Don't create it just because the section exists in the template.

### 5. Close the loop

Get human approval on the final reflection:

> "Reflection is written. Take a look at `reflection.md` — does it capture what matters? Ready to close this project?"

When the human approves, update `loop-state.md`:

```markdown
# Loop State — {project-name}

**Current phase:** 5 — Reflect
**Current stage:** Complete
**Status:** project-complete
**Last updated:** {currentDate}

## Phase 5 Summary
- Reflection: `phase-5-reflect/reflection.md`
- Success criteria: {N}/{M} met
- Intent revisions proposed: {yes/no}
- New backlog items: {N}

## Project Complete
All five phases finished. Learnings captured in reflection.md.
```

Close the session:

> "Project complete. Reflection is at `phase-5-reflect/reflection.md`. {If backlog items were added: '{N} new ideas added to `backlog.md`.} Thanks for seeing this one through."

## Resuming a Session

If the user runs `/reflect` and Phase 5 is already in progress:

1. Read `loop-state.md` to find the current stage
2. Read `phase-5-reflect/reflection.md` if it exists
3. Resume based on stage:
   - If stage is `Gather` with no reflection.md → restart Gather
   - If stage is `Gather` with partial reflection.md → present what's there, move to Reflect
   - If stage is `Reflect` with conversation log → summarize where you left off, continue the conversation
   - If stage is `Close` with a Draft reflection → finalize and close
4. Tell the user where you're picking up:
   > "Phase 5 is in progress. {Stage description}. Pick up where we left off?"

## Principles

- **The human's perspective is the point.** Your assessment is the starting material. The human's reaction, corrections, and insights are what make the reflection valuable. Don't treat your initial analysis as the final word.
- **Steer, don't interrogate.** This is a conversation, not a questionnaire. Adapt to what the human wants to talk about. If they're passionate about one topic, go deeper there instead of rushing through a checklist.
- **Capture concretely.** "It went well" is not a useful learning. "The workstream structure kept steps focused and prevented scope creep" is. Push for specifics in both your analysis and the human's input.
- **Write after every exchange.** Same pattern as every other skill. If the session crashes mid-conversation, the exchanges so far are preserved in the conversation log.
- **New ideas are first-class outputs.** Projects generate ideas. Capture them in the backlog. A reflection that doesn't surface any new ideas probably didn't go deep enough.
- **Close cleanly.** Update loop-state, write backlog items, check documentation. Don't leave loose threads. The project should feel finished.
