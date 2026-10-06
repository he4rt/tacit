---
id: integrations/idempotency
title: Idempotency
track: integrations
level: intermediate
prerequisites: [backend/request-response, data/transactions]
signals:
  - "Idempotency-Key headers, dedupe tables, unique event ids"
  - "webhook handlers, retries, queue consumers"
  - "upserts (ON CONFLICT DO NOTHING/UPDATE)"
---

## In one sentence

An operation is idempotent when doing it twice has the same effect as doing it once.

## Analogy

An elevator button: pressing it five times doesn't call five elevators.

## Why it matters

Networks fail and systems retry. Webhooks arrive twice, users double-click, queues redeliver. Without idempotency, a retry charges the customer twice or creates duplicate orders.

## In code

```ts
// webhook handler: the provider may deliver the same event more than once
const inserted = await db.insert(processedEvents)
  .values({ eventId: event.id })
  .onConflictDoNothing()
  .returning();
if (inserted.length === 0) return new Response(null, { status: 200 }); // already handled
await handlePayment(event);
```

## Common mistakes

- Assuming the provider sends each webhook exactly once.
- Checking "already processed?" and then inserting in two separate steps — two concurrent deliveries both pass the check. Use a unique constraint.
- Returning an error for duplicates, which makes the provider retry forever.

## Good questions

- **What if**: The payment webhook arrives twice within the same second. Walk through what happens with and without the `processedEvents` table.
- **Explain why**: Why a unique constraint instead of `SELECT` then `INSERT`?
- **Choose**: Which HTTP methods are idempotent by definition: GET, POST, PUT, DELETE?

## Going deeper

Retries with backoff, the outbox pattern, exactly-once vs at-least-once delivery.
