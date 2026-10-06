---
id: backend/request-response
title: HTTP request and response
track: backend
level: basic
prerequisites: []
signals:
  - "route handlers: app.get/post, router.*, export async function GET/POST"
  - "status codes, req.body, res.json, Response objects"
---

## In one sentence

A client sends an HTTP request (method, path, headers, body) and the server answers with a response (status code, headers, body).

## Analogy

Ordering at a counter: you say what you want (method + path), give details (body), and get back your order or an explanation of why not (status code).

## Why it matters

It's the contract between front-end and back-end. Methods and status codes tell the client what happened without reading the body.

## In code

```ts
// POST /todos
export async function POST(req: Request) {
  const { title } = await req.json();
  if (!title) return Response.json({ error: "title is required" }, { status: 400 });
  const todo = await createTodo(title);
  return Response.json(todo, { status: 201 });
}
```

Common status codes: `200` ok, `201` created, `400` bad input, `401` not authenticated, `403` not allowed, `404` not found, `500` server error.

## Common mistakes

- Returning `200` with `{ error: ... }` — clients and monitoring think everything worked.
- Using `GET` for actions that change data.

## Good questions

- **Predict**: What status code does the client get if `title` is missing?
- **Explain why**: Why `201` instead of `200` here?
- **Trace**: What happens from clicking "Add" in the UI until the todo appears in the list?

## Going deeper

`backend/input-validation`, `backend/layered-architecture`.
