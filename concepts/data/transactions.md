---
id: data/transactions
title: Database transactions
track: data
level: intermediate
prerequisites: [data/foreign-keys]
signals:
  - "BEGIN/COMMIT/ROLLBACK, db.transaction(), $transaction, session.begin()"
  - "several writes that must succeed or fail together"
---

## In one sentence

A transaction groups several database operations so they either all happen or none do.

## Analogy

A bank transfer: debiting one account and crediting another must happen together. Money must never disappear halfway.

## Why it matters

Without a transaction, a failure between two writes leaves the data inconsistent (an order without its items, a debit without its credit).

## In code

```ts
await db.transaction(async (tx) => {
  const order = await tx.insert(orders).values({ userId }).returning();
  await tx.insert(orderItems).values(items.map((i) => ({ ...i, orderId: order[0].id })));
}); // any error inside → everything is rolled back
```

## Common mistakes

- Calling external APIs (payments, emails) inside a transaction — they can't be rolled back and keep the transaction open for a long time.
- Using the global `db` instead of `tx` inside the callback, so some writes escape the transaction.
- Wrapping single-statement operations "just in case" — one statement is already atomic.

## Good questions

- **What if**: The second insert fails. What's in the database afterwards — with and without the transaction?
- **Spot the bug**: Show the example using `db.insert` for the second write and ask what's wrong.
- **Choose**: Should sending the confirmation email happen inside or after the transaction?

## Going deeper

Isolation levels, `integrations/idempotency`, the outbox pattern.
