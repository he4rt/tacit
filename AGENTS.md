# AGENTS.md

Guidance for AI agents working **on** this repository (not for Tacit users).

## What this is

Tacit is a plugin for AI coding agents that teaches users the code their agent writes. It is markdown-first: there is no application code, only skills, shared references, a concept catalog, and a validation script.

## Layout

- `.claude-plugin/` — Claude Code plugin and marketplace manifests. Keep `version` identical in both (release-please bumps them).
- `skills/<name>/SKILL.md` — user-facing workflows. Frontmatter `name` must match the folder.
- `references/` — shared rules all skills follow. Skills link to them with paths relative to the skill directory (`../../references/...`).
- `concepts/<track>/<id>.md` — the concept catalog. `concepts/INDEX.md` is generated; never edit it by hand.
- `scripts/check.mjs` — validator and index generator (Node, no dependencies).

## Rules

- Run `node scripts/check.mjs` after changing concepts, skills or manifests; commit the regenerated index.
- Keep skills agent-agnostic: no agent-specific tool names, no features that only one agent has in the core flow. Agent-specific extras go in clearly separated files.
- Everything in the repo is written in English. Skills instruct the agent to reply in the learner's language.
- Use Conventional Commits.
- Update README.md when adding or renaming skills, and CONTRIBUTING.md when changing the contribution flow.
