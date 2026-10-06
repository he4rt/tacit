---
name: learning-progress
description: Show the learner's Tacit progress — concepts mastered, in practice, skipped or missed, by track — and suggest what to learn next. Use when the user asks what they've learned, how they're doing, or what to study next.
---

# Learning progress

Read `~/.tacit/profile.md` and `../../concepts/INDEX.md` (relative to this skill's directory). The profile format is described in `../../references/learner-profile.md`.

If the profile doesn't exist, say so in one line and suggest `learning-setup` or a `walkthrough` on code they're working on.

## Show

1. **Summary line**: e.g. "12 concepts seen — 5 mastered, 4 practicing, 3 to revisit."
2. **By track** (data, backend, integrations, quality, then any language or ad-hoc concepts): a compact table or list with each concept's status. Use the concept titles from the catalog, not the ids.
3. **To revisit**: skipped concepts and concepts with more misses than correct answers, with the note from the profile if there is one.
4. **Next steps**: 2–3 suggestions:
   - concepts whose prerequisites they've mastered but haven't seen yet (from the catalog's `prerequisites`);
   - a concrete idea for practicing them — e.g. "next time your agent adds an external API call, run a walkthrough and pay attention to retries".
5. The recent session log (last 5 entries).

Keep it scannable. Don't quiz the learner here unless they ask to practice — in that case, pick a concept from "to revisit" and ask one question following `../../references/question-types.md`, then update the profile.
