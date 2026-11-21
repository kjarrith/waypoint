# Intent: Universal Way

**Status:** Approved
**Date:** 2026-03-01
**Author:** K. Thorisson + Claude

---

## Desired Outcome
The Way becomes a domain-agnostic, open source Claude plugin that guides any person from a raw idea to real, high-quality progress — regardless of whether the project is software, fundraising, hiring, migration, or anything else — published to a Claude plugin marketplace.

## Purpose
AI cannot one-shot complex work. The missing piece is a structured path from fuzzy intent to clear specification to real deliverables. The Way provides that path: five phases (Intent → Gap → Plan → Work → Reflect) that work for any domain, carried by a conversational experience that makes thinking feel natural rather than bureaucratic. It's a thinking amplifier, not an automation shortcut.

## Success Criteria
- [ ] All five skill prompts (intent, gap, plan, work, reflect) are domain-agnostic — no software-specific assumptions in the core skills (no references to codebases, code files, code evaluation, or programming languages as defaults)
- [ ] The plugin works end-to-end for a non-software project (e.g., hiring, fundraising, or migration) without the user needing to configure or adapt it
- [ ] The plugin is structured as a proper Claude plugin: `.claude-plugin/plugin.json` manifest, skills in `skills/`, valid directory structure per the plugin reference
- [ ] A `marketplace.json` exists in the repo, and the plugin is installable via `/plugin marketplace add` + `/plugin install`
- [ ] The plugin works in both Claude Code and Claude Desktop/Cowork (filesystem-based state, no terminal-specific dependencies)
- [ ] The README clearly communicates what The Way is, why it exists, and how to install and use it — written for a marketplace audience
- [ ] CLAUDE.md provides minimal orientation: tells Claude the skills exist and when to suggest them, without being intrusive
- [ ] The repo is MIT-licensed and ready for open source publication
- [ ] The experience feels elegant and opinionated — the agent acts as a thinking partner, not a form to fill out

## Non-Goals
- Speed optimization or shortcuts — The Way deliberately trades startup time for outcome quality
- Automation that removes thinking — it amplifies thinking, it doesn't replace it
- Domain-specific subagents in v1 — the universal core ships first; domain extensions are a separate project
- Hooks automation in v1 — hooks are a future enhancement, not a v1 deliverable
- Multi-agent / multi-terminal coordination — parked for a future project
- A deep experience polish pass — structural universalization comes first; dedicated UX refinement follows
- Project management features (dashboards, status boards, Gantt charts) — the interface is conversation
- Requiring users to configure the framework for their domain before using it

## Constraints
- Must use the Claude plugin architecture: skills, plugin manifest, marketplace.json
- Filesystem-as-state pattern is the core state model (both Claude Code and Cowork support this)
- Plugin must be self-contained — no dependencies outside the plugin directory
- The five-phase structure (Intent → Gap → Plan → Work → Reflect) and the Specify → Generate → Evaluate triad are the conceptual backbone — universalize them, don't replace them
- MIT license
- Monorepo: plugin and marketplace.json in the same GitHub repository
- SPEC.md is retired — SKILL.md files are the authority for phase behavior; README is the public-facing document

## Open Questions
- What is the right granularity for "domain-agnostic" in the gap analysis phase? The current gap skill does codebase exploration. The universal version needs to discover current state for *any* domain — but how abstract can "research the current state" be before it becomes unhelpful? — revisit when: rewriting the gap skill
- How should the work phase handle "deliverables" that aren't files (conversations had, introductions made, decisions reached)? — revisit when: rewriting the work skill
- Should cross-cutting skills (/theway:review, /theway:status from SPEC.md) be included in v1? They were specified but focus on multi-project workflows. — revisit when: planning phase

## Source Material
- Braindump: `phase-1-intent/braindump.md`
- Clarifications: `phase-1-intent/clarifications.md`
- References: `phase-1-intent/references/`
