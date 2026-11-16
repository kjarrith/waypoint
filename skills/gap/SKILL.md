---
name: gap
description: "Run a structured gap analysis for a project with an approved intent document. Use when the user says 'gap', 'gap analysis', 'analyze the gap', 'what's the current state', or invokes /gap. This is Phase 2 of the value creation metaprocess — mapping the delta between where we are and where the intent says we want to be."
---

# Gap Analysis Session

This is the second of five steps in "The Way", an agent-human collaboration framework. The user has already run `/intent` to create an approved intent document. The goal is to map the distance between current reality and the approved intent.

Act as an investigative analyst — thorough, systematic, and honest about unknowns. Your job is to build a complete picture of current state, compare it against every dimension of the intent document, and produce a gap map that a planning agent can decompose into steps.

You might not be able to do this alone. The human knows things you can't see — existing materials, tools, processes, relationships, business context, prior work. Your first job is to figure out what you don't know, and then go learn it.

The output of this session is `gap-analysis.md` — a gap map that makes the delta concrete, specific, and plannable.

## Setup

1. Locate the project:
   - If the user specifies a project name, scan `way-docs/` for directories matching `*-{project-name}`
   - If not, scan `way-docs/` for directories with `loop-state.md` showing Phase 1 complete
   - If multiple projects match, ask the user which one
   - If no projects exist, tell the user to run `/intent` first

2. Validate readiness:
   - Read `{project-dir}/loop-state.md` — confirm Phase 1 is complete
   - Read `{project-dir}/phase-1-intent/intent.md` — confirm status is `Approved`
   - If intent is not approved, tell the user and suggest completing `/intent` first

3. Read the full intent document carefully. This is the target you're measuring against.

4. Initialize or update the project-level working memory file at `{project-dir}/working-memory.md`:
   ```markdown
   # Working Memory — {project-name}
   Last updated: {currentDate}

   ## Human Context
   {will be populated as the human reveals context not captured in formal documents}

   ## Research Progress
   {will be populated with sources, research plan, and findings during gap analysis}

   ## Open Threads
   {will be populated as questions or blockers arise}
   ```

5. Create the Phase 2 directory: `{project-dir}/phase-2-gap/`

6. Initialize the gap analysis file at `{project-dir}/phase-2-gap/gap-analysis.md`:
   ```markdown
   # Gap Analysis — {project-name}
   Date: {currentDate}
   Intent: `phase-1-intent/intent.md`
   Status: In Progress

   ---
   ```

7. Update `loop-state.md`:
   ```markdown
   **Current phase:** 2 — Gap Analysis
   **Current stage:** Orientation
   **Status:** in-progress
   **Last updated:** {currentDate}
   ```

## Stage 1: Orientation (1-3 exchanges with the human)

You need the human to tell you what you can't see. This is the most important conversation in the gap analysis.

### Opening

Start with something like:

> "I've read the intent document. Before I start researching, I need to understand the landscape. What exists today that's related to this project? Walk me through the current state — any prior work, existing resources, tools, processes, or materials I should know about. Where does the relevant stuff live?"

Use `AskUserQuestion`. Let them talk.

### After each response:

#### 1. Update working memory

Append to `working-memory.md` under **Research Progress > Key Sources**:

```markdown
### Source {N}: {name}
- **Type:** {document | codebase | website | tool/service | process | dataset | design-asset | relationship/contact | folder | other}
- **Location:** {path, URL, or description of where/how to access it}
- **Accessible:** {yes — I can examine it | no — human will need to provide info | partial — I can see some of it}
- **Relevance:** {which intent dimensions this relates to}
- **Notes:** {anything the human said about this source}
```

#### 2. Probe for more

Don't accept the first answer as complete. Probe with:
- "What about [dimension from intent not yet covered]? Is there anything existing for that?"
- "You mentioned X — is that the only place, or is there also [likely related source]?"
- "Is there anything that used to exist but was abandoned? Sometimes dead projects have useful artifacts."
- "Who else has context on this? Any prior discussions, handoff notes, or documented decisions I should know about?"
- "Are there external services, partners, or third-party tools involved?"

#### 3. Build the research plan

After each exchange, update `working-memory.md` under **Research Progress > Research Plan**. The plan is a checklist of investigation tasks:

```markdown
### Research Plan

### Automated research (agent can do independently)
- [ ] {task — adapt to whatever the project is. Examples by domain:}
- [ ] {software: "Explore the src/ directory to understand current architecture"}
- [ ] {software: "Read package.json and dependency files for current tech stack"}
- [ ] {hiring: "Review the current job descriptions and role requirements"}
- [ ] {content: "Audit existing published articles for topic coverage and style"}
- [ ] {any domain: "Fetch and analyze [URL] for current live state"}
- [ ] {any domain: "Read [document] for background context"}

### Needs human input
- [ ] {task — things only the human can provide. Examples:}
- [ ] {"Clarify current metrics (traffic, conversion, pipeline size, etc.)"}
- [ ] {"Confirm which existing materials are approved/current vs. outdated"}
- [ ] {"Provide access to [resource] or summarize its contents"}
```

### Transition to Research

When you have a solid picture of the landscape and a research plan:

> "Here's my research plan: [summary]. I'm going to go investigate all the automated items. For the items that need your input, I'll ask you as I go. Sound good?"

Use `AskUserQuestion`. Get confirmation or adjustments before proceeding.

## Stage 2: Research (agent-driven, with human check-ins)

Execute the research plan systematically. For each task:

### 1. Do the research

Use whatever tools are available to you — the specifics depend on your environment and the project domain:
- **Files and documents**: Search for, read, and analyze any accessible files, documents, or project artifacts
- **Web research**: Look up external URLs, research best practices, analyze competitors or comparable examples
- **Live inspection**: If you can view websites, apps, or other live systems, examine them directly
- **Deep exploration**: For broad or complex research tasks, use available subagent or task delegation tools to avoid flooding your own context

Adapt your approach to the project. For a software project, you'll explore codebases, check dependencies, and read architecture docs. For a hiring project, you'll review job descriptions, existing processes, and candidate pipelines. For a content project, you'll audit existing materials, analyze publication patterns, and assess quality. Let the project tell you what to investigate.

### 2. Log findings in working memory

After each research task, append to `working-memory.md` under **Research Progress > Findings Log**:

```markdown
### Finding {N}: {short title}
**Research task:** {which task from the plan}
**What I found:** {concise summary of what exists, what state it's in}
**Relevant to:** {which intent dimensions or success criteria}
**Gap signal:** {does this suggest a gap, a non-gap, or something ambiguous?}
**Evidence examined:** {list of specific files, URLs, documents, or observations}
```

Check off completed tasks in the Research Plan as you go.

### 3. Ask the human when blocked

When you hit a "Needs human input" task or discover something that needs clarification:

> "I found [thing] while researching [area]. [Specific question]. Can you clarify?"

Don't batch these up — ask as you go. Update working memory with their answers.

### 4. Recognize when new research tasks emerge

As you investigate, you'll discover things that weren't in the original plan. Add new tasks to the Research Plan and investigate them. Update the working memory file to keep track.

### Transition to Synthesis

When the research plan is substantially complete (all automated tasks done, critical human-input tasks resolved):

> "Research is done. I've examined [N sources] and logged [N findings]. Ready for me to synthesize this into the gap map?"

## Stage 3: Synthesis (agent-driven)

Now write the gap analysis. Read `working-memory.md` in full (this is why you've been maintaining it — your context window may have lost earlier details, but the file has everything).

Write to `phase-2-gap/gap-analysis.md`:

```markdown
# Gap Analysis — {project-name}
Date: {currentDate}
Intent: `phase-1-intent/intent.md`
Status: Complete

---

## Executive Summary
{3-5 sentences: the overall picture. How far is current state from the intent? What are the biggest gaps? Any surprises?}

## Current State

### What exists today
{Structured overview of what's already in place. Organize by whatever categories fit the project — e.g., codebase/design/infrastructure for software, processes/people/tools for operations, content/channels/analytics for marketing. Let the project domain determine the structure.}

### Relevant landscape
{The broader context that matters for planning. For software: tech stack, architecture, dependencies. For hiring: market conditions, team structure, existing pipeline. For content: publication cadence, audience data, competitive landscape. Include specifics — file paths, URLs, metrics, names — whatever constitutes concrete evidence in this domain.}

### Relevant prior work
{Anything that was attempted before, abandoned efforts, existing specs or designs that relate.}

## Gap Map

{For each intent dimension where a gap exists, create a section. Skip dimensions where current state already satisfies the intent.}

### Gap: {short title}
- **Intent says:** {quote or paraphrase the relevant part of intent.md}
- **Current state:** {what exists now — be specific with evidence from research}
- **Delta:** {concrete description of what's missing or different}
- **Complexity:** {low | medium | high — based on what you learned}
- **Dependencies:** {what this gap depends on or blocks}
- **Notes:** {anything relevant — risks, alternative approaches, things the human should know}

### Gap: {next gap}
...

## Non-Gaps (Already Satisfied)
{List intent dimensions or success criteria that current state already covers. This is valuable — it shows what doesn't need work.}
- {dimension/criterion}: {why it's already satisfied}

## Risks and Unknowns
{Things that surfaced during research that could affect planning:}
- {risk: something that could go wrong}
- {unknown: something that couldn't be determined and might matter}

## Recommended Priorities
{Based on the gap analysis, suggest an order of attack. Consider dependencies, complexity, and impact on success criteria.}
1. {highest priority gap — why}
2. {next priority — why}
3. {etc.}

## Sources
{All sources examined during research, for traceability:}
- {source 1: path, URL, or description}
- {source 2: path, URL, or description}
```

**Writing principles for the gap analysis:**
- Be specific and evidence-based. Vague assessments aren't useful. Cite concrete evidence: file paths for code, URLs for web content, specific metrics for performance, named documents for processes. For example, "47 components with no shared design system" or "3 open roles with no structured interview process" — not "things are disorganized."
- Reference the specific sources you examined — files, URLs, documents, conversations with the human.
- Every gap should trace back to a specific dimension or success criterion in the intent document.
- Non-gaps are as valuable as gaps — they prevent unnecessary work in the planning phase.
- Recommended priorities are suggestions, not decisions. The human and the planning phase will finalize the order.

## Stage 4: Review (human approval)

### 1. Present the gap analysis

> "Here's the gap analysis. [N] gaps identified, [N] dimensions already satisfied. The biggest gaps are [top 2-3]. Take a look — anything I missed, got wrong, or that you want to reframe?"

Use `AskUserQuestion`. Give them space to read and react.

### 2. Handle feedback

If the user has corrections or additions:
- Update `gap-analysis.md` with their input
- If they reveal new information, add it to `working-memory.md` and investigate if needed
- Re-present changed sections

### 3. Handle intent revisions

Sometimes the gap analysis reveals that the intent should change. If the user says something like "actually, seeing the current state, I think we should adjust the goal," handle it explicitly:

> "That's a legitimate intent revision — the gap analysis is supposed to surface these. Let's update the intent document deliberately rather than just adjusting the gap analysis to fit."

- Update `phase-1-intent/intent.md` with the revision
- Add to the Revision History section
- Re-evaluate any gaps affected by the change

### 4. Lock the gap analysis

When the user approves:
- Update status in `gap-analysis.md` from `In Progress` to `Approved`
- Update `loop-state.md`:
  ```markdown
  # Loop State — {project-name}

  **Current phase:** 2 — Gap Analysis
  **Current stage:** Complete
  **Status:** phase-complete
  **Last updated:** {currentDate}

  ## Phase 1 Summary
  - Intent document: `phase-1-intent/intent.md` (Approved)

  ## Phase 2 Summary
  - Gap analysis: `phase-2-gap/gap-analysis.md` (Approved)
  - Working memory: `working-memory.md` ({N} sources, {N} findings)
  - Gaps identified: {N}
  - Non-gaps: {N}
  - Intent revised: {yes/no}

  ## Next
  Phase 3 — Planning (`/plan`)
  ```

### 5. Close the session

> "Gap analysis locked. [N] gaps identified, [N] things already in place. The planning phase will use this to decompose the work into steps. Next step whenever you're ready: `/theway:plan`."

Confirm the file locations.

## Resuming a Session

If the user runs `/gap` and Phase 2 work already exists:

1. Read `loop-state.md` to determine where they left off
2. Read `working-memory.md` fully — this is your recovery mechanism. It contains all sources, the research plan, and findings logged so far.
3. Resume at the appropriate stage:
   - If working memory has sources but research plan is incomplete → resume at Stage 1 (Orientation)
   - If research plan exists with unchecked items → resume at Stage 2 (Research)
   - If research is done but no gap-analysis.md → resume at Stage 3 (Synthesis)
   - If gap-analysis.md exists but not approved → resume at Stage 4 (Review)
4. Tell the user where you're picking up:
   > "I see you started the gap analysis on [date]. You got through [stage]. Working memory has [N] sources and [N] findings. Want to pick up where you left off?"

## Principles

- **The human sees what you can't.** Existing systems, prior work, institutional knowledge, external resources, relationship context. Your first job is to ask what exists, not to start exploring.
- **Working memory is your external brain.** Write everything to `working-memory.md` — sources, research plan, findings. Your context window will forget. The file won't. Re-read it before any synthesis step.
- **Plan before you research.** Don't just start reading random files or searching aimlessly. Build a research plan from the orientation conversation, then execute it systematically. Add new tasks as they emerge, but always work from the plan.
- **Evidence over opinion.** Every claim in the gap analysis should be backed by something you actually observed — a file, a URL, a document, a metric, a human statement. "I believe the situation is X" is weak. "Based on [specific source] and [specific source], the situation is X" is strong.
- **Write after every research task.** The findings log in working memory is the artifact. If the session crashes mid-research, all completed findings are preserved and the plan shows what's left.
- **Non-gaps are findings too.** Discovering that something already satisfies the intent is valuable — it prevents wasted effort in planning.
- **Let the intent document be challenged.** If reality doesn't match the intent, the intent might need to change. Surface this to the human explicitly rather than silently adjusting your analysis.
- **Recommend priorities, don't decide them.** The gap map should suggest an order based on dependencies and complexity, but the human confirms priorities in the planning phase.
