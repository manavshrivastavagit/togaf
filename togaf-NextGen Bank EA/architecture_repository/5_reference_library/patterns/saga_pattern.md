# Integration Pattern: Saga Orchestration

## 1. Intent
Manage data consistency across multiple independent microservices in a distributed system without relying on two-phase commit (2PC) database protocols.

---

## 2. The Problem
In a microservices architecture, a single business process often spans multiple services, each with its own database. For example, a loan origination workflow:
1.  Verify Aadhaar Identity (`Onboarding Service`)
2.  Validate Bureau Credit Score (`Risk Service`)
3.  Generate Loan Agreement (`Ledger Service`)
4.  Initiate auto-repayment mandate (`Payment Service`)

If the payment mandate fails, we cannot run a simple SQL database rollback because the Aadhaar verification and credit scoring have already committed to their respective databases.

---

## 3. The Solution
A **Saga** is a sequence of local transactions. Each local transaction updates the database inside a single service.
*   If a step fails, the Saga Orchestrator triggers **compensating transactions** in reverse order to undo the updates made by the preceding local transactions.
*   **Orchestration**: A centralized controller orchestrates the steps and compensation actions.
*   **Choreography**: Services publish events, and other services react, driving the workflow implicitly. For lending, **Orchestration** is preferred for strict compliance tracking.

```
                  ┌─────────────────────┐
                  │   Saga Orchestrator │
                  └──────────┬──────────┘
                             │
            ┌────────────────┼────────────────┐
       1. Do│           2. Do│           3. Do│
            ▼                ▼                ▼
     ┌──────────────┐ ┌──────────────┐ ┌──────────────┐
     │  Onboarding  │ │ Risk Engine  │ │ Payment Hub  │
     └──────┬───────┘ └──────┬───────┘ └──────┬───────┘
            │                │                │
            │1.Compensate    │2.Compensate    │3.FAIL!
            └────────────────┴────────────────┴───────
```

---

## 4. Saga Lifecycle Definition (Example)

| Step | Service | Local Transaction | Compensating Transaction (Rollback) |
| :--- | :--- | :--- | :--- |
| **1** | Onboarding | Create customer profile | Mark profile as `DRAFT_REJECTED` |
| **2** | Risk | Evaluate scorecard & block limit | Release risk block on borrower limit |
| **3** | Ledger | Assemble contract PDF | Delete contract draft & invalidate signature |
| **4** | Payment | Setup UPI mandate | Cancel pending mandate requests |

---

## 5. Key Design Principles

1.  **Idempotence**: All local and compensating transactions must be idempotent. If the orchestrator retries a compensating call (due to network timeout), the target service must handle it without duplicating side-effects.
2.  **State Persistence**: The orchestrator must persist its own execution state (e.g., in Postgres or Temporal state) to resume the workflow in case of server failure.
