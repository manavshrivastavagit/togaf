# Architecture Waiver Record: WAV-2026-001

Concession for temporary higher response latency on the **CIBIL Credit Bureau API mock** in the staging environment.

---

## 1. Metadata & Control

| Field | Details |
| :--- | :--- |
| **Waiver ID** | WAV-2026-001 |
| **Title** | Higher Staging Latency on CIBIL API Mock |
| **System / Module** | Risk Underwriting Service (`python-risk`) |
| **Requestor** | Lead Developer, Risk Team |
| **Date Approved** | 2026-05-15 |
| **Expiration Date**| 2026-11-15 (Waiver duration: 180 Days) |
| **Status** | **Active (Temporary)** |

---

## 2. Standard Deviated From
*   **Standard Rule**: Target API Gateway endpoint latency must be **< 200 milliseconds** for the 95th percentile under test loads.
*   **Deviation**: The risk evaluation endpoint (`POST /risk/underwrite`) averages **850ms** in staging due to the external Credit Bureau sandbox latency.

---

## 3. Rationale for Deviation
The CIBIL Credit Bureau sandbox provider operates on shared public sandbox endpoints that do not have dedicated leased-line support or performance SLAs. The external API consistently takes 700ms–900ms to parse queries, making it impossible for the underwriting service to meet the 200ms target in the staging environment.

---

## 4. Compensating Controls & Mitigations
*   **Circuit Breakers**: A Resilience4j circuit breaker has been configured on the outbound bureau query client with a timeout threshold of 2.0 seconds, preventing thread pool depletion.
*   **Staged Underwriting**: If the bureau query exceeds 2s, the circuit breaker opens, and the underwriting service routes the user to a "delayed offering evaluation" queue, triggering an SMS webhook rather than dropping the request.

---

## 5. Remediation Plan

1.  **Dedicated leased line**: The network engineering team has ordered an AWS Direct Connect leased line connection to the CIBIL staging servers (target completion: Sept 2026).
2.  **Staging mock implementation**: The development team will build an internal CIBIL mock service inside the AWS EKS cluster by August 2026 to run performance testing without hitches from the external sandbox.
3.  **Remediation Gate**: Re-evaluate the latency under load once the leased line is active and close this waiver.

---

## 6. Approvals
*   **Lead Architect**: *Supportive (with conditions)*
*   **Chief Information Security Officer (CISO)**: *Approved*
*   **Architecture Board Chairperson**: *Approved*
