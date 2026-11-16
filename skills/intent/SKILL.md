---
name: intent
description: "Phase 1 of The Way: turn a raw idea into an approved intent document through conversation. Use when the user invokes /theway:intent or asks to start a new Way project."
---

# Intent

First read `conventions.md` in the plugin root, two levels up from this skill's directory. It defines the folders, IDs and document rules.

Help the user get an idea out of their head and into `intent.md`: a short contract that every later phase checks its work against. Be a thinking partner: curious, direct, and unwilling to accept vague answers. Time spent here pays off more than in any other phase.

## 1. Start

Get a short working name (lowercase, hyphenated, like `onboarding-redesign`) and claim the project ID and folder as `conventions.md` describes. Read any existing material the user points to, or that is obviously relevant.

## 2. Braindump

Ask one open question and let them talk. After each answer, react briefly (what's interesting, what it connects to, what tension you see) and ask the next question, steering toward what is still missing:

- **Purpose:** why this needs to exist.
- **Audience:** who it's for and what they care about.
- **Outcome:** the one thing that should happen.
- **Success:** how we'll know it worked.
- **Constraints:** hard limits such as time, budget, existing systems or brand.
- **Non-goals:** what a reasonable person might assume is in scope but isn't.

Add other dimensions, like tone or visual direction, only when the project needs them. Always cover purpose, outcome, success and constraints. Push past first answers: "a new landing page" is not intent; "a landing page that convinces enterprise buyers we're mature enough to trust with their data" is.

This usually takes three to eight exchanges. When the core is out, play back what you heard, grouped by dimension, along with the gaps, tensions and assumptions you noticed. If some ideas could stand alone as their own project, ask whether to keep them or park them in `index.md`.

## 3. Clarify

Resolve the gaps and tensions in about five questions at most. Where research could inform an answer (the web, files, earlier decisions), do it first and lead with what you found. Pure judgment calls are just asked.

## 4. Write intent.md

```markdown
# Intent: {Project name}

Status: Draft
ID: {NNN} · Started: {YYYY-MM-DD}

## Desired outcome
{One sentence: what is true when this is done.}

## Purpose
{Why it needs to exist. Two or three sentences.}

## Success criteria
- [ ] {Something an agent could check yes or no against the finished result.}

## Non-goals
- {Something a reasonable person might assume is in scope.}

## Constraints
- {A hard limit, not a preference.}

## {Other dimensions, only where they matter}

## In the user's words
> {A few verbatim quotes that carry intent the summary can't.}

## Open questions
- {Question that won't block the next phase.} Revisit when: {trigger}.
```

Every sentence should be checkable: "modern feel" isn't; "clean layout with generous whitespace, like {reference}" is.

## 5. Approve

Ask the user to read it and push back on anything wrong or missing. Revise until they approve, then set `Status: Approved`. Close by naming the next step: `/theway:gap`, or `/theway:work` if the current state is already clear enough to skip gap (say why).
