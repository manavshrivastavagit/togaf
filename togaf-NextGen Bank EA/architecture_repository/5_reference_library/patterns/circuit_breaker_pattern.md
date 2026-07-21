# Integration Pattern: Resilience Circuit Breaker

## 1. Intent
Prevent a failure in one service or third-party API provider from cascading throughout the entire system. A circuit breaker isolates the dependency, failing fast and allowing the caller to execute fallback logic immediately without wasting resources.

---

## 2. The Problem
Lending microservices rely heavily on third-party APIs (e.g., Aadhaar OTP, CIBIL bureau, UPI mandate systems).
If a partner API experiences high latency or downtime:
1.  Our incoming HTTP threads block, waiting for responses.
2.  Container thread pools exhaust rapidly.
3.  The entire platform becomes unresponsive to other customers, leading to a system-wide crash.

---

## 3. The Solution
Wrap all outbound partner API calls in a Circuit Breaker state machine:

```
          ┌─────────────────────────────────────────┐
          │                                         │ Success < Threshold
          │                  ┌──────────────┐       │
          └─────────────────>│    CLOSED    │<──────┘
                             │  (Normal Op) │
                             └──────┬───────┘
                                    │
                                    │ Failures > Threshold
                                    ▼
                             ┌──────────────┐
          ┌─────────────────>│     OPEN     │
          │                  │ (Fail-Fast)  │
          │                  └──────┬───────┘
          │                         │
          │ Success fails           │ Trip Time Expires
          │                         ▼
          │                  ┌──────────────┐
          └──────────────────│  HALF-OPEN   │
                             │ (Test Probes)│
                             └──────────────┘
```

*   **CLOSED**: Normal operations. Traffic flows to the target API.
*   **OPEN**: Failure threshold exceeded (e.g., 50% failures in rolling window). All calls fail immediately (fail-fast), returning cached data or running fallbacks.
*   **HALF-OPEN**: Trip duration expires. The breaker allows a limited number of test calls to check if the partner API has recovered. If yes, it closes; if no, it re-opens.

---

## 4. Parameter Configurations (Resilience4j / Istio Envoy)

| Parameter | Recommended Value | Rationale |
| :--- | :--- | :--- |
| **Failure Rate Threshold** | 50% | Trip the breaker if half of the rolling requests fail. |
| **Slow Call Rate Threshold**| 75% | Trip the breaker if responses exceed the SLA (e.g., > 2s). |
| **Slow Call Duration** | 2000 ms | Any partner API call taking longer than 2s is treated as slow. |
| **Wait Duration in Open State**| 60 seconds | Keep the breaker open for 60s before probe checking. |
| **Minimum Number of Calls** | 10 | Evaluate metrics only after at least 10 calls have executed. |

---

## 5. Fallback Implementation Strategies

When the circuit breaker is **OPEN**, the service should execute one of these fallbacks:
-   *Bureau scoring down*: Query cached CIBIL score if pulled within last 30 days, or route to Experian.
-   *Liveness check API down*: Display a "verification delayed" screen to the user, schedule an automated retry webhook, and notify the user via SMS once resolved.
-   *UPI Mandate registration down*: Fallback to e-NACH/NetBanking registration immediately.
