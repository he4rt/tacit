---
id: backend/input-validation
title: Input validation at the boundary
track: backend
level: basic
prerequisites: [backend/request-response]
signals:
  - "schema libraries: zod, yup, joi, pydantic, class-validator"
  - "parse/safeParse/validate calls in handlers"
---

## In one sentence

Every piece of data coming from outside the system (requests, webhooks, files) is checked for shape and rules before the rest of the code trusts it.

## Analogy

The airport security check: once you're past it, nobody re-checks your bag at every gate.

## Why it matters

Without it, bad data reaches the database, crashes code deep in the system with confusing errors, or opens security holes. Validating once at the edge keeps the inner code simple.

## In code

```ts
const CreateTodo = z.object({ title: z.string().min(1).max(200) });

const parsed = CreateTodo.safeParse(await req.json());
if (!parsed.success) return Response.json(parsed.error.flatten(), { status: 400 });
await createTodo(parsed.data.title); // typed and trusted from here on
```

## Common mistakes

- Validating only in the front-end — anyone can call the API directly.
- Trusting TypeScript types for external data — types disappear at runtime.
- Validating the same thing in every layer instead of once at the boundary.

## Good questions

- **Explain why**: The form already requires a title. Why validate again on the server?
- **What if**: What happens if someone sends `{ "title": 42 }` and we remove the schema?
- **Hands-on**: Make the title also reject strings with only spaces.

## Going deeper

`backend/layered-architecture`, parse-don't-validate.
