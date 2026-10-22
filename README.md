# Tacit

**Learn while you delegate.**

AI agents now write most of the code. That's great for speed — and terrible for learning. If you're starting out, it's easy to ship a working app without understanding its data model, its architecture, or why any of it is built that way.

Tacit is a plugin for AI coding agents that turns "here's your code" into "here's your code — let's make sure you get it". After your agent builds something, Tacit walks you through it **file by file**: what each piece does, the concepts behind it, how everything connects (with diagrams), and short questions to check you actually understood. You can always skip.

It adapts to you **per concept**: things you've mastered get one line, new things get explained. The more you learn, the less it interrupts.

## When to use it

Tacit teaches from code that **already exists** — you don't have to change how you work with your agent. Keep delegating, then run a walkthrough when you want to understand what's there:

- **Code your agent just wrote** — the uncommitted changes from your last session.
- **A teammate's work** — a commit or a branch before you review or build on it.
- **A project you just joined** — any folder or set of files, as they are today.

Every walkthrough builds on what you already know, so the same concept never gets explained to you twice at the same depth.

## Install

### Claude Code

```
/plugin marketplace add he4rt/tacit
/plugin install tacit@tacit
```

Support for Codex, Gemini CLI and others is on the roadmap. Tacit's core is written as portable [Agent Skills](https://agentskills.io).

### Updates

Auto-update is **off by default** for third-party marketplaces. To turn it on, open `/plugin` → **Marketplaces** → **tacit** → **Enable auto-update**.

To update manually, run in your terminal:

```sh
claude plugin marketplace update tacit
claude plugin update tacit@tacit
```

Restart Claude Code to load the new version. Updates never touch your profile in `~/.tacit/`.

## Usage

| Skill | What it does |
|---|---|
| `/walkthrough [commit \| branch \| paths]` | Guided walkthrough of your uncommitted changes (default), a commit, a branch, or specific files. |
| `/learn <task>` *(experimental)* | Build a feature in small slices: think through the approach first where you're ready, then a short walkthrough of each slice. |
| `/learning-setup` | Short placement check + preferences (depth, hands-on exercises, diagrams). Optional — Tacit works without it. |
| `/learning-progress` | What you've mastered, what to revisit, and what to learn next. |

If another plugin uses the same command name, use the namespaced form, e.g. `/tacit:walkthrough`.

A typical flow:

1. Ask your agent to build something ("add a to-do list with a database").
2. Run `/walkthrough`.
3. Answer a few questions (or skip), and come out understanding what was built.

### Preferences

| Setting | Values | Default |
|---|---|---|
| `depth` | `quick` · `standard` · `deep` | `standard` |
| `handsOn` | `off` · `light` (rarely, 1–5 lines) · `moderate` | `light` |
| `diagrams` | `true` · `false` | `true` |
| `diagramStyle` | `text` (works in any terminal) · `mermaid` (for viewers that render it) | `text` |

Your profile lives in `~/.tacit/profile.md` — plain markdown you can read and edit. It never leaves your machine through Tacit.

## How it works

```
skills/        the agent-facing workflows (walkthrough, setup, progress)
references/    shared teaching rules: method, question types, profile format
concepts/      the concept catalog — one markdown file per concept
```

The **concept catalog** is the heart of Tacit: each concept has a plain-language explanation, an analogy, common mistakes, and good questions to ask. Tracks go from the basics (primary keys, HTTP) to advanced architecture (CQRS, event sourcing, sagas).

## How Tacit teaches

Tacit adapts **per concept, not per person** — you can know REST inside out and never have seen a database transaction. Every concept in your profile has a status, and that status decides how much Tacit says:

| Status | What Tacit does |
|---|---|
| `unseen` | Analogy first, then the code, an optional diagram, and one question |
| `introduced` / `skipped` | Re-explains from a different angle, then one question |
| `practicing` | Short reminder and one question |
| `mastered` | One line ("this uses a repository, which you already know") — no question |

A concept becomes `mastered` after 2+ correct answers across different sessions or questions, with more correct answers than misses. So the more you learn, the less Tacit interrupts.

A few rules every session follows:

- **Questions require reasoning about *this* code** — predict, explain why, what if, spot the bug, trace, choose. Never "did you understand?".
- **Hint before answer.** A wrong answer gets a hint; a second miss gets a short explanation, and the walkthrough moves on. It's not an exam.
- **Skipping is always allowed.** Skipped concepts come back in a later session, never nagged in the same one.
- **Small steps.** One file per message, short enough to read in under a minute, and Tacit waits for you before moving on.
- **Your language.** Tacit replies in the language you write in, keeping code identifiers as they are.
- **Hands off your code.** Tacit doesn't change the code it's teaching unless you ask, or as an exercise you accepted.

The rules live in [`references/`](references/) — read them if you want to know exactly how Tacit behaves, or propose a change.

## Roadmap

- [x] v0.1 — `walkthrough`, `learning-setup`, `learning-progress`, initial catalog
- [ ] Catalog with 20–30 basic and intermediate concepts
- [ ] `/learn <task>` — build features in small slices. Before each slice, think through the approach for concepts you're ready to reason about; after it, a walkthrough compares your idea with what was built (draft in [`skills/learn`](skills/learn/SKILL.md))
- [ ] Advanced tracks: CQRS, event sourcing, sagas, outbox
- [ ] Codex, Gemini CLI and Cursor support
- [ ] Optional hook to require finishing the walkthrough before moving on

## Contributing

The easiest way to contribute is to **add a concept** — no need to understand the rest of the plugin. See [CONTRIBUTING.md](CONTRIBUTING.md).

## License

[MIT](LICENSE)
