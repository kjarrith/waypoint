# Clarifications — universal-way

## Clarification 1: What happens to SPEC.md

**Gap/tension:** The current SPEC.md is thorough but software-leaning. As skills are universalized, SPEC.md either needs to evolve or be replaced. Having both a spec and skill files creates a dual-authority problem.

**Research:** N/A (judgment call)

**Question asked:** As we universalize the skills, what happens to SPEC.md? Rewrite it as the universal spec, keep it as historical, or replace it?

**User's answer:** "Replace with README for marketplace." Ditch SPEC.md entirely. The plugin needs a good README for the marketplace, not an internal spec.

**Impact on intent:** The SKILL.md files become the sole authority for how each phase works. SPEC.md is retired. The README becomes the public-facing document — it needs to sell the framework and explain how to use it, not specify internal behavior. This simplifies the project: we're rewriting skills + creating a README + plugin packaging. No spec maintenance.

---

## Clarification 2: CLAUDE.md scope

**Gap/tension:** The plugin's CLAUDE.md shapes how Claude behaves in projects where The Way is installed. It could be minimal (just awareness) or philosophy-infused (shaping Claude's general behavior).

**Research:** N/A (judgment call)

**Question asked:** Should CLAUDE.md be a minimal orientation or carry the framework's philosophy?

**User's answer:** Minimal orientation. Just tell Claude the skills exist and when to suggest them.

**Impact on intent:** CLAUDE.md stays light — it's a signpost, not a manifesto. The philosophy lives in the skill prompts themselves, where it activates when invoked. This keeps the plugin non-intrusive: installing The Way doesn't change how Claude behaves for other tasks. It only activates when you call it.

---

## Clarification 3: License and distribution structure

**Gap/tension:** Open source release needs a license choice and repo structure decision.

**Research:** N/A (preference)

**Question asked:** License preference? Same repo or separate marketplace repo?

**User's answer:** MIT license, marketplace.json in the same repo. Simple monorepo approach.

**Impact on intent:** Single repo contains the plugin AND the marketplace entry. Users add the marketplace via GitHub repo URL, then install the plugin. MIT license — maximally permissive. Simplifies maintenance: one repo, one version, one release process.

---
