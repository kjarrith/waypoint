# Backlog

## Resolve SPEC Phase 4 design: build/evaluate vs work
- **Date:** 2026-03-01
- **Source:** plan-skill
- **Description:** The SPEC describes separate `/theway:build` and `/theway:evaluate` skills for Phase 4, but the actual implementation is a combined `/theway:work` skill. The Five Phases table, Skills To Build section, and Phase 4 descriptions all need aligning with reality. Surfaced in 3 of 6 work steps.
- **Status:** resolved (2026-03-01) — SPEC Phase 4 aligned with `/theway:work`; "Skills To Build" converted to "Phase 4 Design Notes"

## Investigate loop-state vs working-memory overlap
- **Date:** 2026-03-01
- **Source:** plan-skill
- **Description:** After consolidating working memory to a single project-level file, the overlap between loop-state.md (phase/stage/status) and working-memory.md (Session Context) became visible. Decide whether to merge them into one file or sharpen the boundary so each has a clear, non-overlapping role.
- **Status:** resolved (2026-03-01) — Sharpened boundary: loop-state = "where" (machine state), working-memory = "why/what" (rich context). Session Context removed from working-memory templates.

## Move folder bootstrapping from intent to each skill
- **Date:** 2026-03-01
- **Source:** plan-skill
- **Description:** The intent skill currently creates all phase directories (phase-1-intent/, phase-2-gap/, phase-3-plan/, etc.) upfront during Setup. Each skill should create only its own phase directory when it starts — cleaner ownership, no empty folders.
- **Status:** resolved (2026-03-01) — Intent trimmed to phase-1 only; gap and plan skills now create their own directories on entry.

## Domain-specific subagent packs
- **Date:** 2026-03-01
- **Source:** universal-way
- **Description:** Create subagents for specific domains (software development, hiring/recruiting, fundraising, content strategy) that activate contextually within The Way's universal phases. Software subagent could handle code evaluation, hiring subagent could handle candidate scoring, etc.
- **Status:** parked

## Hooks automation for The Way
- **Date:** 2026-03-01
- **Source:** universal-way
- **Description:** Use Claude plugin hooks (PreToolUse, PostToolUse, SessionStart, TaskCompleted, etc.) to automate elements of The Way — phase transition validation, review triggers, automatic state management.
- **Status:** parked

## Multi-agent / teams pattern
- **Date:** 2026-03-01
- **Source:** universal-way
- **Description:** Implement the multi-terminal pattern from SPEC.md — separate builder/evaluator terminals, filesystem-based coordination between concurrent Claude instances. Enables parallel build-evaluate cycles for large projects.
- **Status:** parked

## Experience refinement polish pass
- **Date:** 2026-03-01
- **Source:** universal-way
- **Description:** Dedicated project focused on conversational pacing, prompt quality, the "feel" of working with The Way as a thinking partner. Deep work on the experience layer after structural changes land.
- **Status:** parked

## Revise reflect skill — three-objective reframing
- **Date:** 2026-03-01
- **Source:** universal-way (reflection)
- **Description:** Restructure the reflect skill around three clear objectives with deliverables: (1) capture process learnings, (2) capture ideas and intent signals about next steps, (3) ensure docs match the new reality. Drop the loose conversation-arc approach (outcome reaction, what went well, surprises, etc.) in favor of focused phases. "Surprises" should not be a standalone topic.
- **Status:** parked

## Validate with a non-software project
- **Date:** 2026-03-01
- **Source:** universal-way (reflection)
- **Description:** Run a real non-software project (hiring, content, fundraising) through all 5 phases to validate the universalization end-to-end. Currently 4/9 success criteria are partially met due to lack of testing.
- **Status:** parked

## Test runtime installability and Cowork compatibility
- **Date:** 2026-03-01
- **Source:** universal-way (reflection)
- **Description:** Verify the plugin loads with `claude --plugin-dir .`, triggers correctly, and works in Cowork (tool availability, filesystem-based state).
- **Status:** parked
