# Technology Architecture: API Gateway Governance & Rate Limiting Policy

This document defines the security, throttling, and routing policies enforced at the **API Gateway Ingress Layer** (Kong/Apigee) for NextGen Bank's **STP Micro-Loan Platform**.

---

## 1. Gateway Security Policies

All public incoming client traffic must pass through the API Gateway, which enforces:
*   **Protocol**: HTTPS (TLS v1.3 mandatory). Older TLS versions (v1.0, v1.1, v1.2) are blocked at the edge.
*   **WAF Filters**: Web Application Firewall (WAF) inspects payloads for SQL Injection, Cross-Site Scripting (XSS), and automated scraper headers.
*   **Token Verification**: The gateway intercepts and validates the JWT Access Token in the `Authorization: Bearer <token>` header against the Keycloak OIDC public keys. Unauthorized calls are rejected with HTTP 401.

---

## 2. Ingress Rate Limiting & Throttling Rules

To prevent resource exhaustion (DDoS) and mitigate financial fraud (e.g., testing credentials or spamming OTP services), the gateway enforces strict endpoint-level rate limits:

| Route / Endpoint | Metric Rate Limit | Action on Violation | Security Objective |
| :--- | :--- | :--- | :--- |
| `POST /identity/verify-pan` | 10 requests / min per IP | HTTP 429 Too Many Requests | Prevent PAN enumeration harvesting attacks. |
| `POST /identity/aadhaar-kyc` | 5 requests / min per Device | HTTP 429 & Temp Block Device (1 hr) | Mitigate Aadhaar OTP spamming charges. |
| `POST /risk/underwrite` | 2 requests / min per User | HTTP 429 | Prevent credit scoring model gaming. |
| `POST /payment/disburse` | 1 request / min per Account | HTTP 429 & Alert Admin | Prevent duplicate disbursal transaction loops. |

---

## 3. JWT Claims Mapping & Header Ingress

The gateway decodes valid OIDC tokens and strips downstream headers, forwarding only standard, sanitized headers to the microservice mesh:

```
┌─────────────────┐       ┌─────────────────┐       ┌──────────────────────┐
│  Mobile Client  │ ────> │   API Gateway   │ ────> │  Go-Onboarding Service│
│ (JWT in Header) │       │ (Verify Token)  │       │  (Reads Sanitized H) │
└─────────────────┘       └─────────────────┘       └──────────────────────┘
                           Decodes JWT & maps:
                           - X-User-Id: Token Sub
                           - X-User-Roles: Role Claims
                           - X-Trace-Id: Request Trace
```

Downstream microservices (such as `go-onboarding` and `python-risk`) must reject any requests containing raw claims that do not originate from the gateway's internal mTLS network.
