---
title: RabbitMQ Recipes
type: reference
tags: [technical-knowledge, rabbitmq, messaging, recipes]
status: researched
last_verified: 2026-11-20
sources:
  - https://www.rabbitmq.com/tutorials
  - https://www.rabbitmq.com/docs/confirms
---

# RabbitMQ Recipes

Use a maintained client library for the language/runtime. Examples show AMQP concepts; client method names differ.

## Declare durable queue and publish persistent message

```js
await channel.assertQueue('jobs', { durable: true })
channel.sendToQueue('jobs', Buffer.from(JSON.stringify(job)), {
  persistent: true,
  contentType: 'application/json',
  messageId: job.id,
})
```

Durable queue + persistent message supports broker restart recovery, but publisher confirms are needed to know broker accepted publish. Make consumers idempotent because delivery may repeat.

## Consume with manual acknowledgement

```js
await channel.prefetch(10)
channel.consume('jobs', async msg => {
  if (!msg) return
  try {
    await processJob(JSON.parse(msg.content.toString()))
    channel.ack(msg)
  } catch (error) {
    channel.nack(msg, false, shouldRetry(error))
  }
}, { noAck: false })
```

Ack only after durable work succeeds. `nack(requeue=true)` can create hot infinite loops; use bounded retry with delay/dead-letter policy and terminal dead-letter queue.

## Publisher confirms and handling channel close

Use confirm channel and await confirm for critical messages. Handle connection/channel error and close; reconnect with backoff and recreate topology. Do not assume a successful socket write means the broker durably accepted the message.

## Retry and dead-letter

Configure dead-letter exchange/queue and bounded retry strategy; preserve original message ID and attempt count. Separate transient failures (retry) from permanent invalid payload (dead-letter/alert).

## Ordering and throughput

Multiple consumers increase throughput but weaken global ordering. Set prefetch to bound in-flight work and memory. Use partition/routing strategy when per-entity order is required.

## Read next

[[RabbitMQ Acknowledgements and Redelivery]] · [[Docker Compose Recipes]] · [[HTTP Semantics and REST]]

## Reference Catalog

[[Technical-Knowledge/13-References/Reference-Catalog|Browse all references by topic]]
