# Application Architecture: Third-Party Partner Integration & SLA Matrix

This document defines the integration parameters, service level agreements (SLAs), and automated fallback configurations for all external partner integrations connected to the **Micro-Loan Platform**.

---

## 1. Partner Integration Specifications

The platform orchestrates six external integration points:

| Integration Point | Partner Provider | Protocol | Expected SLA (Response) | Target Availability |
| :--- | :--- | :--- | :--- | :--- |
| **Aadhaar e-KYC** | UIDAI / DigiLocker | HTTPS REST | < 800 ms | 99.9% |
| **PAN Verification** | NSDL / CDSL | HTTPS SOAP | < 500 ms | 99.5% |
| **Bank Statements** | Account Aggregators (Setu) | HTTPS REST | < 1200 ms | 99.9% |
| **Credit Scoring** | CIBIL / Experian | SOAP / HTTPS | < 1500 ms | 99.0% |
| **UPI Auto-Pay** | NPCI Sponsor Bank | REST / SFTP | < 1000 ms | 99.9% |
| **e-Sign Registry** | NeSL Registrar | HTTPS REST | < 1500 ms | 99.5% |

---

## 2. Automated Fallback & Failover Logic

To satisfy the **STP-First** principle, partner API outages must not block the loan application funnel. The following failover rules are configured in the integration client:

```
                  ┌───────────────────────────────┐
                  │ Outbound Bureau scoring Query │
                  └───────────────┬───────────────┘
                                  │
                          ┌───────▼───────┐
                          │ Query CIBIL   │
                          └───────┬───────┘
                                  │
                 ┌────────────────┴────────────────┐
            Success (SLA < 1.5s)           Timeout / Outage (503)
                 │                                 │
                 ▼                                 ▼
         [ Score Returned ]              ┌──────────────────┐
                                         │  Query Experian  │
                                         └─────────┬────────┘
                                                   │
                                     ┌─────────────┴─────────────┐
                                  Success                     Timeout
                                     │                           │
                                     ▼                           ▼
                             [ Score Returned ]        [ Route to Asynchronous ]
                                                       [ Email Alert Webhook   ]
```

### 2.1 Identity Verification Fallback
*   **Primary Path**: Aadhaar OTP validation direct with UIDAI.
*   **Secondary Path (Fallback)**: If UIDAI experiences timeout, the app redirects the customer to fetch their signed Aadhaar XML via **DigiLocker Ingress**, preventing a complete acquisition block.

### 2.2 Payment Mandate Fallback
*   **Primary Path**: UPI Auto-Pay mandate registration via NPCI.
*   **Secondary Path (Fallback)**: If UPI networks fail, the Payment Hub redirects the user to configure a netbanking-based **e-NACH Mandate**, preserving the auto-repayment enrollment.

---

## 3. Client Retry & Timeout Configurations (Envoy / Istio)

All outbound HTTP calls are wrapped with these mesh configurations:
*   **Max Retries**: 2 attempts (applicable only to idempotent `GET` and `PUT` methods; `POST` creations are not retried).
*   **Retry Backoff**: Exponential backoff starting at 100ms, scaling to a maximum of 500ms.
*   **Circuit Breaker Trigger**: Trip the breaker to OPEN state if the last 10 consecutive calls experience `HTTP 5xx` or timeout.
