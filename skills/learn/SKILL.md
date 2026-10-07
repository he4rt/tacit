---
name: learn
description: Build a feature in small slices while learning. Before each slice, the learner thinks through the approach for concepts they're ready to reason about; after it, a short walkthrough compares their idea with what was built. Use only when the user explicitly asks to build something with Tacit's learning mode.
argument-hint: "<task>"
disable-model-invocation: true
---

# Learn

Build what the learner asked for, in small slices, so they **think before** the code where they can and **understand after** the code always. This is a conversation across many turns.

Before starting, read these files (paths relative to this skill's directory):

- `../../references/teaching-method.md` — how to teach, depth levels, diagrams, hands-on
- `../../references/question-types.md` — how to ask and evaluate questions
- `../../references/learner-profile.md` — where the profile lives and how to update it
- `../../concepts/INDEX.md` — the concept catalog
- `../walkthrough/SKILL.md` — the per-file walkthrough this skill reuses after each slice

## Why think first only sometimes

Reasoning about a problem before seeing the answer helps learning — but only when the learner has enough to reason with. Someone who has never seen a transaction can't propose one; asking just produces a guess. So the profile status of each concept decides whether the learner thinks first or studies the result:

| Profile status | Before the slice | After the slice |
|---|---|---|
| `unseen` | One-line heads-up: "this step uses X — I'll explain it once it's built" | Full explanation in the walkthrough |
| `introduced` / `skipped` | **Choose** question: 2–3 options, one sound | Walkthrough compares their pick with the code |
| `practicing` | Open **"how would you…"** question | Walkthrough compares their approach with the code |
| `mastered` | Nothing | One line |

At most **one** think-first question per slice — pick the concept closest to `practicing`. Never more questions before the code than after it.

## 1. Load the learner profile

Read `~/.tacit/profile.md`. If it doesn't exist, use the defaults (`depth: standard`, `handsOn: light`, `diagrams: true`, `diagramStyle: text`, every concept `unseen`) and continue — don't ask for setup now.

## 2. Understand the task

The task is in `$ARGUMENTS`. If it's empty, ask what they want to build in one line.

Inspect the parts of the codebase the task touches (read only). If the request is ambiguous in a way that changes the design, ask **one** clarifying question; otherwise make a reasonable choice and say so.

## 3. Plan the slices (first message)

Split the task into **slices**: each one a small, working step with one cohesive behavior, usually 1–5 files. Order them so each builds on the previous one (schema → logic → API → UI → tests alongside).

In the first message:

1. One or two sentences on what you're going to build, in plain language.
2. The slices as a numbered list, one line each.
3. If `diagrams` is on and the task crosses several layers, one diagram of the target flow.
4. How it works: before some steps you'll ask how they'd approach it, after each step a short walkthrough, and they can say "skip", "just build it" or "stop" anytime.

Then go straight to the first slice.

## 4. For each slice

### a. Think first

Identify the concepts the slice will use (match them to the catalog; read the concept file for any you'll ask about). Apply the table above.

When asking, give just enough context to reason: what this slice needs to do and the constraint that matters. Don't hint at the answer. End with the question and the skip option, then **stop and wait**.

### b. Respond to their approach

Their answer is a prediction, not an exam:

- **Sound approach**: say so in one line. If it differs from what you'd have done but is valid, **build it their way** and mention the trade-off. It's their code.
- **Approach with a real problem**: ask one **What if** question that exposes it ("what happens if two requests do this at the same time?"). If they adjust, build that. If not, explain briefly and build the sound version.
- **"I don't know" / skip**: no comment, move on.

### c. Build the slice

Implement only this slice. Follow the project's conventions. Run the existing tests or checks if the project has them, and fix what you broke.

### d. Walk through the slice

Run the walkthrough from `../walkthrough/SKILL.md` (steps 4 and 5) on the files of this slice, with two differences:

- **Open by comparing**: "You suggested X — here's where that shows up" or "You picked A; we went with B because…". Keep it to two or three lines.
- **Don't re-ask** about the concept they already reasoned about in step a, unless their answer showed a misunderstanding.

Files whose concepts are all `mastered` get one line each, not a full stop.

### e. Next

Ask whether to continue to the next slice. If they want to change the plan, update the remaining slices and show them again.

## 5. Escape hatches

- **"just build it"**: build the remaining slices without think-first questions, then offer one walkthrough of everything that was built.
- **"skip"** on a question: mark the concept as skipped, move on.
- **"stop"**: stop after the current slice is in a working state, then close the loop. Never leave the code half-built.

## 6. Close the loop

After the last slice (or when the learner stops), follow step 6 of `../walkthrough/SKILL.md`: recap, optional final diagram, one profile update, one concept to revisit. Add a session log line like `learn: <task> (N slices)`.

For think-first answers, a sound approach counts as **correct**; an unsound one is **not** counted as missed — they hadn't been taught yet. Outcomes from the walkthrough questions count as usual.
