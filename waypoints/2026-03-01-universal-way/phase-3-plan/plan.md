# Plan — universal-way
Date: 2026-03-01
Intent: `phase-1-intent/intent.md`
Gap Analysis: `phase-2-gap/gap-analysis.md`
Status: Approved

---

## Summary

Two workstreams, 8 total steps. Workstream 1 universalizes all five skill prompts — the core of the project. Workstream 2 packages the plugin for open source marketplace release. WS2 depends on WS1 because the README and plugin.json need accurate descriptions of the universalized skills. Within WS1, skills are ordered by rewrite severity: gap (major) → plan (medium) → work (medium) → intent (small) → reflect (tiny).

## Workstreams

### Workstream 1: Universalize Skills
**Purpose:** Rewrite all five skill prompts from "assume software" to "detect domain, adapt accordingly." Each skill's structure stays — the stages, file patterns, and approval gates are already universal. The language, examples, templates, and tool guidance change so the skills work for any project (software, hiring, fundraising, migration, content, etc.) while keeping software as a first-class domain.
**Gaps addressed:** Gap 1 (skill language), Gap 8 (Cowork tool compatibility)
**Handoff gates:** None (first workstream)

#### Step 1: Universalize the gap skill
- **Deliverable:** Rewritten `skills/gap/SKILL.md`
- **Sub-steps:**
  1. Replace the orientation opening — currently asks about "repos, folders, Figma files." Replace with domain-agnostic framing that adapts to whatever the project is (e.g., "What exists today that's related to this project? Walk me through the current landscape — any prior work, existing resources, tools, processes, or materials I should know about.")
  2. Universalize source type taxonomy — currently "repo | folder | file." Expand to include non-software sources (processes, relationships, documents, systems, services, etc.)
  3. Replace ALL example research tasks — currently reference `apps/agent-squad/src/`, `package.json`, etc. Replace with domain-adaptive examples that span multiple domains
  4. Universalize research tool guidance — currently lists codebase-specific tools (`Glob`, `Grep`, `browser-use`). Replace with generic guidance ("use available tools to investigate") with domain-adaptive suggestions
  5. Rewrite the gap analysis template — remove mandatory "Technical landscape" section, replace with domain-adaptive "Current State" sections that the agent populates based on what the project is
  6. Replace evidence examples — currently cite `.ts` files and `src/components/`. Use multi-domain examples
  7. Review all principles at the end — update any that reference software-specific concepts
- **Evaluation criteria:**
  - [ ] No software-specific language appears as a default or assumption (no "codebase", "repo", "tech stack", "architecture" as mandatory sections)
  - [ ] At least 3 domains are represented in examples (e.g., software, hiring, content/marketing)
  - [ ] Software projects remain well-served — when the project IS software, the agent should still explore codebases, check dependencies, etc. The skill guides this adaptation.
  - [ ] No Claude Code-specific tool names are hard-coded (no `Glob`, `Grep`, `Task`, `browser-use` as explicit instructions)
  - [ ] The orientation → research → synthesis → review stage structure is preserved
  - [ ] All cross-cutting patterns preserved: write-after-every-exchange, working memory, session resumption, human approval gate
- **Escalation triggers:** If a structural change to the stages seems needed (not just language changes), check with human
- **Dependencies:** None
- **Scope:** Large

#### Step 2: Universalize the plan skill
- **Deliverable:** Rewritten `skills/plan/SKILL.md`
- **Sub-steps:**
  1. Universalize deliverable language — "file paths, formats, components" → domain-adaptive deliverable descriptions
  2. Replace example evaluation criteria — currently references code structure. Use multi-domain examples
  3. Ensure step-sizing guidance works across domains — "completable in a single focused agent session" is good; make sure guidance doesn't assume file-based outputs only
  4. Remove any hard-coded tool references
- **Evaluation criteria:**
  - [ ] No software-specific assumptions in deliverable or evaluation guidance
  - [ ] Workstream → step → evaluation criteria → handoff gate structure preserved exactly
  - [ ] Examples span at least 2 domains
  - [ ] No platform-specific tool names hard-coded
  - [ ] All cross-cutting patterns preserved
- **Escalation triggers:** If step-sizing guidance needs rethinking for non-software domains
- **Dependencies:** None (can reference Step 1 patterns but not blocked by it)
- **Scope:** Medium

#### Step 3: Universalize the work skill
- **Deliverable:** Rewritten `skills/work/SKILL.md`
- **Sub-steps:**
  1. Universalize execution guidance — "file editing, code writing, web research" → domain-adaptive ("produce the deliverable using whatever approach the project requires")
  2. Rewrite work log template — "Files created/modified" → "What was produced" or similar abstraction that works for file and non-file deliverables
  3. Ensure self-evaluation guidance works across domains — the evaluate stage should apply whether the deliverable is code, a document, a process, or a decision
  4. Address the open question about non-file deliverables — for projects like fundraising or hiring, "deliverables" may include completed outreach, documented decisions, or process artifacts that the agent helps create and track
  5. Remove any hard-coded tool references
- **Evaluation criteria:**
  - [ ] Work log template accommodates both file-based and non-file deliverables
  - [ ] Self-evaluation loop works regardless of deliverable type
  - [ ] No software-specific language as defaults
  - [ ] The pickup → execute → evaluate → present → feedback → advance cycle preserved exactly
  - [ ] All cross-cutting patterns preserved
- **Escalation triggers:** If non-file deliverable handling requires a structural change to the step cycle
- **Dependencies:** None
- **Scope:** Medium

#### Step 4: Universalize the intent skill
- **Deliverable:** Rewritten `skills/intent/SKILL.md`
- **Sub-steps:**
  1. Replace "Do you have access to a code base?" in setup — use domain-agnostic orientation ("What context are you working in? Do you have existing materials, resources, or prior work related to this project?")
  2. Replace software examples in dimension guidance — "backend APIs", "frontend framework" → multi-domain examples
  3. Universalize clarify-stage research guidance — "Search the codebase" → "Research existing context"
  4. Remove any hard-coded tool references
- **Evaluation criteria:**
  - [ ] Setup orientation works for any project domain without assuming software
  - [ ] Intent dimension examples span at least 2 domains
  - [ ] No platform-specific tool names hard-coded
  - [ ] The braindump → organize → clarify → crystallize → validate structure preserved exactly
  - [ ] All cross-cutting patterns preserved
- **Escalation triggers:** None expected — changes are small
- **Dependencies:** None
- **Scope:** Small

#### Step 5: Universalize the reflect skill
- **Deliverable:** Rewritten `skills/reflect/SKILL.md`
- **Sub-steps:**
  1. Replace "anything in the repo or outside it" → domain-agnostic language ("anything related to this project — documents, tools, processes, or external resources — that should be updated")
  2. Scan for any other software-leaning language (minimal expected)
- **Evaluation criteria:**
  - [ ] No software-specific language as defaults
  - [ ] The gather → reflect → close structure preserved exactly
  - [ ] All cross-cutting patterns preserved
- **Escalation triggers:** None expected — changes are tiny
- **Dependencies:** None
- **Scope:** Small

### Workstream 2: Package for Release
**Purpose:** Everything needed to go from "working universal plugin" to "published open source marketplace plugin." Retire SPEC.md, write the marketplace README, update metadata, create distribution files.
**Gaps addressed:** Gap 2 (README), Gap 3 (marketplace.json), Gap 4 (LICENSE), Gap 5 (SPEC.md retirement), Gap 6 (plugin.json), Gap 7 (CLAUDE.md)
**Handoff gates:**
- Requires from Workstream 1: All 5 skill SKILL.md files rewritten and approved (Step 5 complete)

#### Step 6: Retire SPEC.md and clean up repo
- **Deliverable:** SPEC.md deleted, `.gitignore` updated, repo cleaned
- **Sub-steps:**
  1. Verify all cross-cutting patterns from SPEC.md are present in the skills (write-after-every-exchange, working memory, loop state, human approval gates, intent revision handling, session resumption). If any are missing, add them to the relevant skill(s) before deleting SPEC.md.
  2. Delete SPEC.md
  3. Update `.gitignore` to exclude: `.obsidian/`, `way-docs/`, `.DS_Store`
  4. Verify no remaining files reference SPEC.md
- **Evaluation criteria:**
  - [ ] SPEC.md is deleted
  - [ ] `.gitignore` excludes `.obsidian/`, `way-docs/`, `.DS_Store`
  - [ ] No remaining references to SPEC.md in any file
  - [ ] All cross-cutting patterns from SPEC.md are preserved in the skills (verify each: write-after-every-exchange, working memory, loop state as state machine, human approval gates, intent revision handling, session resumption)
- **Escalation triggers:** If a cross-cutting pattern from SPEC.md is NOT in the skills and needs to be added
- **Dependencies:** WS1 complete (skills must be self-sufficient)
- **Scope:** Small

#### Step 7: Rewrite README and CLAUDE.md
- **Deliverable:** Rewritten `README.md` and `CLAUDE.md`
- **Sub-steps:**
  1. Write README for a marketplace audience:
     - Hook: what The Way is and why it matters (the "slow down to go fast" value proposition)
     - The five phases: accurate descriptions matching the actual universalized skills
     - Installation: marketplace install AND local dev (`--plugin-dir`)
     - Project structure: accurate file tree showing what gets created
     - Key patterns: brief explanation of the design principles
     - No mention of SPEC.md, no "coming soon" skills, no external framework links
  2. Update CLAUDE.md with minimal trigger guidance:
     - Brief description of The Way
     - When to suggest each skill (trigger conditions)
     - Keep it to ~10-15 lines max
- **Evaluation criteria:**
  - [ ] README accurately describes all 5 skills as they actually work (not SPEC.md descriptions)
  - [ ] README includes both marketplace and local installation instructions
  - [ ] README communicates the value proposition in the first paragraph
  - [ ] README does not reference SPEC.md, "coming soon" features, or external repos
  - [ ] CLAUDE.md includes trigger conditions for when to suggest each skill
  - [ ] CLAUDE.md is under 20 lines
- **Escalation triggers:** If the user wants to review the README tone/positioning before finalizing
- **Dependencies:** WS1 complete (accurate skill descriptions), Step 6 (SPEC.md retired)
- **Scope:** Medium

#### Step 8: Create distribution files
- **Deliverable:** Updated `plugin.json`, new `marketplace.json`, new `LICENSE`
- **Sub-steps:**
  1. Update `.claude-plugin/plugin.json`: new description, updated keywords (remove "project-management", add domain-agnostic terms), bump version to 1.0.0
  2. Create `.claude-plugin/marketplace.json` with plugin entry using relative path source (monorepo pattern)
  3. Add MIT `LICENSE` file to repo root
- **Evaluation criteria:**
  - [ ] plugin.json description matches universal framing (no SPEC.md language, no software-specific terms)
  - [ ] plugin.json keywords are domain-agnostic
  - [ ] plugin.json version is 1.0.0
  - [ ] marketplace.json is valid and follows the Claude marketplace schema (name, owner, plugins array with source)
  - [ ] LICENSE file exists with MIT text, correct author name, and current year
  - [ ] Plugin is installable: `claude --plugin-dir .` works with the final structure
- **Escalation triggers:** If marketplace.json validation fails
- **Dependencies:** Step 7 (README finalized), Step 6 (cleanup done)
- **Scope:** Small

## Execution Sequence

1. **WS1 Step 1: Gap skill** — biggest rewrite, sets the pattern for all other skill rewrites
2. **WS1 Step 2: Plan skill** — second-largest rewrite, follows patterns from Step 1
3. **WS1 Step 3: Work skill** — addresses the non-file deliverable question
4. **WS1 Step 4: Intent skill** — small changes, follows established patterns
5. **WS1 Step 5: Reflect skill** — tiny changes, closes out WS1
6. **WS2 Step 6: SPEC.md retirement** — cleanup before writing new docs
7. **WS2 Step 7: README + CLAUDE.md** — the marketplace face of the plugin
8. **WS2 Step 8: Distribution files** — final packaging

## Risks

- **Over-abstracting kills warmth:** If domain-adaptive examples become too generic ("research the current state"), the skills lose the conversational quality that makes The Way work. Mitigation: use concrete multi-domain examples rather than abstract language.
- **Gap skill rewrite scope creep:** The gap skill is the biggest rewrite and could expand if structural changes seem needed. Mitigation: preserve the 4-stage structure; only change language, examples, and templates.
- **README positioning:** Writing for a marketplace audience is different from internal docs. The tone needs to sell without overselling. Mitigation: focus on the core insight (AI needs clear intent to do complex work) and let the framework speak for itself.

## Progressive Commitment

- **Firm:** WS1 Steps 1-5 (skill rewrites are well-understood — same structure, new language), WS2 Step 6 (SPEC.md retirement is straightforward), WS2 Step 8 (distribution files are templated)
- **Provisional:** WS2 Step 7 (README — tone and positioning may need iteration with the human)
- **Directional:** None — all steps are well-defined
