# Working Memory — universal-way
Last updated: 2026-03-01

## Human Context
- All relevant material lives in this repo (the-way-plugin/).
- User pointed to https://claudemarketplaces.com/ as a reference for existing Claude plugin marketplaces.
- CRITICAL NUANCE: "Do not over-index into non-dev stuff. I also want this to be really useful for devs." The goal is NOT to strip software out — it's to make the framework domain-agnostic while keeping software as a first-class experience. The skills should adapt to whatever the project is, not pretend software doesn't exist.

## Research Progress

### Key Sources

### Source 1: the-way-plugin repo
- **Type:** repo
- **Location:** /Users/k_thorisson/code/the-way-plugin/
- **Accessible:** yes
- **Relevance:** This IS the project. Contains current skills, SPEC.md, CLAUDE.md, directory structure.
- **Notes:** Everything that needs to change lives here.

### Source 2: Claude plugin/marketplace documentation
- **Type:** external-url
- **Location:** https://code.claude.com/docs/en/plugins-reference, https://code.claude.com/docs/en/plugin-marketplaces
- **Accessible:** yes (already fetched during intent phase)
- **Relevance:** Defines the target plugin structure (manifest, skills, agents, hooks, marketplace.json)
- **Notes:** Already captured in braindump Exchange 5.5.

### Source 3: Claude marketplaces directory
- **Type:** external-url
- **Location:** https://claudemarketplaces.com/
- **Accessible:** yes
- **Relevance:** Reference for how other plugins are packaged and distributed. Competitive landscape.
- **Notes:** User-provided reference.

### Research Plan

### Automated research (agent can do independently)
- [x] Read all 5 SKILL.md files and audit for software-specific language/assumptions
- [x] Examine current directory structure vs. Claude plugin architecture requirements
- [x] Check for existing plugin infrastructure (.claude-plugin/, plugin.json, marketplace.json, LICENSE)
- [x] Read current CLAUDE.md and README.md for baseline
- [x] Read current SPEC.md for cross-cutting patterns that skills reference
- [x] Fetch https://claudemarketplaces.com/ to understand marketplace landscape and competing/similar plugins
- [x] Check Claude plugin docs for any Cowork-specific requirements or limitations

### Needs human input
- (none identified)

### Findings Log

### Finding 1: Intent skill — mostly domain-agnostic with minor software leaks
**Research task:** Audit SKILL.md files for software-specific language
**What I found:** The intent skill is the most universal of the five. Two software-specific leaks:
- Line 18: Setup asks "Do you have access to a code base?" — assumes software context
- Line 102: Example mentions "backend APIs" and "internal tools" — software examples
- Line 196: Clarify stage says "Search the codebase" — assumes code exists
- Line 200: Example question "Which frontend framework should we use?" — software-specific
Otherwise, the intent skill's structure (braindump → organize → clarify → crystallize → validate) is inherently domain-agnostic.
**Relevant to:** Success criterion 1 (domain-agnostic skills)
**Gap signal:** Small gap — a few phrases to universalize, but the structure works

### Finding 2: Gap skill — MOST software-heavy, needs major rewrite
**Research task:** Audit SKILL.md files for software-specific language
**What I found:** The gap skill has deep software assumptions throughout:
- Line 74: Orientation opening asks about "repos, folders, Figma files, existing sites" — software/design-leaning
- Lines 86: Source types list "repo | folder | file" — file/code-centric taxonomy
- Lines 110-113: ALL example research tasks are software-specific: "Explore `apps/agent-squad/src/`", "Read `docs/architecture.md`", "Scan `package.json`", "Search codebase for existing components"
- Lines 137-140: Research tools listed are codebase-specific: "Codebase exploration: Glob, Grep, Read", "Browser inspection: browser-use"
- Lines 197-200: Current State template has a mandatory "Technical landscape" section with "tech stack, architecture, infrastructure"
- Line 242: Evidence example is pure software: "`src/components/` directory has 47 files"
- Line 325: Evidence example references `.ts` source files
The overall orientation → research → synthesis flow is universal, but the specific examples, templates, and tool guidance are all software-centric.
**Relevant to:** Success criterion 1, open question about gap skill granularity
**Gap signal:** MAJOR gap — most rewriting needed here

### Finding 3: Plan skill — moderately software-leaning
**Research task:** Audit SKILL.md files for software-specific language
**What I found:** The plan skill has structural universality (workstreams, steps, handoff gates) but software-leaning language:
- Line 178: Deliverables described as "specific files, components, or artifacts" — leans code
- Line 185: Example of good criteria: "SKILL.md follows YAML frontmatter + markdown body format" — very specific to THIS project
- Line 232: Deliverable template says "file paths, formats, components" — assumes file outputs
The workstream → steps → evaluation criteria → handoff gates structure is actually very universal and works for any domain.
**Relevant to:** Success criterion 1
**Gap signal:** Medium gap — structure is universal, examples and deliverable language need updating

### Finding 4: Work skill — moderately software-leaning
**Research task:** Audit SKILL.md files for software-specific language
**What I found:** The work skill has good universal structure (pickup → execute → evaluate → present → feedback → advance) but some software assumptions:
- Line 68: "file editing, code writing, web research" — lists code-writing as a primary activity
- Line 111: Work log template has "Files created/modified" — assumes file deliverables
For non-file projects (fundraising: outreach emails sent, conversations had), the "files created/modified" framing breaks down. The self-evaluation loop itself is universal.
**Relevant to:** Success criterion 1, open question about non-file deliverables
**Gap signal:** Medium gap — self-eval loop is universal, deliverable tracking needs abstraction

### Finding 5: Reflect skill — most domain-agnostic already
**Research task:** Audit SKILL.md files for software-specific language
**What I found:** The reflect skill is nearly universal already:
- Line 165: "anything in the repo or outside it (docs, READMEs, external tools)" — assumes repo context
- Otherwise the gather → reflect → close structure and the conversation arc (outcome, went well, change, surprises, next) are completely domain-agnostic
**Relevant to:** Success criterion 1
**Gap signal:** Very small gap — one line to change

### Finding 6: Plugin directory structure — mostly compliant, some gaps
**Research task:** Examine structure vs. Claude plugin architecture requirements
**What I found:**
Current structure:
```
.claude-plugin/plugin.json  ✓ (exists, valid)
skills/                     ✓ (correct location, 5 skills)
  intent/SKILL.md           ✓
  gap/SKILL.md              ✓
  plan/SKILL.md             ✓
  work/SKILL.md             ✓
  reflect/SKILL.md          ✓
CLAUDE.md                   ✓ (exists)
README.md                   ✓ (exists)
```
Missing:
- No `marketplace.json` (needed for marketplace distribution)
- No LICENSE file (MIT specified in plugin.json but actual file missing)
- No `.claude-plugin/marketplace.json` (needed if monorepo marketplace)
Present but should be handled:
- SPEC.md (should be retired per intent)
- .obsidian/ (Obsidian editor config, should be gitignored)
- way-docs/ (project artifacts, probably should be gitignored for published plugin)
- .DS_Store files in skills/ directory
**Relevant to:** Success criteria 3, 4, 8
**Gap signal:** Medium gap — structure is close, needs marketplace.json, LICENSE, cleanup

### Finding 7: plugin.json analysis
**Research task:** Check existing plugin infrastructure
**What I found:** plugin.json exists and is mostly good:
```json
{
  "name": "theway",
  "version": "0.1.0",
  "description": "A human-agent collaboration framework...",
  "author": {"name": "Kjartan Thorisson", "url": "https://github.com/kjarrith"},
  "repository": "https://github.com/kjarrith/theway-plugin",
  "license": "MIT",
  "keywords": ["workflow", "agent-collaboration", "intent", "planning", "project-management", "metaprocess"]
}
```
Issues:
- Description mentions "builder-evaluator loops" — SPEC.md language, not what /work actually does
- Keywords include "project-management" — explicitly a non-goal per intent
- No `homepage` field
- Description is software-leaning ("projects from intent to delivered value" is ok, but could be more evocative)
**Relevant to:** Success criteria 3, 8
**Gap signal:** Small gap — description and keywords need updating

### Finding 8: README analysis
**Research task:** Read current README for baseline
**What I found:** README has a good structure but multiple accuracy issues:
- "A Claude Code plugin" → should work in both Claude Code and Cowork
- Phase 4 described as "Builder-evaluator execution loops" — SPEC.md language
- Project structure shows `build-log.md`, `evaluation.md`, `status.md` per step — old SPEC.md structure; actual work skill produces single `step-{NN}-{name}.md` files
- "More skills coming: review, status" — not in v1 scope per intent
- "Requirements: Claude Code 1.0.33 or later" — probably needs updating
- Links to external "value-creation-metaprocess" doc — separate dependency
- Not written for a marketplace audience — reads more like internal dev docs
**Relevant to:** Success criterion 6 (README for marketplace)
**Gap signal:** Major gap — needs full rewrite for accuracy, audience, and marketplace positioning

### Finding 9: CLAUDE.md analysis
**Research task:** Read current CLAUDE.md
**What I found:** Current content is one line: "A human-agent collaboration plugin for use within the Claude ecosystem. Skills guide projects through: Intent → Gap → Plan → Work → Reflect."
Per the intent, CLAUDE.md should provide "minimal orientation: tells Claude the skills exist and when to suggest them." The current version is close but doesn't tell Claude WHEN to suggest the skills (trigger conditions).
**Relevant to:** Success criterion 7
**Gap signal:** Small gap — needs trigger guidance added

### Finding 10: Marketplace landscape
**Research task:** Fetch claudemarketplaces.com
**What I found:** Active ecosystem with 5+ marketplaces:
- Anthropic's official (13 plugins, dev-focused)
- wshobson/agents (73 plugins, production workflows)
- davila7/claude-code-templates (10 templates)
- henkisdabro/claudecode-marketplace (27 plugins, utilities)
- hopeoverture/worldbuilding-app-skills (26 skills, full-stack)
Key insight: ALL existing plugins are developer/software-focused. No workflow metaprocess or universal collaboration frameworks exist. The Way would be genuinely unique in this ecosystem — potentially the first non-developer-focused plugin.
**Relevant to:** Distribution, positioning, success criteria 5
**Gap signal:** Opportunity, not a gap. Unique positioning.

### Finding 11: Cowork compatibility
**Research task:** Check for terminal-specific dependencies
**What I found:** The skills reference several Claude Code-specific tools:
- `Glob`, `Grep`, `Read`, `Edit`, `Write` — filesystem tools, should work in Cowork
- `AskUserQuestion` — should work in Cowork
- `WebSearch`, `WebFetch` — should work in Cowork
- `Task` with `Explore` agents (gap skill line 142) — Claude Code specific, may not exist in Cowork
- `browser-use` (gap skill line 139) — may not exist as a standard tool
- `mkdir -p` via Bash — should work if Cowork has shell access
- All skills use filesystem-as-state (Read/Write/Edit) — should work if Cowork has filesystem access
No hard blockers found, but tool references should use generic language ("use available research tools") rather than naming specific Claude Code tools that may not exist in Cowork.
**Relevant to:** Success criterion 5 (works in both environments)
**Gap signal:** Small gap — avoid hard-coding tool names that are platform-specific

## Design Reasoning

**Intent summary:** Transform the-way-plugin from a software-centric framework into a domain-agnostic, open source Claude plugin. The five phases stay, the experience stays, the language adapts to any domain while keeping software as a first-class experience. Package for marketplace distribution.

**Gaps summary:**
1. Skill language assumes software — needs domain-adaptive framing (major: gap skill, medium: plan/work, small: intent/reflect)
2. README not written for marketplace audience (major rewrite)
3. Missing marketplace.json (new file needed)
4. Missing LICENSE file (trivial)
5. SPEC.md retirement and cleanup (delete + gitignore updates)
6. plugin.json needs updating (description, keywords)
7. CLAUDE.md needs skill trigger guidance (small addition)
8. Cowork tool compatibility (addressed as part of Gap 1)

### Complexity Assessment
**Level:** Moderate
**Reasoning:** 8 gaps, but they cluster cleanly into 2 groups: core skill rewrites (the main work, 5 files) and packaging/release (quick items with one medium README rewrite). Clear dependency: packaging depends on skills being done for accurate descriptions. No technical uncertainty — the changes are well-understood prompt engineering and file creation.
**Implications:** Two workstreams with one handoff gate. WS1 has 5 steps (one per skill). WS2 has 3 steps (cleanup, docs, distribution files). Total: 8 steps.

### Workstream Design

#### Candidate workstreams
1. **Universalize Skills**: Groups gaps 1 and 8. The core work — rewrite each skill's language, examples, and templates from "assume software" to "detect domain, adapt." Includes Cowork tool compatibility as part of each rewrite.
2. **Package for Release**: Groups gaps 2, 3, 4, 5, 6, 7. Everything needed to go from "working plugin" to "publishable open source marketplace plugin."

#### Dependencies between workstreams
- Workstream 1 must produce all 5 universalized skills before Workstream 2 can write the README (Gap 2), because README skill descriptions must be accurate.
- Workstream 2's cleanup step (SPEC.md retirement, gitignore) can technically start after WS1 Step 1, but sequencing after WS1 is cleaner.

#### Handoff gates
- **WS1 → WS2**: All 5 skill SKILL.md files are rewritten and approved. The README, plugin.json description, and CLAUDE.md can then be written to accurately reflect the skills.

#### Open questions
- Intent open question: Should cross-cutting skills (/theway:review, /theway:status) be included? Recommendation: NO for v1 per intent non-goals. Mention them in README as future.

## Open Threads
- The README links to an external repo (kjarrith/noona-way) for "the value creation metaprocess." Should this link be kept, updated, or the content brought into the README?
