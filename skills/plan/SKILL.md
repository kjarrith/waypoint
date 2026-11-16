---
name: plan
description: Decompose a project into an actionable, workstream-based plan with steps and handoff gates. Use when the user says 'plan', 'make a plan', 'what should we build', 'decompose the gaps'. This is Phase 3 of the value creation metaprocess — turning the gap analysis into ordered, agent-sized steps.
---

# Planning Session

This is the third of five steps in "The Way", an agent-human collaboration framework. The user has an approved intent document and an approved gap analysis. The goal is to decompose the gaps into a hierarchical plan: workstreams containing steps, with explicit handoff gates between workstreams.

Act as a systems thinker — someone who sees structure in complexity, finds natural groupings, and sequences work so that dependencies flow cleanly. Your job is to turn "here are the gaps" into "here's what to do, in what order, and how to know each piece is done."

The output of this session is `plan.md` — a workstream-based plan that the build and evaluate skills will consume in Phase 4.

## Setup

1. Locate the project:
   - If the user specifies a project name, scan `way-docs/` for directories matching `*-{project-name}`
   - If not, scan `way-docs/` for directories with `loop-state.md` showing Phase 2 complete
   - If multiple projects match, ask the user which one
   - If no projects exist or none have completed Phase 2, tell the user to run `/gap` first

2. Validate readiness:
   - Read `loop-state.md` — confirm Phase 2 is complete
   - Read `phase-1-intent/intent.md` — confirm status is `Approved`
   - Read `phase-2-gap/gap-analysis.md` — confirm status is `Approved`
   - If either is not approved, tell the user and suggest completing the missing phase

3. Read both documents in full. These are your inputs — the intent defines what good looks like and the gap analysis defines what's missing.

4. Initialize or update the project-level working memory file at `working-memory.md` (project root):
   ```markdown
   # Working Memory — {project-name}
   Last updated: {currentDate}

   ## Design Reasoning
   Intent summary: {2-3 sentence summary of intent.md, in your own words — forces internalization}
   Gaps summary: {Numbered list of gaps from gap-analysis.md, each with a 1-sentence summary}
   {will be populated during Analysis — complexity assessment, workstream design rationale}

   ## Research Progress
   {will be populated if planning requires further research}

   ## Open Threads
   {will be populated as questions or blockers arise}
   ```
   Note: If `working-memory.md` already exists from Phase 2, update the Design Reasoning with intent/gap summaries and clear any stale Research Progress entries. Preserve Human Context from earlier phases.

5. Create the Phase 3 directory: `mkdir -p {project-dir}/phase-3-plan/`

6. Initialize the plan file at `phase-3-plan/plan.md`:
   ```markdown
   # Plan — {project-name}
   Date: {currentDate}
   Intent: `phase-1-intent/intent.md`
   Gap Analysis: `phase-2-gap/gap-analysis.md`
   Status: Draft

   ---
   ```

7. Update `loop-state.md`:
   ```markdown
   **Current phase:** 3 — Planning
   **Current stage:** Analysis
   **Status:** in-progress
   **Last updated:** {currentDate}
   ```

## Stage 1: Analysis (agent-driven)

Read the intent and gap analysis carefully. Your goal is to see the structure hiding in the gaps.

### 1. Assess project complexity

How many gaps? How do they relate? Write to working memory under **Design Reasoning > Complexity Assessment**:

```markdown
### Complexity Assessment
**Level:** {simple | moderate | complex}
**Reasoning:** {2-3 sentences: what drives this assessment}
**Implications:** {how this affects plan depth — e.g., "Single workstream, 3-5 steps, no sub-steps needed" or "Multiple workstreams with dependencies, gates needed between them"}
```

Guidance:
- **Simple**: 1-3 gaps, mostly independent, clear path from gap to solution. One workstream, a handful of steps.
- **Moderate**: 3-6 gaps, some dependencies, 2-3 natural groupings. Multiple workstreams with a few handoff gates.
- **Complex**: 6+ gaps, significant interdependencies, multiple workstreams that co-evolve. Detailed handoff gates, possibly sub-steps within large steps.

### 2. Identify natural workstreams

Look for gaps that cluster together — shared concerns, sequential dependencies, or parallel tracks. Write your reasoning to working memory under **Design Reasoning > Workstream Design**:

```markdown
### Workstream Design

#### Candidate workstreams
1. **{name}**: Groups gaps {X, Y}. Rationale: {why these belong together}
2. **{name}**: Groups gaps {Z}. Rationale: {why this is separate}

#### Dependencies between workstreams
- {Workstream A} must produce {specific thing} before {Workstream B} can start {specific activity}
- {Workstream C} can run in parallel with {Workstream A}

#### Handoff gates
- **{A} → {B}**: {what B needs from A, and how to know it's ready}

#### Open questions
- {anything that needs research or human input before finalizing structure}
```

### 3. Research if needed

If structuring the plan requires investigation (evaluating approaches, comparing options, checking feasibility), do it now. Use whatever research tools are available — search files, read documents, look things up online, delegate to subagents for deeper exploration.

Log findings in working memory under **Research Progress**:

```markdown
### Research {N}: {topic}
**Question:** {what needed answering}
**Finding:** {what you learned}
**Impact on plan:** {how this affects workstream structure or step design}
```

If no research is needed, skip this step.

### Transition to Structuring

When you have a clear picture of the workstreams, dependencies, and handoff gates:

> "I've analyzed the {N} gaps and I'm seeing {N} workstreams. Here's the structure I'm thinking — let me walk you through it before I detail the steps."

## Stage 2: Structuring (1-2 exchanges with the human)

Present your proposed workstream structure. This is a lightweight alignment check — get the human to confirm the architecture before you invest time in detailed step decomposition.

### Present the structure

For each proposed workstream, share:
- **Name and purpose** — what it accomplishes
- **Gaps it addresses** — mapped back to gap-analysis.md
- **Handoff gates** — what it needs from other workstreams, what it provides

Also share:
- **Overall execution flow** — which workstreams are sequential, which can be parallel
- **Complexity assessment** — how deep you plan to go

Use `AskUserQuestion`. Something like:

> "Does this structure make sense? Should any workstreams be merged, split, or reordered? Any gaps that I've grouped wrong?"

For simple projects (one workstream), keep this brief:

> "This is a straightforward project. I'm thinking one workstream with {N} steps covering all {N} gaps. Sound right?"

### Handle feedback

If the human wants changes:
- Update working memory with their feedback
- Adjust workstream design
- Re-present if changes are significant

### Update loop state

```markdown
**Current stage:** Decomposition
```

## Stage 3: Decomposition (agent-driven)

Now write the full plan. Re-read working memory before starting — your analysis and the human's structural feedback are in there.

### For each workstream:

#### 1. Define the steps

Break the workstream into concrete steps. Each step should be:
- **Completable in a single focused session** — not so big the owner loses track, not so small that the evaluation overhead exceeds the value
- **Clearly deliverable** — a specific, nameable output (a document, a working feature, a process definition, a design, a decision record — not a vague activity)
- **Evaluable** — criteria derived from intent.md that an evaluator can check yes/no
- **Owned** — it's clear who does the work. Many steps will be agent+human (the default), but some may require other people or teams. Surface this explicitly rather than assuming the agent handles everything.

**Batch similar work into one step.** When multiple gaps require the same type of change across different artifacts (e.g., the same language update applied to 5 files, or the same process change across 3 teams), group them into a single step with a checklist — not separate steps that each require their own approval cycle. The evaluation overhead of separate steps is only justified when the work is genuinely different in nature, not just different in target. A step like "Apply X change across artifacts A, B, C, D, E" with clear per-artifact criteria is better than five steps that each repeat the same pattern.

For each step, consider who is best positioned to do the work:
- **Agent + human** (default): The agent produces the deliverable, the human reviews and approves. Most software, writing, analysis, and design work falls here.
- **Human-led**: The human does the work (a conversation, a negotiation, a decision that requires authority). The agent supports by preparing materials, tracking progress, and evaluating outcomes.
- **External party**: Someone outside the agent+human pair does the work (a hiring manager conducts interviews, a legal team reviews contracts, a vendor delivers a service). The agent tracks the dependency and helps the human coordinate.

Not every step needs an explicit owner — when it's agent+human, that's the default. But when a step requires someone else, flag it clearly so the work phase knows to handle it as a coordination task rather than a build task.

#### 2. Write evaluation criteria carefully

Evaluation criteria per step are critical — they're what the evaluator agent uses in Phase 4. They come from intent.md success criteria but need to be made specific to the step's deliverable.

Vague: "Good quality output"
Specific (software): "API endpoint returns valid JSON, handles the 3 error cases defined in intent, and includes rate limiting"
Specific (hiring): "Job description includes role responsibilities, required qualifications, and compensation range as defined in intent"
Specific (content): "Article covers all 4 key themes from intent, is under 2000 words, and includes a clear call-to-action"

Every criterion should be yes/no checkable by an agent looking at the deliverable.

#### 3. Define handoff gates

For workstreams that depend on others, specify exactly what's needed:
- What deliverable or decision from the upstream workstream?
- Which step produces it?
- How to know it's ready?

Keep gates concise but specific. "Content done" is too vague. "Approved messaging hierarchy and key copy for hero, features, and CTA sections (Workstream 1, Step 2)" is actionable.

#### 4. Apply proportional depth

Match depth to complexity:
- **Simple steps**: One-liner deliverable, 1-2 evaluation criteria
- **Medium steps**: Detailed deliverable, 2-4 evaluation criteria
- **Complex steps**: Detailed deliverable with sub-steps that break it into smaller pieces, 3-5 evaluation criteria

Sub-steps are optional — only use them when a step is large enough to benefit from internal decomposition. They give the builder a roadmap within the step without creating separate plan entries.

### Write plan.md

Write the full plan to `phase-3-plan/plan.md` using this format:

```markdown
# Plan — {project-name}
Date: {date}
Intent: `phase-1-intent/intent.md`
Gap Analysis: `phase-2-gap/gap-analysis.md`
Status: Draft

---

## Summary
{2-4 sentences: overall approach, number of workstreams, key sequencing decisions}

## Workstreams

### Workstream 1: {name}
**Purpose:** {1-2 sentences — what this workstream accomplishes}
**Gaps addressed:** {list from gap-analysis.md}
**Handoff gates:** None

#### Step 1: {name}
- **Deliverable:** {specific output — name the artifact, document, feature, or outcome}
- **Owner:** {agent+human | human-led | external: {who} — omit if agent+human (the default)}
- **Evaluation criteria:**
  - [ ] {criterion — yes/no checkable, derived from intent.md}
  - [ ] {criterion}
- **Escalation triggers:** {when to stop and involve the human}
- **Dependencies:** none
- **Scope:** {small | medium | large}

#### Step 2: {name}
- **Deliverable:** ...
- **Owner:** ...
- **Sub-steps:** {optional — only for steps large enough to benefit}
  1. {sub-step description}
  2. {sub-step description}
- **Evaluation criteria:** ...
- **Escalation triggers:** ...
- **Dependencies:** Step 1
- **Scope:** ...

### Workstream 2: {name}
**Purpose:** ...
**Gaps addressed:** ...
**Handoff gates:**
- Requires from Workstream 1: {specific deliverable or decision} (Step {ref})

#### Step 1: {name}
...

## Execution Sequence
{Ordered list showing the recommended build sequence. Note which workstreams/steps can run in parallel.}
1. {first — why it goes first}
2. {next — what it depends on}
...

## Risks
- {risk: what could go wrong, impact, suggested mitigation}

## Progressive Commitment
- **Firm:** {workstreams/steps that are well-understood and ready to build}
- **Provisional:** {likely correct, may adjust based on earlier outcomes}
- **Directional:** {rough shape only, will be refined as the project progresses}
```

### Transition to Review

> "The plan is drafted. {N} workstreams, {N} total steps. Take a look — I'll walk you through the key decisions."

## Stage 4: Review (human approval)

### 1. Present the plan

Walk the human through:
- The overall structure and why you organized it this way
- Key sequencing decisions and any trade-offs
- Where you applied proportional depth (what's detailed vs. light)
- What's in the Progressive Commitment categories

Use `AskUserQuestion`:

> "Does this plan feel right? Any steps to add, remove, restructure, or re-scope? Pay special attention to the handoff gates — those define when downstream work can begin."

### 2. Handle feedback

If the human has changes:
- Update `plan.md` with their input
- If changes are structural (workstream reorganization), update working memory too
- Re-present changed sections

### 3. Handle intent revisions

If planning reveals the intent should change (e.g., "seeing the decomposition, I realize we should also do X"):

> "That's a scope change — let's update the intent document deliberately rather than just adding it to the plan."

- Update `phase-1-intent/intent.md` with the revision and add to Revision History
- Assess whether the gap analysis needs updating
- Adjust the plan to reflect the revised intent

### 4. Lock the plan

When the user approves:
- Update status in `plan.md` from `Draft` to `Approved`
- Update `loop-state.md`:
  ```markdown
  # Loop State — {project-name}

  **Current phase:** 3 — Planning
  **Current stage:** Complete
  **Status:** phase-complete
  **Last updated:** {currentDate}

  ## Phase 1 Summary
  - Intent document: `phase-1-intent/intent.md` (Approved)

  ## Phase 2 Summary
  - Gap analysis: `phase-2-gap/gap-analysis.md` (Approved)

  ## Phase 3 Summary
  - Plan: `phase-3-plan/plan.md` (Approved)
  - Working memory: `working-memory.md`
  - Workstreams: {N}
  - Total steps: {N}
  - Intent revised: {yes/no}

  ## Next
  Phase 4 — Work (`/theway:work`)
  ```

### 5. Close the session

> "Plan locked. {N} workstreams, {N} steps. The work phase will execute these in order, with evaluation after each step. Next step whenever you're ready: `/theway:work`."

Confirm the file locations.

## Resuming a Session

If the user runs `/plan` and Phase 3 work already exists:

1. Read `loop-state.md` to determine where they left off
2. Read `working-memory.md` (project root) in full — this has your analysis and design reasoning
3. Resume at the appropriate stage:
   - If working memory has upstream summaries but no workstream design → resume at Stage 1 (Analysis)
   - If workstream design exists but plan.md is just the header → resume at Stage 2 (Structuring) or Stage 3 (Decomposition)
   - If plan.md has full content but status is Draft → resume at Stage 4 (Review)
4. Tell the user where you're picking up:
   > "I see you started planning on {date}. You got through {stage}. Want to pick up where you left off?"

## Principles

- **Structure follows gaps, not convention.** Don't impose a multi-workstream structure on a simple project. If one workstream covers everything, use one workstream. The format is always hierarchical, but depth is proportional.
- **Handoff gates are contracts.** They define the minimum viable input for a downstream workstream to begin. Be specific: name the deliverable, name the step that produces it, name the criteria for "ready." Vague gates are useless gates.
- **Steps are agent-sized.** Each step should be completable in a single focused agent session. If you can't describe the deliverable specifically, the step is too big. If the evaluation criteria are trivial, the step is too small. If multiple steps follow the same pattern on different targets, they're probably one step with a checklist.
- **Evaluation criteria come from intent.** Every step's criteria should trace back to intent.md success criteria, made specific to the deliverable. If a step has criteria that don't connect to the intent, either the step is unnecessary or the intent is incomplete.
- **Progressive commitment is honest uncertainty.** Don't mark all steps as "firm" to look confident. Later steps are genuinely less certain — that's expected, not a weakness.
- **Write after every exchange.** Working memory and plan.md get updated after each interaction. If the session crashes, all prior work is preserved.
- **The human shapes the structure.** You propose, they adjust. Don't skip the Structuring stage — getting workstream alignment before detailing steps saves rework.
- **Plans are living documents.** The approved plan is a starting point. Phase 4 will surface realities that change it. That's expected, not a failure.
