---
title: "Why I prefer binlog-based sync over dual writes"
description: "Keeping MySQL and Elasticsearch consistent without making every write path care about search."
date: 2026-11-26 10:00:00 -0800
tags: [Data Sync, Search]
---

## The problem

A search index has to follow the source database. Dual writes from the application look simple, but a partial failure leaves the two stores silently out of sync.

## Principles I lean on

- The database's change log is the source of truth; the index is a projection of it.
- Preserve order per primary key, and handle deletes as first-class events.
- Plan for full reindexing and backfills from day one.

## Trade-offs

| Decision | Option A | Option B |
|---|---|---|
| Sync method | Dual write: simple, can drift | Binlog CDC: consistent, more infrastructure |
| Permissions | Filter at index time: fast queries | Filter at query time: always current |
