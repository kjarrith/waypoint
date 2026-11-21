# Gap Analysis — universal-way
Date: 2026-03-01
Intent: `phase-1-intent/intent.md`
Status: Approved

---

## Executive Summary

The plugin is structurally close to the target. The five-phase architecture (Intent → Gap → Plan → Work → Reflect) is inherently domain-agnostic — the *structure* works for any project. The gap is in the *language and examples* within each skill: they assume software projects (codebases, file deliverables, tech stacks) rather than adapting to whatever domain the project is in. The biggest rewrite is the gap skill; the reflect skill barely needs changes. On the packaging side, the plugin directory is already valid — the main missing pieces are `marketplace.json`, a `LICENSE` file, and a README rewritten for a marketplace audience. The core design principle for all changes: **don't assume software, but don't exclude it either** — let the framework detect and adapt to the project domain.

## Current State

### What exists today
- **5 implemented skills** in `skills/` with correct `SKILL.md` structure: intent, gap, plan, work, reflect
- **Valid plugin manifest** at `.claude-plugin/plugin.json` (name: "theway", version: 0.1.0, MIT license)
- **CLAUDE.md** with minimal one-line description
- **README.md** with good structure but outdated content
- **SPEC.md** with detailed framework specification (to be retired per intent)
- **Cross-cutting patterns** documented in SPEC.md: write-after-every-exchange, working memory, loop state, human approval gates, intent revision handling, session resumption — all already implemented in the skills
- **Backlog system** at `way-docs/backlog.md` — functional cross-project artifact
- **.gitignore** exists but only ignores `.DS_Store`

### Skill architecture
Each skill follows a consistent pattern: YAML frontmatter (name, description) → staged workflow → file-based state → human approval gate → session resumption support. This architecture is sound and universal. The stages within each skill are also inherently universal:
- Intent: braindump → organize → clarify → crystallize → validate
- Gap: orientation → research → synthesis → review
- Plan: analysis → structuring → decomposition → review
- Work: pickup → execute → evaluate → present → feedback → advance
- Reflect: gather → reflect → close

### What's reusable
- The entire skill architecture and stage structure
- The file-based state model (loop-state.md, working-memory.md, phase artifacts)
- The cross-cutting patterns (crash recovery, session resumption, human approval gates)
- The plugin directory structure (`.claude-plugin/`, `skills/`)
- Most of the intent and reflect skills (minimal changes needed)

## Gap Map

### Gap 1: Skill language assumes software — needs domain-adaptive framing
- **Intent says:** "All five skill prompts are domain-agnostic — no software-specific assumptions in the core skills"
- **Current state:** Skills contain software-specific language at varying severity:
  - **Intent skill** (small): "Do you have access to a code base?" (line 18), "backend APIs" example (line 102), "Search the codebase" (line 196), "Which frontend framework should we use?" (line 200)
  - **Gap skill** (major): Research examples all reference `apps/agent-squad/src/`, `package.json`, `docs/architecture.md` (lines 110-113). Template has mandatory "Technical landscape" section (lines 197-200). Evidence examples cite `.ts` files (line 325). Tool guidance is codebase-specific (lines 137-140).
  - **Plan skill** (medium): Deliverables described as "file paths, formats, components" (line 232). Example criteria reference code structure (line 185).
  - **Work skill** (medium): Lists "code writing" as primary activity (line 68). Work log template has "Files created/modified" (line 111) which breaks for non-file deliverables.
  - **Reflect skill** (tiny): One reference to "the repo" (line 165).
- **Delta:** Each skill needs its language reframed from "assume software" to "detect domain, adapt accordingly." The key design choice: use universal language by default, with guidance for the agent to adapt its approach based on what the project is. For software projects, the agent should still explore codebases, check dependencies, and evaluate code. For hiring projects, it should research candidates, map processes, and evaluate outcomes. The skills should guide this adaptation rather than assuming one domain.
- **Complexity:** Medium — the structure stays; the language, examples, and templates change
- **Dependencies:** None — this can be done skill by skill
- **Notes:** CRITICAL NUANCE from user: "Do not over-index into non-dev stuff. I also want this to be really useful for devs." The solution is NOT to strip software references but to make the default language universal while providing domain-adaptive guidance. Example: instead of "Search the codebase for existing components," write something like "Research what already exists. For software projects, explore the codebase. For hiring, review current processes and candidate pipelines. For content, audit existing materials."

### Gap 2: README not written for marketplace audience
- **Intent says:** "The README clearly communicates what The Way is, why it exists, and how to install and use it — written for a marketplace audience"
- **Current state:** README has several accuracy issues:
  - Says "A Claude Code plugin" (should cover both Claude Code and Cowork)
  - Phase 4 described as "Builder-evaluator execution loops" — SPEC.md language that doesn't match the actual `/work` skill
  - Project structure shows old SPEC.md artifacts (`build-log.md`, `evaluation.md`, `status.md`) instead of actual `step-{NN}-{name}.md` files
  - "More skills coming: review, status" — not in v1 scope
  - "Requirements: Claude Code 1.0.33 or later" — needs verification
  - Links to external repo for "value creation metaprocess" — external dependency
  - Written as internal dev docs, not as a marketplace pitch
- **Delta:** Full README rewrite needed. Must sell the framework's value proposition ("slow down to go fast"), explain the five phases clearly and accurately, provide installation instructions for both marketplace and local dev, and reflect the actual skill behavior (not SPEC.md).
- **Complexity:** Medium
- **Dependencies:** Depends on Gap 1 (skill rewrites) for accurate skill descriptions
- **Notes:** The README is the storefront. For a marketplace, it needs to hook people in 10 seconds: what is this, why should I care, how do I start.

### Gap 3: Missing marketplace.json
- **Intent says:** "A marketplace.json exists in the repo, and the plugin is installable via `/plugin marketplace add` + `/plugin install`"
- **Current state:** No `marketplace.json` exists anywhere in the repo. The plugin can be used locally with `claude --plugin-dir` but cannot be discovered or installed via a marketplace.
- **Delta:** Create `.claude-plugin/marketplace.json` with the plugin entry pointing to a relative path (monorepo pattern). Must include name, owner, description, and plugin source.
- **Complexity:** Low
- **Dependencies:** None
- **Notes:** Per the plugin docs, marketplace.json goes in `.claude-plugin/` alongside plugin.json. The monorepo pattern uses a relative path source.

### Gap 4: Missing LICENSE file
- **Intent says:** "The repo is MIT-licensed and ready for open source publication"
- **Current state:** `plugin.json` declares `"license": "MIT"` but no actual `LICENSE` file exists in the repo. Open source publication requires a license file.
- **Delta:** Add standard MIT LICENSE file to repo root.
- **Complexity:** Low
- **Dependencies:** None
- **Notes:** Standard MIT license text with author name and year.

### Gap 5: SPEC.md retirement and cleanup
- **Intent says:** "SPEC.md is retired — SKILL.md files are the authority for phase behavior"
- **Current state:** SPEC.md (406 lines) exists and contains the detailed framework specification, including cross-cutting patterns that the skills reference implicitly. Also present: `.obsidian/` directory (editor config), `.DS_Store` files, and `way-docs/` (project artifacts from using the framework).
- **Delta:**
  1. Delete or archive SPEC.md (the valuable cross-cutting patterns are already implemented in the skills; any missing patterns should be absorbed into the relevant skills or CLAUDE.md)
  2. Update `.gitignore` to exclude `.obsidian/`, `way-docs/`, `.DS_Store`
  3. Clean up any stale references to SPEC.md in other files
- **Complexity:** Low
- **Dependencies:** Gap 1 (ensure skills are self-sufficient before removing SPEC.md)
- **Notes:** Some SPEC.md content (the Specify → Generate → Evaluate triad, the escalation protocol, the multi-terminal pattern) has value as conceptual framing. The README could reference these concepts at a high level. The detailed specs should live in the skills.

### Gap 6: plugin.json needs updating
- **Intent says:** Plugin should be structured as a proper Claude plugin with valid manifest
- **Current state:** plugin.json exists but has issues:
  - Description mentions "builder-evaluator loops" (SPEC.md language)
  - Keywords include "project-management" (a non-goal per intent)
  - No `homepage` field
- **Delta:** Update description to match universal framing. Replace keywords with domain-agnostic terms. Add homepage if a URL is available.
- **Complexity:** Low
- **Dependencies:** Gap 1 (final language decisions)
- **Notes:** Description should convey the value proposition concisely: structured human-agent collaboration from idea to result.

### Gap 7: CLAUDE.md needs skill trigger guidance
- **Intent says:** "CLAUDE.md provides minimal orientation: tells Claude the skills exist and when to suggest them, without being intrusive"
- **Current state:** One line: "A human-agent collaboration plugin for use within the Claude ecosystem. Skills guide projects through: Intent → Gap → Plan → Work → Reflect."
- **Delta:** Add brief trigger guidance so Claude knows when to suggest each skill. E.g., "Suggest `/theway:intent` when the user describes a new project, says 'I want to build...', or needs to clarify what they're trying to accomplish."
- **Complexity:** Low
- **Dependencies:** None
- **Notes:** Keep it genuinely minimal. A few lines, not a manifesto.

### Gap 8: Cowork tool compatibility
- **Intent says:** "The plugin works in both Claude Code and Claude Desktop/Cowork (filesystem-based state, no terminal-specific dependencies)"
- **Current state:** Skills reference specific Claude Code tools by name:
  - Gap skill names `Task` with `Explore` agents (line 142), `browser-use` (line 139), and specific tool names (`Glob`, `Grep`, `Read`)
  - Multiple skills use `mkdir -p` via Bash
- **Delta:** Replace hard-coded tool names with generic guidance. Instead of "use `Glob` to search files," write "search for relevant files." Instead of "use `Task` with `Explore` agents," write "use available research tools for deeper investigation." The agent will use whatever tools are available in its environment.
- **Complexity:** Low — language changes only, part of the Gap 1 rewrite
- **Dependencies:** Addressed as part of Gap 1
- **Notes:** This is essentially a subset of Gap 1's language universalization, but specifically targeting platform portability rather than domain portability.

## Non-Gaps (Already Satisfied)

- **Plugin directory structure**: `.claude-plugin/plugin.json` exists, `skills/` directory with correct SKILL.md structure. Already valid per Claude plugin reference.
- **Five-phase architecture**: Intent → Gap → Plan → Work → Reflect is inherently domain-agnostic. The *structure* needs no changes.
- **Stage patterns within skills**: Each skill's internal stages (braindump→organize→clarify→crystallize→validate, etc.) are universal patterns that work for any domain.
- **File-based state model**: loop-state.md, working-memory.md, phase artifacts — all domain-agnostic by design.
- **Cross-cutting patterns**: Write-after-every-exchange, session resumption, human approval gates, intent revision handling — all implemented and universal.
- **Human-in-the-loop design**: Approval gates between phases, escalation within phases — works for any domain.
- **Backlog system**: Cross-project backlog at `way-docs/backlog.md` — functional and domain-agnostic.

## Risks and Unknowns

- **Risk: Over-abstracting kills the experience.** If we make skills too generic ("research the current state"), they lose the warmth and specificity that makes the agent a good thinking partner. The challenge is being universal without being vague. Mitigation: use domain-adaptive examples ("For software projects, explore the codebase. For hiring, review the recruiting pipeline.") rather than stripping all specificity.
- **Risk: Cowork tool availability is uncertain.** We don't have a definitive list of which tools are available in Claude Desktop/Cowork. We're assuming filesystem tools work there. Mitigation: use generic tool guidance and test in Cowork before publishing.
- **Unknown: Optimal README length for marketplace discovery.** We don't know what converts in the marketplace. Is it a short punchy pitch or a detailed guide? Mitigation: write a clear, concise README and iterate based on feedback.
- **Unknown: Whether `way-docs/` should ship with the plugin or be gitignored.** It's user data (project artifacts) but also shows how the framework works. Probably should be gitignored for a clean install, with the README explaining the structure.

## Recommended Priorities

1. **Gap 1: Universalize skill language** — Highest priority. This is the core of the project. Everything else depends on the skills being right. Start with the gap skill (biggest rewrite), then plan, work, intent, reflect.
2. **Gap 5: Retire SPEC.md and clean up** — Do this early to avoid confusion. Ensure skills are self-sufficient first.
3. **Gap 2: Rewrite README** — Depends on Gap 1 for accurate descriptions. This is the marketplace face of the plugin.
4. **Gap 7: Update CLAUDE.md** — Quick win, low dependency.
5. **Gap 6: Update plugin.json** — Quick win, finalize after skill language is settled.
6. **Gap 3: Create marketplace.json** — Straightforward, do after plugin.json is final.
7. **Gap 4: Add LICENSE file** — Trivial, do anytime.
8. **Gap 8: Cowork compatibility** — Addressed as part of Gap 1.

## Sources
- `skills/intent/SKILL.md` (387 lines)
- `skills/gap/SKILL.md` (330 lines)
- `skills/plan/SKILL.md` (367 lines)
- `skills/work/SKILL.md` (247 lines)
- `skills/reflect/SKILL.md` (243 lines)
- `.claude-plugin/plugin.json`
- `CLAUDE.md`
- `README.md`
- `SPEC.md`
- `.gitignore`
- https://code.claude.com/docs/en/plugins-reference
- https://code.claude.com/docs/en/plugin-marketplaces
- https://claudemarketplaces.com/
