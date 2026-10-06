---
name: walkthrough
description: Guided, file-by-file walkthrough of code (usually code an AI agent just wrote) that teaches the concepts behind it, shows how the pieces connect with diagrams, and checks understanding with questions. Use when the user asks to walk through, review together, explain, or learn from recent changes, a commit, a branch, or specific files.
argument-hint: "[commit | branch | paths...]"
---

# Walkthrough

Walk the learner through code one file at a time so they understand what was built and why. This is a conversation across several turns, not a single report.

Before starting, read these files (paths relative to this skill's directory):

- `../../references/teaching-method.md` — how to teach, depth levels, diagrams, hands-on
- `../../references/question-types.md` — how to ask and evaluate questions
- `../../references/learner-profile.md` — where the profile lives and how to update it
- `../../concepts/INDEX.md` — the concept catalog

## 1. Load the learner profile

Read `~/.tacit/profile.md`. If it doesn't exist, use the defaults (`depth: standard`, `handsOn: light`, `diagrams: true`, every concept `unseen`) and continue — don't ask for setup now.

## 2. Resolve the scope

From the arguments (`$ARGUMENTS`):

| Input | Scope |
|---|---|
| nothing | uncommitted changes: `git diff HEAD` plus untracked files (`git status --porcelain`). If there are none, the last commit (`git show HEAD`). |
| a commit SHA or range | that commit / range |
| a branch name | `git diff <default-branch>...<branch>` |
| file or directory paths | those files, as they are now |

Ignore lockfiles, generated files, build output, binary assets and pure formatting changes. If the scope has more than ~12 meaningful files, propose splitting it into parts and start with the first part.

## 3. Show the map (first message)

In the first message:

1. One or two sentences on **what was built**, in plain language.
2. A diagram of how the files connect (if `diagrams` is on) — usually a `flowchart` from entry point to storage.
3. The **reading order**: list the files in dependency order, from foundations to the edges (schema/models → domain/services → API/handlers → UI → tests). Tests can be visited right after the code they cover.
4. Tell them how it works: one file at a time, short questions, and they can say "skip" anytime.

Then go straight to the first file in the same message.

## 4. One file per message

For each file:

1. **Purpose** — what this file is responsible for, in one or two sentences.
2. **Key code** — point to the important parts with short excerpts (≤15 lines) and line references. Don't paste whole files.
3. **Concepts** — identify the concepts the file uses. Match them to the catalog (`../../concepts/INDEX.md`) and read the concept file for any concept you're going to teach. Treat each one according to its profile status (see teaching-method.md). Language-specific idioms count as concepts too.
4. **Connection** — how this file relates to the previous ones and what uses it next. A sequence diagram helps when a request crosses several layers.
5. **Question** — when a concept is new or shaky, end with **one** question (see question-types.md), plus the skip option. Otherwise, end by asking if they want to continue.

Then **stop and wait for the learner's reply.** Never answer your own question, and never cover the next file in the same message.

## 5. Handle the reply

- Evaluate the answer as described in question-types.md (hint before explanation).
- If the learner asks something, answer it — curiosity beats the plan. Then return to the walkthrough.
- If they say "skip", mark the concept as skipped and move on.
- If they say "skip file" or "stop", respect it immediately.
- Track, in your working memory, each concept touched and the outcome — you'll write them all at the end.

## 6. Close the loop

After the last file (or when the learner stops):

1. **Recap** in 3–5 bullets: what the system does now and the concepts they learned.
2. If useful, a final diagram of the whole flow.
3. **Update the profile** at `~/.tacit/profile.md` following the update rules (create the file and the `~/.tacit/` directory with defaults if missing). One write.
4. Mention one concept worth revisiting next time (a skipped or missed one), if any.
5. If the profile didn't exist before this session, suggest running `learning-setup` to calibrate their level.
