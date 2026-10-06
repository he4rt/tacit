---
name: learning-setup
description: Calibrate the Tacit learner profile — a short placement check plus preferences for depth, hands-on exercises and diagrams. Use when the user wants to set up or reset Tacit, change how deep explanations go, or turn exercises on or off.
disable-model-invocation: true
---

# Learning setup

Create or update the learner profile at `~/.tacit/profile.md`. Keep the whole setup under 3 minutes.

Before starting, read (paths relative to this skill's directory):

- `../../references/learner-profile.md` — profile format and status rules
- `../../concepts/INDEX.md` — the concept catalog

## 1. Check for an existing profile

If `~/.tacit/profile.md` exists, show the current preferences in a short table and ask whether they want to **change preferences** only, **recalibrate** their level, or **start over**. Never delete concept history unless they choose to start over and confirm it.

## 2. Background (one message)

Ask, in one message:

- Which languages/stacks they work with (e.g. TypeScript, Python, SQL).
- How they'd describe their experience: just starting / comfortable building small apps / working professionally / experienced with architecture.

## 3. Placement check

Ask **3 to 5 quick questions**, one per message, picking concepts from the catalog based on their answer to step 2:

- Start at the level they claimed. If they answer correctly, go one level up; if wrong, one level down.
- Cover different tracks (data, backend, integrations, quality).
- Use multiple-choice when the platform supports it, to keep this fast.
- Always allow "skip" / "I don't know" — that's useful information, not a failure.

Record results: a correct answer marks the concept `practicing`; mark the easier concepts of the same track that they clearly know as `practicing` too. Don't mark anything `mastered` from the placement check alone.

## 4. Preferences (one message)

Explain and ask for each, with the default in bold:

- **Depth**: `quick` (only essentials) / **`standard`** / `deep` (trade-offs and alternatives)
- **Hands-on**: `off` / **`light`** (rarely, 1–5 lines) / `moderate` (small exercises every few files)
- **Diagrams**: **on** / off

## 5. Save and confirm

Write `~/.tacit/profile.md` following the format in learner-profile.md (create `~/.tacit/` if needed). Then summarize in a few lines: their preferences, where they're starting, and that they can run `walkthrough` after their agent writes code — or anytime on existing code.
