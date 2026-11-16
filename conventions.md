# The Way: shared conventions

Every theway skill follows these rules. This file is the only place the folder layout, IDs, documents and phase order are defined.

## Where projects live

Projects live in `way-docs/` at the root of the working directory. Create it on first use.

```
way-docs/
  index.md
  {YYYY-MM}/
    {NNN}-{project-name}/
      intent.md
      gap.md
      plan.md          only when the project needs one
      work.md
      reflection.md
```

- `NNN` is a three-digit ID from one counter across all of `way-docs/`, not one per month. `YYYY-MM` is the month the project started.
- Find a project by ID with `way-docs/*/{NNN}-*/` and by name with `way-docs/*/*-{name}/`. If the user doesn't name one, use the project this conversation is about; otherwise read `index.md` and ask.

## Starting a project

Only intent starts projects. Claim the ID before the conversation begins, so parallel sessions can't take the same one:

1. Next ID = the highest ID in `index.md` or among existing project folders, plus one. The first project is `001`.
2. Create the project folder and add its row to `index.md` straight away. Create `index.md` from the template below if it doesn't exist.

## index.md

```markdown
# Way projects

| ID | Project | Started | Summary |
|----|---------|---------|---------|
| 001 | landing-page | 2026-11-16 | One line on what it's for |

## Parked ideas

- **{idea}** (from 001, 2026-11-16): one or two sentences on what it is and why it was parked.
```

The index holds only what can't be read elsewhere. It has no status column: a project's progress is read from its documents. When a parked idea becomes a project, remove it from the list and mention it in the new project's intent.

## Documents

- The conversation is the working memory. Write each phase's document when the phase is ready for review, not exchange by exchange. The exception is `work.md`, which gets one entry per approved step because work spans sessions.
- `intent.md`, `gap.md`, `plan.md` and `reflection.md` carry `Status: Draft` until the user approves them, then `Status: Approved`. `work.md` carries `Status: In progress` until every step is approved, then `Status: Done`. Which documents exist, and their status, is the project's state. There is no separate state file.
- Write for an agent that never saw the conversation: a new session picks up a project by reading its documents. Record what was decided and why, not the conversation that got there.

## Phases

intent → gap → plan (optional) → work → reflect

- Gap can be skipped when the current state is already clear. Plan is only for projects with several workstreams, real dependencies, steps owned by other people, or steps too big for one sitting. Gap ends by recommending whether a plan is needed.
- If a later phase shows the intent was wrong, say so. With the user's agreement, update `intent.md` and add a dated line under a `## Revisions` heading at the bottom. Never quietly work around the intent.

## Working with the user

- The user decides. You research, organize and recommend, and every document needs their approval.
- Ask one thing at a time in plain chat. Use `AskUserQuestion` only when there is a real choice between two to four options.
- Research before asking whenever research could inform the answer, and lead with what you found.
