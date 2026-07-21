# Integration Pattern: Transactional Outbox

## 1. Intent
Ensure reliable event publishing by separating the database write operation from the event dispatching process. This guarantees that an event is published to the message broker if and only if the local database transaction completes successfully.

---

## 2. The Problem (Dual-Write Failure)
In microservice architectures, a service often needs to update its local database AND publish an event to a message broker (e.g., Kafka). For example, the `Lending Ledger` updates a loan balance and publishes a `RepaymentProcessed` event.
If the database write succeeds but the message broker is down, the event is lost. If the broker write succeeds first but the database rollback occurs, the broker has invalid state. This is known as the **Dual-Write Problem**.

---

## 3. The Solution
Instead of publishing directly to the broker inside the business logic, the service writes the event payload into a dedicated `outbox` table within the *same* database transaction as the business write. A separate process (Outbox Publisher) polls the outbox table or reads the transaction log (Change Data Capture / CDC) to publish the events asynchronously to the broker.

```
┌────────────────────────────────────────────────────────┐
│                   MICROSERVICE DOMAIN                  │
│                                                        │
│  ┌─────────────────┐       1. Write inside             │
│  │  Business Logic │ ────  Transactional Boundary      │
│  └────────┬────────┘      │                            │
│           │               ▼                            │
│           │        ┌──────────────┐   ┌──────────────┐ │
│           │        │ Business Tab │   │ Outbox Table │ │
│           │        └──────────────┘   └──────┬───────┘ │
│           │                                  │         │
│           └──────────────────────┐           │ 2. Read │
│                                  ▼           ▼         │
│                            ┌─────────────────────┐     │
│                            │   Outbox Publisher  │     │
│                            └──────────┬──────────┘     │
└───────────────────────────────────────┼────────────────┘
                                        │ 3. Publish
                                        ▼
                                ┌──────────────┐
                                │ Message Bus  │
                                └──────────────┘
```

---

## 4. Database Schema Example (PostgreSQL)

```sql
CREATE TABLE outbox_events (
    event_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    aggregate_type VARCHAR(255) NOT NULL,
    aggregate_id VARCHAR(255) NOT NULL,
    event_type VARCHAR(255) NOT NULL,
    payload JSONB NOT NULL,
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP,
    status VARCHAR(50) DEFAULT 'PENDING',
    processed_at TIMESTAMP WITH TIME ZONE
);

CREATE INDEX idx_outbox_pending ON outbox_events(created_at) WHERE status = 'PENDING';
```

---

## 5. Publisher Implementation Strategies

1.  **Transaction Log Tailer (Debezium / CDC)**: Best performance. Tools like Debezium monitor the PostgreSQL Write-Ahead Log (WAL) and stream changes to Kafka automatically. Zero query overhead on the database.
2.  **Polling Publisher**: A simple background scheduler queries the outbox table (`SELECT ... WHERE status = 'PENDING' ORDER BY created_at LIMIT 100 FOR UPDATE SKIP LOCKED`), publishes to Kafka, and updates the status to `PROCESSED`.
