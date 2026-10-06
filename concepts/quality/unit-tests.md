---
id: quality/unit-tests
title: Unit tests
track: quality
level: basic
prerequisites: []
signals:
  - "*.test.*, *.spec.*, test_*.py files"
  - "describe/it/test/expect, assert, pytest"
---

## In one sentence

A unit test runs a small piece of code (a function, a class) in isolation and checks that it produces the expected result.

## Analogy

Testing each Lego brick before building the castle: if a brick is broken, you find it immediately, not when the tower falls.

## Why it matters

Tests catch regressions when code changes, document how code is meant to behave, and let you (or your agent) refactor with confidence. They're also the fastest way to check AI-written code does what you asked.

## In code

```ts
test("rejects empty titles", () => {
  expect(() => createTodoTitle("")).toThrow("title is required");
});

test("trims whitespace", () => {
  expect(createTodoTitle("  buy milk ")).toBe("buy milk");
});
```

Structure: **arrange** (set up input), **act** (call the code), **assert** (check the result).

## Common mistakes

- Testing implementation details instead of behavior — tests break on every refactor.
- Only testing the happy path; bugs live in edge cases.
- Tests that always pass (e.g. missing `await`, assertions that never run).

## Good questions

- **Predict**: Which of these tests fails if we remove the `.trim()` call?
- **What if**: What edge case is missing from these tests?
- **Hands-on**: Write a test for a title with 201 characters.

## Going deeper

Integration tests, mocks and fakes, test-driven development.
