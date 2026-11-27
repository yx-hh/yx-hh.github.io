---
title: "Idempotency belongs to the whole payout path, not one endpoint"
description: "A retry can come from the user, the client, a worker, or a batch job. Every layer needs an answer."
date: 2026-11-26 12:00:00 -0800
tags: [Payments, Reliability]
---

## The problem

A cashback payout can be retried in many places: a double click, a client timeout, a worker restarting mid-job, or a batch file regenerated after a failure. An idempotency key on the API alone doesn't stop money from moving twice.

## Principles I lean on

- One key per business intent (the redemption request), carried through every hop.
- An explicit state machine with legal transitions only, e.g. `PENDING → BATCHED → SENT → SETTLED / RETURNED`.
- Let the database enforce uniqueness instead of trusting application checks.
- Build bank files from state, not from a queue of requests, so regenerating a file is safe.

## Trade-offs

| Option | Gain | Cost |
|---|---|---|
| DB unique constraint | Simple, survives crashes | Needs careful key design |
| Distributed lock | Flexible across services | Lock expiry and failover edge cases |

## What I'd revisit

Exactly-once is a promise you can't keep across a bank boundary. Design for at-least-once plus deduplication, and treat daily reconciliation as the real safety net.
