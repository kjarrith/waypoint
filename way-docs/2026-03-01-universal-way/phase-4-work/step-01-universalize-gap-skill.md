# Work Log — Step 1: Universalize the gap skill
Date: 2026-03-01

## What was done
Rewrote `skills/gap/SKILL.md` to be domain-agnostic while keeping software as a first-class domain. All 7 sub-steps from the plan were addressed in a single rewrite.

## Decisions made
- **Source type taxonomy**: Expanded from `repo | folder | file | external-url | design-file | database | service | other` to `document | codebase | website | tool/service | process | dataset | design-asset | relationship/contact | folder | other`. Chose types that span domains without being so abstract they lose meaning.
- **"Technical landscape" → "Relevant landscape"**: Renamed the mandatory section and made it domain-adaptive with inline examples for software, hiring, and content. This avoids forcing a "tech stack" section on non-software projects while still guiding software projects to document their stack.
- **Research plan examples format**: Used `{domain: "example"}` inline format to show multi-domain examples without creating separate sections per domain. This keeps the template compact while showing how to adapt.
- **Tool guidance approach**: Replaced the enumerated tool list (`Glob`, `Grep`, `Read`, `Task`, `Explore`, `browser-use`) with generic functional categories (files/documents, web research, live inspection, deep exploration) plus a domain-adaptive paragraph that describes what investigation looks like for software vs. hiring vs. content projects.
- **Evidence examples**: Used two contrasting examples from different domains — "47 components with no shared design system" (software) and "3 open roles with no structured interview process" (hiring) — to demonstrate specificity without assuming a single domain.
- **"Files/URLs examined" → "Evidence examined"**: Broadened the findings log field to accommodate non-file evidence (observations, conversations, metrics).

## Files created/modified
- `skills/gap/SKILL.md`: Full rewrite — same structure, universalized language/examples/templates

## Self-Evaluation

### No software-specific language appears as a default or assumption
**Verdict:** Pass
**Evidence:** Searched the full file for software-specific terms used as defaults. "codebase", "tech stack", "architecture", "repo" appear only within explicitly labeled domain examples (e.g., "For software: tech stack, architecture, dependencies") or as one option in a list (e.g., source type "codebase" among 10 types). No section title, opening prompt, or instruction assumes the project is software.

### At least 3 domains are represented in examples
**Verdict:** Pass
**Evidence:** Three domains appear consistently throughout: software (lines 111-112, 145, 200, 203, 245), hiring (lines 113, 145, 203, 245), and content (lines 114, 145, 200, 203). Operations/marketing also appear as category examples in the gap analysis template (line 200).

### Software projects remain well-served
**Verdict:** Pass
**Evidence:** Software gets concrete guidance at every stage: "codebase" is a source type (line 86), research plan includes "Explore the src/ directory" and "Read package.json" examples (lines 111-112), research guidance says "For a software project, you'll explore codebases, check dependencies, and read architecture docs" (line 145), template suggests "codebase/design/infrastructure" as a category structure (line 200), and landscape section guides "For software: tech stack, architecture, dependencies" (line 203).

### No Claude Code-specific tool names are hard-coded
**Verdict:** Pass
**Evidence:** Grep for `Glob`, `Grep`, `browser-use`, `Task`, `Explore`, `Read` (as tool names) returns zero matches. Tool guidance uses functional categories only: "Search for, read, and analyze any accessible files", "use available subagent or task delegation tools."

### The orientation → research → synthesis → review stage structure is preserved
**Verdict:** Pass
**Evidence:** All four stages present in the same order: Stage 1: Orientation (line 66), Stage 2: Research (line 133), Stage 3: Synthesis (line 180), Stage 4: Review (line 251). Transition prompts between stages preserved.

### All cross-cutting patterns preserved
**Verdict:** Pass
**Evidence:** Write-after-every-exchange: working memory updated after each orientation response (lines 80-91) and each research task (lines 147-158), plus principle at line 329. Working memory: initialization (lines 31-44), key sources (82-91), research plan (104-123), findings log (147-158). Session resumption: full section at lines 309-321 with stage-based recovery. Human approval gate: Stage 4 (lines 251-307) with present → feedback → intent revision → lock flow.

## Overall
**Verdict:** Pass
All 6 evaluation criteria satisfied. The rewrite preserves the full structure and cross-cutting patterns while making the language, examples, templates, and tool guidance domain-agnostic. Software remains well-served through explicit domain-adaptive guidance rather than being the default assumption.

## For the human
The biggest subjective call was the source type taxonomy. The original had 7 types; the new one has 10. I added `process`, `dataset`, `design-asset`, and `relationship/contact` to cover non-software domains, and consolidated `repo` into `codebase`. If any of these feel wrong or if you'd prefer a different taxonomy, that's an easy adjustment. The rest of the changes are straightforward language universalization.
