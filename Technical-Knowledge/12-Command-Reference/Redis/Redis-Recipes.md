---
title: Redis Recipes
type: reference
tags: [technical-knowledge, redis, database, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://redis.io/docs/latest/develop/
  - https://redis.io/docs/latest/commands/
---

# Redis Recipes

Redis is a data structure server. Choose data type and expiration/eviction policy from the access pattern; avoid using it as an unbounded cache.

## Set/get value with TTL

```text
SET session:abc <serialized-value> EX 1800
GET session:abc
TTL session:abc
```

Use namespaced keys and expirations for temporary data. Do not store plaintext credentials; protect access with ACL/TLS/network boundaries.

## Cache-aside

1. Read cache key.
2. On miss, load source of truth.
3. Write with TTL.
4. On mutation, invalidate/update relevant key.

Prevent cache stampedes for hot keys with request coalescing/jitter/lock design; cache invalidation must account for related keys and tenant/user scope.

## Increment safely

Use `INCR`/`INCRBY` for atomic integer counters. A read-modify-write sequence in application code can lose updates under concurrency. Set expiration deliberately; a counter without TTL may grow forever.

## Use hashes/lists/sets

- Hash: grouped fields for a record (`HSET user:42 name Ada`).
- Set: unique membership (`SADD online user:42`).
- Sorted set: ordered score/rank (`ZADD leaderboard 10 user:42`).
Choose based on atomic operations needed, data growth, and query patterns.

## Inspect health and persistence

Use `INFO`, `SLOWLOG GET`, and `LATENCY` tools under operator access. Review RDB/AOF durability, replication/failover and backup restore drills; persistence settings are part of data-loss objectives.

## Read next

[[Redis Cache-Aside]] · [[Redis Persistence and Durability Choices]] · [[Database Connection Pooling]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
