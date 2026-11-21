# Work Log — Step 4: Universalize the intent skill
Date: 2026-03-01

## What was done
Made 3 targeted edits to `skills/intent/SKILL.md` to remove software-specific assumptions in setup orientation, dimension examples, and research guidance.

## Decisions made
- **Setup orientation**: Changed from "Do you have access to a code base?" to "Are there existing materials, resources, or prior work related to this project that you can access?" This works for any domain — code, documents, processes, prior campaigns, whatever.
- **Dimension coverage examples**: Changed "backend APIs" to "a backend service, a hiring process" and "internal tools" to "an internal tool, a personal workflow." Two domains per example, one software and one not.
- **Research guidance examples**: Changed "Which frontend framework should we use?" to "What's the standard approach for this kind of project?" — domain-agnostic while still showing when research helps vs. when it's a judgment call.

## What was produced
- `skills/intent/SKILL.md`: 3 targeted edits — setup orientation, dimension examples, research guidance

## Self-Evaluation

### Setup orientation works for any project domain without assuming software
**Verdict:** Pass
**Evidence:** Line 18 now reads "Are there existing materials, resources, or prior work related to this project that you can access? Are you working in a specific project folder, or is this starting from scratch?" No mention of codebases, repos, or software-specific context. Works equally for software, hiring, fundraising, content, or any other domain.

### Intent dimension examples span at least 2 domains
**Verdict:** Pass
**Evidence:** Line 102: "a backend service, a hiring process" (software + hiring) and "an internal tool, a personal workflow" (software + personal/operations). Project name examples at line 19 already span domains: `landing-page`, `onboarding-redesign`, `q3-content-strategy`.

### No platform-specific tool names hard-coded
**Verdict:** Pass
**Evidence:** Lines 195-198 now use generic guidance: "Search the web for best practices", "Search any accessible project files", "delegate to available research tools or subagents." Grep for WebSearch, WebFetch, Glob, Grep, Task, Explore returns zero matches.

### The braindump → organize → clarify → crystallize → validate structure preserved exactly
**Verdict:** Pass
**Evidence:** All five stages preserved in order: Stage 1: Braindump (line 43), Stage 2: Organize (line 114), Stage 3: Clarify (line 184), Stage 4: Crystallize (line 239), Stage 5: Validate (line 290).

### All cross-cutting patterns preserved
**Verdict:** Pass
**Evidence:** Write-after-every-exchange: braindump updated after each response (lines 59-76), clarifications recorded (lines 212-231). Session resumption: lines 363-375 with stage-based recovery. Human approval gate: Stage 5 (lines 290-338) with present → feedback → lock flow. Backlog writing: lines 340-361.

## Overall
**Verdict:** Pass
All 5 evaluation criteria satisfied. The intent skill needed minimal changes — it was already the most domain-agnostic of the five skills. Three targeted edits were sufficient: setup orientation, dimension examples, and research guidance.

## For the human
This was the lightest rewrite as expected. The intent skill's core — braindump → organize → clarify → crystallize → validate — was already universal. The main issue was the setup question ("Do you have access to a code base?") which immediately framed every project as software. That's gone now.
