---
id: data/foreign-keys
title: Foreign keys and relationships
track: data
level: basic
prerequisites: [data/primary-keys]
signals:
  - "REFERENCES, FOREIGN KEY, ON DELETE in migrations"
  - "ORM relations: belongsTo, hasMany, references(), relations()"
  - "columns named {entity}_id / {entity}Id"
---

## In one sentence

A foreign key is a column that stores the primary key of a row in another table, linking the two — and the database guarantees that link is valid.

## Analogy

An order slip with a customer number on it: the number only makes sense if that customer exists in the customer book.

## Why it matters

It models relationships (one user has many todos) and protects integrity: you can't create a todo for a user that doesn't exist, and you decide what happens to the todos when the user is deleted.

## In code

```sql
CREATE TABLE todos (
  id      UUID PRIMARY KEY,
  user_id UUID NOT NULL REFERENCES users(id) ON DELETE CASCADE,
  title   TEXT NOT NULL
);
```

`ON DELETE CASCADE` deletes the user's todos together with the user. Alternatives: `RESTRICT` (block the deletion) or `SET NULL`.

## Common mistakes

- Storing the relationship as a plain column without the constraint — orphaned rows appear silently.
- Choosing `CASCADE` by default where losing data is dangerous (e.g. invoices).
- Forgetting an index on the foreign key column, making joins and deletes slow.

## Good questions

- **What if**: What happens to a user's todos when the user is deleted, given this schema?
- **Choose**: Should deleting a customer cascade to their invoices? Why or why not?
- **Predict**: What error do we get if we insert a todo with a `user_id` that doesn't exist?

## Going deeper

One-to-many vs many-to-many (join tables), `data/transactions`.
