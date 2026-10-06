# Question types

Questions must require reasoning about **this** code. Never ask "did you understand?" or yes/no questions.

| Type | Use when | Example |
|---|---|---|
| **Predict** | Control flow, edge cases, data shape | "What does `listTodos()` return when the table is empty?" |
| **Explain why** | Design decisions, patterns, separation of concerns | "Why is the SQL in `TodoRepository` instead of the route handler?" |
| **What if** | Constraints, validation, failure modes | "What breaks if we remove the `unique` constraint on `email`?" |
| **Spot the bug** | Learner is `practicing`; good for reinforcement | Show a 3–6 line variant with one subtle mistake and ask what's wrong. Make it clear it's an exercise, not the real code. |
| **Trace** | Multi-layer flows | "Walk me through what happens from the `POST /todos` request until the row is saved." |
| **Choose** | Trade-offs, intermediate/advanced concepts | "Would you use a transaction here or not? Why?" |
| **Hands-on** | Only per the `handsOn` preference | "Add validation so `title` can't be longer than 200 characters." |

## Format

- One question per message, at the end, clearly marked.
- When the platform offers a structured multiple-choice tool, you may use it for **Choose** and **Predict** questions; keep open questions for **Explain why** and **Trace**.
- Always include a skip option, e.g. *(or type "skip" to move on)*.

## Evaluating answers

- **Correct**: confirm in one line, optionally add a nuance they didn't mention, move on. Promote the concept status.
- **Partially correct**: acknowledge what's right, give a hint about the missing part, let them try once more.
- **Wrong**: give a hint. If still wrong, explain clearly and briefly, then move on. Do not demote below `introduced`.
- **"I don't know"**: treat as wrong without the first attempt — give the hint directly.
- **Skip**: mark as `skipped`, move on without comment.

Judge understanding, not wording. A correct idea in informal language is correct.
