# 🐰 RabbitMQ Queues & Exchanges

## Exchanges
- `orders.exchange` (type: direct)
- `events.exchange` (type: topic)

## Queues
- `orders.cmd.create.q` (bind: `orders.exchange` → routing `order.create`)
- `orders.cmd.cancel.q` (bind: `orders.exchange` → routing `order.cancel`)
- `events.order.created.q` (bind: `events.exchange` routing `order.created.*`)

## Policies (Quorum + DLX)
- Quorum: `ha-mode=all`, `quorum.initial-group-size=3`
- DLX: `*.q` → DLX `dead.exchange` với TTL 60000 ms
