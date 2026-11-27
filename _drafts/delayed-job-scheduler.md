---
title: "Designing a delayed-job scheduler: time wheel vs. Redis sorted sets"
description: "Two good answers with different failure modes. Which one fits depends on scale and how much state you can afford to lose."
tags: [System Design, Scheduling]
---

## The problem

Run millions of jobs at a future time (reminders, retries, expirations) with low latency and no lost jobs when a node dies.

## Options

| | Redis ZSET (score = run time) | Hierarchical time wheel |
|---|---|---|
| Insert / fire | O(log n), poll by score | O(1) per tick, in memory |
| Durability | Comes with Redis persistence | Needs its own WAL or snapshot |
| Scaling | Shard keys to avoid one hot ZSET | Shard ownership via a coordinator such as ZooKeeper |

## Principles I lean on

- Deliver at least once and make jobs idempotent; don't chase exactly-once.
- Separate "when to fire" from "doing the work" so a slow job can't stall the clock.
