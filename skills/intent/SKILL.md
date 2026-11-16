---
name: intent
description: "Run a structured intent crystallization session that takes a user from raw idea to approved intent document. Use when the user says 'intent', 'let's define intent', 'new project', 'I want to build...', 'we need a...', or invokes /intent. This is Phase 1 of the value creation metaprocess — everything downstream depends on the quality of this output."
---

# Intent Crystallization Session

This is the first of five steps in "The Way", an agent-human collaboration framework. 

The goal is to guide the user from a raw idea to a crystallized, approved intent document through five stages: Braindump, Organize, Clarify, Crystallize, Validate.

Act as a thinking partner — collaborative, curious, and relentlessly clarifying. Your job is to help the user externalize what they actually want, not what they think they should say. Never accept vague. Never assume you understand. Never rush past the braindump into premature structure.

The output of this session is `intent.md` — the contract that every downstream agent, skill, and evaluation will reference. Time invested here is 10x more valuable than time invested anywhere else.

## Setup

1. Orientation: begin by understanding the context in which the conversation is happening. Are there existing materials, resources, or prior work related to this project that you can access? Are you working in a specific project folder, or is this starting from scratch?
2. Ask the user what this project is about if they haven't already said. Get a working name for the project (short, lowercase, hyphenated — e.g. `landing-page`, `onboarding-redesign`, `q3-content-strategy`).
3. Determine the project root: `way-docs/{currentDate}-{project-name}/` (using ISO 8601 date, e.g., `way-docs/2026-03-01-landing-page/`)
4. Create the project directory and Phase 1 structure:
   ```
   way-docs/{currentDate}-{project-name}/
     phase-1-intent/
       references/
   ```
   Use `mkdir -p` for each directory. Other phase directories are created by their respective skills on entry.
5. Initialize the braindump file at `way-docs/{currentDate}-{project-name}/phase-1-intent/braindump.md`:
   ```markdown
   # Intent Braindump — {project-name}
   Date: {currentDate}
   ```
6. Initialize loop state at `way-docs/{currentDate}-{project-name}/loop-state.md`:
   ```markdown
   # Loop State — {project-name}

   **Current phase:** 1 — Intent Crystallization
   **Current stage:** Braindump
   **Status:** in-progress
   **Last updated:** {currentDate}
   ```

## Stage 1: Braindump (3-8 exchanges)

The goal is to get everything out of the user's head. Don't structure yet. Don't filter. Don't solve.

### Opening

Start with something like:

> "Alright, tell me about this. What are you imagining? What problem are you solving, who is it for, what does success look like? Don't worry about structure — just talk."

Ask an open-ended question. Let them talk.

### Interview Loop

After each user response, do these three things **in order**:

#### 1. Update the braindump file

Append to `phase-1-intent/braindump.md` using the `Edit` tool (append at end of file):

```markdown

## Exchange {N}

**Question:** {the question you asked}

**Raw answer:** {user's response — preserve their words faithfully}

**Reflection:** {2-3 sentences: what's interesting, what it connects to, what intent dimensions are emerging, what's still missing. If you notice separable components — ideas that could stand alone as a separate project — flag them.}

**Dimensions touched:** {list which intent dimensions this exchange informed: purpose, audience, action, success, constraints, non-goals}

---
```

#### 2. Reflect briefly to the user

Share a short, genuine observation with the user in the chat. Connect it to something — a pattern, a tension, something from project context. 1-2 sentences. This is a reaction, not a summary.

#### 3. Ask the next question

Ask the user a question with a follow-up that targets **uncovered intent dimensions**. Track which dimensions have been touched and steer toward gaps:

**Intent dimensions to cover:**
- **Purpose** — what is this thing and why does it need to exist?
- **Audience** — who is this for, what do they care about, where are they coming from?
- **Primary Action** — the one thing that should happen (conversion, understanding, emotion)
- **Success Criteria** — how will you know this worked? measurable if possible
- **Constraints** — technical, timeline, budget, brand, existing systems
- **Non-Goals** — what this explicitly is NOT (prevents scope creep downstream)
- **Context-dependent** — voice & tone, visual direction, and other optional dimensions that are context-dependent

Question strategies:
- **Go deeper** — "You mentioned X. What specifically about that matters most?"
- **Go wider** — "How does this connect to [something from project context]?"
- **Challenge** — "You said A but also B — if they compete, which wins?"
- **Surface the unsaid** — "What haven't you said yet about this?"
- **Request examples** — "Can you point me to something that captures the feel you want?" (save references to `phase-1-intent/references/`)

**Don't cover every dimension mechanically.** Some projects don't need visual direction (a backend service, a hiring process). Some don't have audience complexity (an internal tool, a personal workflow). Use judgment. But always cover: purpose, primary action, success criteria, and constraints.

You don't have to user *AskUserQuestion* for every question. Sometimes it's better to just ask the question directly and allow the user to respond naturally. Only use *AskUserQuestion* when you believe it would be valuable to present the user with a 2-4 very clear options to choose from.

### Transition to Organize

After 3-8 exchanges, when you sense the user has externalized the core of their thinking, suggest the transition:

> "I think we have a lot of raw material here. Ready for me to organize what I've heard into a structured view? You can always add more after."

Do NOT proceed to Organize until the user confirms. If they have more to say, keep going.

## Stage 2: Organize (agent-driven, 1-2 exchanges)

Read back `phase-1-intent/braindump.md` in full. Cluster everything the user said into the intent dimensions.

### 1. Write the organized view

Append to `phase-1-intent/braindump.md`:

```markdown

## Organized View

### What I heard — by dimension

**Purpose:**
{what the user said about why this exists, synthesized}

**Audience:**
{who it's for, synthesized}

**Action and work needed:**
{what should happen, synthesized}

**Success Criteria:**
{how we'll know it worked, synthesized}

**Constraints:**
{limits and requirements, synthesized}

**Non-Goals:**
{what this is NOT, synthesized — or "Not discussed"}

**Other context-dependent dimensions (optional):**
{other important context-dependent dimensions that are not covered by the other dimensions, synthesized}

### Gaps and tensions I noticed
- {gap: dimension not covered or underspecified}
- {tension: two things the user said that might conflict}
- {assumption: something I'm inferring that hasn't been stated}

### Scope signals
{If the braindump contains ideas that seem separable from the core project — things that could be their own project — list them here. If everything is tightly coupled, write "No separable components detected."}
- **Core:** {what's central to this project — the ideas that define its purpose}
- **Potentially separable:** {ideas that could be parked for a future project}
  - {idea}: {why it seems separable — different audience, independent deliverable, etc.}

---
```

### 2. Present to the user

Show them the organized view. Ask:

> "Here's what I heard, organized by dimension. Does this track? Anything I got wrong, missed, or that you want to push back on? I also noticed [gaps/tensions] — we'll dig into those next."

If you identified potentially separable components in the scope signals:

> "I also noticed some ideas that might be separable from the core project: [list]. These could be parked in the backlog for a future project. What do you want to keep in scope vs. park for later?"

Use `AskUserQuestion`. Let them react, correct, add. Update the file with their corrections.

If the user decides to park ideas, write them to the backlog (see **Backlog Writing** below) and note in the organized view which ideas were deferred.

### 3. Update loop state

Update `loop-state.md`:
```markdown
**Current stage:** Clarify
```

## Stage 3: Clarify (2-5 targeted questions)

Now address the gaps and tensions identified in the Organize stage. If scope wasn't fully resolved in Organize (e.g., the user was unsure about a separable component), scoping can be one of the clarifying questions:

> "You mentioned [separable idea]. Is that part of this project, or should we park it in the backlog for later?"

### For each gap or tension:

#### 1. Research first (where applicable)

Before asking the user to decide, research where it helps:
- Search the web for best practices, benchmarks, comparable examples
- Search any accessible project files for existing patterns, constraints, or prior decisions
- Look up relevant data that could inform the decision
- For deeper investigation, delegate to available research tools or subagents

Not every question needs research. "What tone do you want?" is a judgment call. "What's the standard approach for this kind of project?" benefits from research. Use judgment.

#### 2. Present findings and ask

For questions that benefited from research:
> "Before I ask you about [gap], I looked into [what you researched]. Here's what I found: [findings]. Given that, [question]?"

For pure judgment questions:
> "You mentioned [tension]. If these compete, which wins?"

Use `AskUserQuestion`. Maximum 5 clarifying questions total. Maximum 2 rounds (if the first round surfaces new questions). Don't exhaust the user.

#### 3. Record each clarification

Append to `phase-1-intent/clarifications.md` (create it on first clarification):

```markdown

## Clarification {N}: {short title}

**Gap/tension:** {what needed clarifying}

**Research:** {what the agent found, if applicable — or "N/A (judgment call)"}

**Question asked:** {the question}

**User's answer:** {their response, faithfully captured}

**Impact on intent:** {how this changes or confirms the intent — which dimension it affects}

---
```

### Transition to Crystallize

After clarifications are resolved:

> "I think I have everything I need to draft the intent document. Ready for me to put it together?"

## Stage 4: Crystallize (agent-driven)

Write `phase-1-intent/intent.md`. This is THE CONTRACT — the single source of truth for everything downstream.

```markdown
# Intent: {Project Name}

**Status:** Draft
**Date:** {currentDate}
**Author:** {user} + Claude

---

## Desired Outcome
{One clear sentence: what does success look like when this is done? "The user wants to..."}

## Purpose
{Why does this need to exist? What problem does it solve? 2-3 sentences max.}

## Success Criteria
{Measurable where possible. Each criterion should be evaluable — an agent should be able to look at the finished deliverable and answer yes/no for each.}
- [ ] {criterion 1}
- [ ] {criterion 2}
- [ ] {criterion 3}

## Non-Goals
{Explicitly what this project is NOT. Prevents scope creep downstream. Every non-goal should be something that a reasonable person might assume is in scope.}
- {non-goal 1}
- {non-goal 2}

## Constraints
{Technical, timeline, budget, brand, existing systems — anything that limits the solution space.}
- {constraint 1}
- {constraint 2}

## Open Questions
{Anything that couldn't be resolved in this session but won't block the next phase. Include triggers for when to revisit.}
- {question — revisit when: {trigger}}

## Source Material
- Braindump: `phase-1-intent/braindump.md`
- Clarifications: `phase-1-intent/clarifications.md`
- References: `phase-1-intent/references/`
```

**Writing principles for intent.md:**
- Every sentence should be evaluable. "Modern feel" is not evaluable. "Clean layout with generous whitespace, similar to [reference]" is.
- Success criteria should be yes/no checkboxes that an evaluator agent can assess against a finished deliverable.
- Non-goals are as important as goals. They prevent downstream agents from gold-plating or expanding scope.
- Constraints are hard limits, not preferences. Preferences go in the relevant dimension (voice, visual, etc.).

## Stage 5: Validate (human approval)

### 1. Present intent.md to the user

> "The intent document is ready at {path to intent.md}. This becomes the contract for everything downstream — gap analysis, planning, building, and evaluation will all reference this. Read it carefully. Is anything wrong? Missing? Not quite right? I'd rather we catch it now."

Use `AskUserQuestion`. Give them space to read and react.

### 2. Handle feedback

If the user has changes:
- Update `intent.md` with their corrections
- Re-present the changed sections
- Ask for confirmation again
- Append a revision note at the bottom of intent.md:
  ```markdown
  ## Revision History
  - {currentDate}: Initial draft → validated with corrections: {brief description of changes}
  ```

Iterate until the user confirms.

### 3. Lock the intent

When the user approves:
- Update the Status field in intent.md from `Draft` to `Approved`
- Update `loop-state.md`:
  ```markdown
  # Loop State — {project-name}

  **Current phase:** 1 — Intent Crystallization
  **Current stage:** Complete
  **Status:** phase-complete
  **Last updated:** {currentDate}

  ## Phase 1 Summary
  - Intent document: `phase-1-intent/intent.md` (Approved)
  - Braindump: `phase-1-intent/braindump.md` ({N} exchanges)
  - Clarifications: `phase-1-intent/clarifications.md` ({N} clarifications)

  ## Next
  Phase 2 — Gap Analysis (`/gap`)
  ```

### 4. Close the session

> "Intent locked. Everything downstream — gap analysis, planning, building, evaluation — will reference this document. If you learn something later that changes the intent, that's fine — we'll handle it in the reflect phase, deliberately. Next step whenever you're ready: `/theway:gap`."

Confirm the file locations.

## Backlog Writing

When the user decides to park ideas during Organize or Clarify, write them to `way-docs/backlog.md`. Create the file if it doesn't exist.

**Format:**

```markdown
# Backlog

## {Idea title}
- **Date:** {currentDate}
- **Source:** {project-name}
- **Description:** {1-2 sentences: what the idea is and why it was separated}
- **Status:** parked

## {Next idea}
...
```

Each entry is a separable idea that emerged during an intent session but was deferred. Status is `parked` when written. If a future `/theway:intent` session picks up an idea from the backlog, update its status to `promoted` and note which project adopted it.

Append new entries — don't overwrite existing ones. The backlog is a cross-project artifact shared across all projects in `way-docs/`.

## Resuming a Session

If the user runs `/intent` and a project already exists with partial Phase 1 work:

1. Read `loop-state.md` to determine where they left off
2. Read whatever files exist (`braindump.md`, `clarifications.md`, `intent.md`)
3. Resume at the appropriate stage:
   - If braindump exists but no organized view → resume at Stage 2 (Organize)
   - If organized view exists but no clarifications → resume at Stage 3 (Clarify)
   - If clarifications exist but no intent.md → resume at Stage 4 (Crystallize)
   - If intent.md exists in Draft status → resume at Stage 5 (Validate)
4. Tell the user where you're picking up:
   > "I see you started this project on [date]. You got through [stage]. Want to pick up where you left off?"

## Principles

- **Capture faithfully.** The braindump records what the user actually said, not a polished version. Their words, their energy, their contradictions.
- **Write after every exchange.** The files are the artifact. If the session crashes at any point, everything up to that point is preserved and resumable.
- **Probe, don't accept.** First answers are surface-level. "A new landing page" is not intent. "A landing page that convinces enterprise buyers our product is mature enough to trust with their data" is intent.
- **Track dimensions explicitly.** After each exchange, note which intent dimensions were touched. Steer toward gaps. But don't be mechanical about it.
- **Research where it helps, skip where it doesn't.** Not every clarification needs a web search. "What tone do you want?" is pure judgment. "What framework should we use?" benefits from data.
- **Evaluable over expressive.** Every statement in intent.md should be something an agent can evaluate a deliverable against. Vague vibes in the braindump are fine. Vague vibes in intent.md are not.
- **The user decides, always.** You organize, research, synthesize, and recommend. They approve. The intent document reflects their judgment, informed by your work.
- **Know when to stop.** A great 5-exchange braindump with 3 clarifications beats an exhaustive 15-exchange session that tires the user out. Capture the signal, not the noise.
