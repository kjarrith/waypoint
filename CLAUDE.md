# The Way plugin

Five skills (`skills/*/SKILL.md`) take a project from intent to reflection. `conventions.md` is the single source of truth for the folder layout, IDs, documents and phase order; every skill reads it first and must not restate it.

When editing:

- Keep the skills short. Give goals, the output's shape and a few rails, and trust the model with the rest. No scripted lines, no per-exchange file writes, no resume logic: the conversation is the working memory and the phase documents are the state.
- A rule that more than one skill needs goes in `conventions.md`.
- Bump `version` in `.claude-plugin/plugin.json` on every change that users should pick up.
