# Contributing to Tacit

Thanks for helping people learn! There are three ways to contribute, from easiest to most involved.

## 1. Add or improve a concept

Concepts live in `concepts/<track>/<concept>.md`.

1. Copy `concepts/_TEMPLATE.md` to `concepts/<track>/<your-concept>.md`.
2. Fill in the frontmatter:
   - `id` must match the path (`data/indexes` for `concepts/data/indexes.md`).
   - `track` must match the folder.
   - `level`: `basic`, `intermediate` or `advanced`.
   - `prerequisites`: ids of concepts a learner should know first.
   - `signals`: code patterns that suggest the concept is present — this is how the agent recognizes it.
3. Write the sections. Guidelines:
   - Plain language first; jargon only after it's explained.
   - Keep code examples under 15 lines.
   - Questions must require reasoning about code, never yes/no (see `references/question-types.md`).
   - Write in English; the agent translates when teaching.
4. Run `node scripts/check.mjs` — it validates the catalog and regenerates `concepts/INDEX.md`. Commit both.

New tracks (e.g. a language like `typescript` or `python`) are welcome: create the folder and add concepts.

## 2. Improve the teaching

`references/` holds the rules every skill follows (teaching method, question types, profile format). Changes here affect every session, so please describe in the PR what behavior changes and, ideally, include a before/after transcript.

## 3. Change skills

Skills live in `skills/<name>/SKILL.md`. Keep them **agent-agnostic**: don't reference tools by a specific agent's name (write "run `git diff`", not "use the Bash tool"). Tacit is meant to run on Claude Code today and on Codex, Gemini CLI and others later.

## Local testing

```bash
node scripts/check.mjs           # validate + regenerate the index
claude plugin validate .         # validate manifests (Claude Code)
claude --plugin-dir .            # run Claude Code with your local copy of the plugin
```

## Commits and releases

We use [Conventional Commits](https://www.conventionalcommits.org): `feat:`, `fix:`, `docs:`, `chore:`… Releases and the changelog are generated automatically by release-please from these messages.

Breaking changes (renaming a skill, changing the profile format) must use `feat!:` or a `BREAKING CHANGE:` footer.

## Code of conduct

Be kind. This project exists to help beginners — treat contributors the same way. See [CODE_OF_CONDUCT.md](CODE_OF_CONDUCT.md).
