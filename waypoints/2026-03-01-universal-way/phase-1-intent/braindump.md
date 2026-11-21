# Intent Braindump — universal-way
Date: 2026-03-01

## Exchange 1

**Question:** (Initial invocation — user described the project unprompted)

**Raw answer:** "I want to ensure that the-way-plugin is compatible with all kinds of projects and intents - not only those related to software development. I want the framework to be as abstract and simple as possible - a beautiful timeless and elegant workflow that leads anyone from intent to real progress, no matter what the intent entails. It should work inside claude code but also inside of the claude desktop application. I then want to open source it and publish it to a claude plugin marketplace."

**Reflection:** Three clear threads here. First, universality — the current skills lean software (codebase exploration, file-based deliverables). The user wants the framework to work for content strategy, research projects, event planning, anything. Second, aesthetic elegance — "beautiful, timeless, elegant" signals this isn't just about features but about the *feel* of the workflow. Third, distribution — open source, marketplace, dual-platform (CLI + Desktop). The distribution goal creates real constraints: the filesystem-as-state pattern works in Claude Code but may not map cleanly to Claude Desktop. This could be the central design tension.

**Dimensions touched:** purpose, constraints, non-goals (implicitly: not just for developers)

---

## Exchange 2

**Question:** When you say 'all kinds of projects' — can you give me two or three examples of non-software projects where you'd want this framework to shine?

**Raw answer:** "Fundraising, hiring/recruiting for a specific role, migrating from one system to another."

**Reflection:** These are excellent stress tests. Fundraising is relationship-heavy, milestone-driven, and the "deliverables" are pitch decks, outreach sequences, investor lists — not code. Hiring is process-heavy with heavy human judgment (evaluating candidates). Migration is more technical but still not pure code — it involves planning, data mapping, coordination. What these share: they're all multi-step, they all benefit from clear intent, and they all need a human in the loop for key decisions. What they challenge: the current Phase 4 (Work) is very file-deliverable-oriented. Fundraising "deliverables" might be conversations had, introductions made, term sheets negotiated — things that don't live on a filesystem. The gap analysis phase also currently assumes codebase exploration. These examples sharpen the universality challenge.

**Dimensions touched:** audience (not just developers), purpose (framework for any structured endeavor)

---

## Exchange 3

**Question:** You used the words 'beautiful, timeless, and elegant.' Is this about the user experience, the simplicity of the framework's concepts, or both — and which matters more?

**Raw answer:** "Both, but experience first."

**Reflection:** This is a strong design signal. The user sees The Way as an experience product first, conceptual framework second. "The experience is the product" means the pacing of questions, the quality of reflections, the feel of the agent as a thinking partner — those matter more than having the cleanest possible abstraction. But they also said "both" — so the concepts need to be clean too, just in service of the experience. This has implications for how we approach universalization: we shouldn't strip the framework down to something so abstract it loses its warmth. The personality and collaborative feel of the conversation IS the value. This connects to the marketplace distribution goal — the experience is what will differentiate this from a generic project management template.

**Dimensions touched:** primary action (the experience of structured collaboration), success criteria (it should *feel* right)

---

## Exchange 4

**Question:** In Claude Desktop, what does using The Way look like? Is the conversation the artifact, or do files still get generated somewhere?

**Raw answer:** "I would advise people to use it in Claude Cowork, which has file system access. So that should work."

**Reflection:** This simplifies the platform challenge significantly. Claude Cowork (the collaborative workspace in Claude Desktop) has filesystem access, which means the file-based state pattern can work there too. The user isn't asking for a fundamentally different architecture for Desktop — they're planning to direct users toward the mode that already supports files. This means the core filesystem-as-state design can stay. The distribution challenge shifts from "how do we work without files" to "how do we package this for both Claude Code and Cowork." The key constraint now is: whatever we build must be installable/usable in both environments. That's a packaging/distribution question, not an architecture question.

**Dimensions touched:** constraints (must work in Claude Code + Claude Cowork, both have filesystem access)

---

## Exchange 5

**Question:** When making this universal, are you thinking: rewrite skills to be domain-agnostic, create a universal core + domain extensions, or something different?

**Raw answer:** "Rewrite to be domain-agnostic, and then consider adding sub-skills that agents can evoke under certain specific situations. Claude plugins can even define specific subagents that the main agent can evoke: https://code.claude.com/docs/en/plugins-reference. We could also tap into the hooks, as that might be useful for some elements of the way."

**Reflection:** This is a layered architecture: domain-agnostic core skills that are the universal workflow, plus sub-skills/subagents that activate contextually. The plugin reference link is important — this means Claude's plugin system already supports sub-skill invocation and hooks, which gives us concrete technical primitives to build on. The user is thinking about this as a proper plugin architecture, not just prompt files. Hooks could serve interesting purposes — maybe auto-triggering the review skill, or running validation on phase transitions. The key insight: universality at the skill level (the five phases stay the same for any project), specificity at the sub-skill level (code evaluation for software, candidate scoring for hiring, etc.). This is an elegant approach.

**Dimensions touched:** primary action (domain-agnostic core + contextual sub-skills), constraints (must use Claude plugin architecture: skills, subagents, hooks)

---

## Exchange 5.5 — Agent Research

**Plugin Architecture Reference** (from https://code.claude.com/docs/en/plugins-reference and /plugin-marketplaces):

Key primitives available:
- **Skills**: `/name` shortcuts — directories with `SKILL.md`. This is what the current 5 phases are.
- **Agents (subagents)**: Markdown files in `agents/` with frontmatter. Claude invokes them automatically based on task context. Could serve as domain-specific extensions (e.g., a code-evaluation subagent, a content-review subagent).
- **Hooks**: Event handlers responding to `PreToolUse`, `PostToolUse`, `SessionStart`, `Stop`, `SubagentStart`, `TaskCompleted`, `PreCompact`, etc. Could automate phase transitions, validation, or review triggers.
- **MCP servers**: External tool integrations. Could connect to project management tools, CRMs, etc.
- **Plugin manifest**: `.claude-plugin/plugin.json` with metadata, version, component paths.
- **Marketplace**: `marketplace.json` in a GitHub repo. Users add with `/plugin marketplace add owner/repo` and install with `/plugin install plugin-name@marketplace-name`.
- **Scopes**: user, project, local, managed. Project scope commits to `.claude/settings.json` for team sharing.

Distribution path: GitHub repo → marketplace.json → users install via CLI. Supports semantic versioning, release channels (stable/latest), private repos.

---

## Exchange 6

**Question:** What does success look like? What should this never become?

**Raw answer:** "This framework should become the missing piece in the AI world today. It's not realistic for AI to execute and one shot complex things unless the intent is extremely clear, and the artifacts supporting the actual work are helpful for those that are working (be that agents or humans). The framework and experience should also just become the most comfortable and reliable way for a person to clarify and manifest their intent - i.e to get shit done. I don't want this to be an annoying experience - just an elegant and opinionated framework that moves you through the value creation process in a systematic way that takes a bit more time to get started (because you need to think more) but the end result is a higher quality end result, always."

**Reflection:** This is the clearest articulation of the thesis yet. The user is positioning The Way as infrastructure for the AI era — the insight that AI can't one-shot complex things without clear intent, and that no one is providing the structured path from fuzzy idea to clear specification. Two key design tensions surfaced: (1) "opinionated" vs "not annoying" — the framework has a point of view about how work should happen, but it shouldn't feel heavy or bureaucratic. The elegance is in being opinionated without being burdensome. (2) "takes more time to get started" but "higher quality end result, always" — this is a trade-off the user is explicitly embracing. The value proposition is: slow down to go fast. The non-goal is implicit but clear: this is NOT a speed tool, NOT a shortcut, NOT an automation that removes thinking. It's a thinking amplifier. The "always" in "higher quality end result, always" is a bold claim — that's the bar.

**Dimensions touched:** purpose (the missing piece — structured intent for AI-era work), success criteria (most comfortable way to clarify intent, higher quality end results always), non-goals (not a shortcut, not annoying bureaucracy), voice & tone (elegant, opinionated, not heavy)

---

## Organized View

### What I heard — by dimension

**Purpose:**
The Way is the missing infrastructure for the AI era. AI cannot one-shot complex work without clear intent and well-structured supporting artifacts. The Way provides the structured path from fuzzy idea to clear specification to real progress — for any kind of project, not just software. It's a value creation framework: Intent → Gap → Plan → Work → Reflect, where each phase produces artifacts that make the next phase (and the humans/agents doing the work) more effective.

**Audience:**
Anyone using Claude (Code or Desktop/Cowork) who wants to do complex, multi-step work. Explicitly not limited to developers. Target use cases span software development, fundraising, hiring/recruiting, system migrations, content strategy, and any structured endeavor where intent clarity determines outcome quality. The audience ranges from individual makers to teams.

**Action and work needed:**
1. Rewrite all five skill prompts (intent, gap, plan, work, reflect) to be domain-agnostic — strip software-specific assumptions (codebase exploration, file-based deliverables, code evaluation) and replace with universal patterns that adapt to the project domain.
2. Restructure the plugin to use the full Claude plugin architecture: skills as the core phases, subagents for domain-specific extensions (code evaluation, content review, candidate assessment, etc.), and hooks for automation (phase transitions, validation, review triggers).
3. Package for distribution: plugin manifest, marketplace.json, GitHub repo, open source license.
4. Ensure compatibility with both Claude Code (terminal) and Claude Desktop/Cowork (GUI with filesystem access).
5. Refine the experience: pacing, conversational quality, the feel of working with a thinking partner. The experience IS the product.

**Success Criteria:**
- The framework works for any project domain — software, fundraising, hiring, migration — without the user needing to configure or adapt it.
- The experience is the most comfortable and reliable way for a person to clarify and manifest their intent.
- Projects that go through The Way produce higher quality end results than projects that don't, always.
- It's elegant and opinionated without being annoying or bureaucratic.
- It's published as an open source Claude plugin, installable from a marketplace.
- It works in both Claude Code and Claude Desktop/Cowork.

**Constraints:**
- Must use the Claude plugin architecture (skills, subagents, hooks, plugin manifest, marketplace).
- Filesystem-as-state pattern — both Claude Code and Cowork have filesystem access.
- Must be packageable as a self-contained plugin directory (no external dependencies outside the plugin root).
- The existing five-phase structure (Intent → Gap → Plan → Work → Reflect) and the Specify → Generate → Evaluate triad are the conceptual backbone — universalize them, don't replace them.

**Non-Goals:**
- NOT a speed tool or shortcut. It deliberately trades startup time for outcome quality.
- NOT an automation that removes thinking. It's a thinking amplifier.
- NOT only for software development (this is the current state; the project is about moving past it).
- NOT a project management tool with forms and dashboards. The interface is conversation.
- NOT a framework that requires domain-specific configuration before use. It should adapt automatically.

**Voice & tone (context-dependent):**
- Elegant, opinionated, warm. The agent is a thinking partner, not a form to fill out.
- "Experience first" — the quality of the conversation and pacing matters as much as the conceptual framework.
- "Beautiful, timeless" — the design should feel like it could have existed 10 years ago and still work 10 years from now.

### Gaps and tensions I noticed

- **Success measurement gap**: "Higher quality end result, always" is the bar — but how do we measure this? For software we can look at code quality, test coverage, etc. For fundraising, it's dollars raised. For hiring, it's quality of hire. The framework's success criteria are domain-dependent, which creates a paradox with the universality goal. The intent.md success criteria per project may be the answer — each project defines its own "done."
- **Subagent scope tension**: The user wants domain-agnostic core skills + contextual subagents. But how many subagents ship with v1? Is the plugin just the universal core, with subagents as a future extension model? Or do we ship a few starter subagents (software, content, research)?
- **Hooks specifics gap**: The user mentioned hooks as useful but didn't specify what they'd do. This needs clarification — are hooks a v1 concern or future?
- **SPEC.md vs. new vision tension**: The current SPEC.md is thorough and well-designed but contains software-specific patterns. The question is: do we rewrite SPEC.md as part of this project, or is SPEC.md the "old" version and the universalized skills replace it?
- **"Timeless" vs. platform-specific**: "Beautiful and timeless" as a design goal sits in tension with being a Claude-specific plugin. If the plugin system changes, the implementation changes. The timelessness needs to live in the *concepts and experience*, not the packaging.

### Scope signals
- **Core:** Universalizing the five skill prompts, restructuring the plugin directory for the plugin architecture (skills + subagents + hooks + manifest), open sourcing and publishing to a marketplace.
- **Potentially separable:**
  - **Domain-specific subagent packs**: Creating subagents for specific domains (software, hiring, fundraising) could be its own project after the universal core ships.
  - **The Way for teams/multi-agent**: The SPEC.md mentions a multi-terminal pattern with separate builder/evaluator terminals. This is a distinct project from universalization.
  - **Experience refinement/polish pass**: Deep work on conversational pacing, prompt quality, the "feel" — could be a dedicated project after the structural changes land.

### Scope Decision (user confirmed)

**In scope for v1:** Universalize the five skill prompts + restructure as a proper Claude plugin + package for marketplace + open source. The core only.

**Parked for later:** Domain-specific subagent packs, hooks automation, multi-agent/teams pattern, dedicated experience polish pass.

---
