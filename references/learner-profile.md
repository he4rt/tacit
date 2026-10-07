# Learner profile

The profile is **global per person** (the learner is the same across projects), stored as plain markdown so any agent can read and edit it, and so the learner can read it too.

**Location:** `~/.tacit/profile.md`

If the file doesn't exist, skills must still work using the defaults below, and should suggest running `learning-setup` once at the end of the session (not at the start — don't block the learner).

## Format

```markdown
---
version: 1
depth: standard        # quick | standard | deep
handsOn: light         # off | light | moderate
diagrams: true
diagramStyle: text     # text | mermaid
languages: [typescript, sql]
updated: 2026-10-06
---

# Tacit learner profile

## Concepts

| Concept | Status | Correct | Missed | Last seen | Notes |
|---|---|---|---|---|---|
| data/primary-keys | mastered | 3 | 0 | 2026-10-06 | |
| data/transactions | practicing | 1 | 1 | 2026-10-06 | confused rollback with retry |
| integrations/idempotency | skipped | 0 | 0 | 2026-10-06 | |
| ad-hoc:react-suspense | introduced | 0 | 0 | 2026-10-06 | |

## Session log

- 2026-10-06 — walkthrough of `src/todos/*` (5 files): learned transactions, skipped idempotency.
```

## Status values

| Status | Meaning |
|---|---|
| `unseen` | Never encountered (implicit — concepts not in the table are unseen) |
| `introduced` | Explained once, not yet verified |
| `practicing` | At least one correct answer, or mixed results |
| `mastered` | 2+ correct answers across different sessions or questions, and correct > missed |
| `skipped` | Learner chose to skip; resurface in a later session |

## Update rules

- Update the table at the **end** of each walkthrough (and when the learner stops early), in a single write.
- Correct answer: `correct += 1`; promote `unseen/introduced/skipped → practicing`, `practicing → mastered` when the mastered rule holds.
- Wrong answer (after hint): `missed += 1`; `mastered → practicing`; otherwise at least `introduced`.
- Explained without a question (quick depth): `unseen → introduced`.
- Think-first answers (in `learn`, before the code exists): a sound approach counts as correct; an unsound one is not counted as missed.
- Keep the session log to the last 20 entries; one line each.
- Keep notes short — they exist to pick a better angle next time.
- Never delete rows. Never store code, secrets, or project-identifying details beyond file paths.
