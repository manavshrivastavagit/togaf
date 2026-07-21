# TOGAF Deliverable Template: Architecture Waiver Request

An **Architecture Waiver Request** is submitted by a project team to obtain authorization to temporarily or permanently deviate from established architectural standards or principles.

---

## 1. Document Control & Metadata

| Field | Description |
| :--- | :--- |
| **Waiver ID** | WAV-YYYY-XXXX (Assigned by EA Office) |
| **Title** | [Short, descriptive title] |
| **Requesting System / Module** | [e.g., Onboarding Service / Scorecard Engine] |
| **Requestor Name & Role** | [Name / Title] |
| **Date Filed** | [YYYY-MM-DD] |
| **Standard/Principle Deviated From**| [e.g., Target API Gateway latency must be < 200ms] |
| **Waiver Type** | [Temporary (specify duration) / Permanent] |
| **Requested Expiration Date** | [YYYY-MM-DD (Max 180 days for temporary)] |

---

## 2. Business Justification for Deviation

### 2.1 Context
[Explain the current project situation and why the architecture standard cannot be met under the present constraints.]

### 2.2 Rationale
[Provide the business rationale for the deviation, such as: critical vendor integration constraints, unexpected technical blockers, or market-driven urgency.]

---

## 3. Alternative Options Explored

Document the alternative designs that were considered and why they were rejected in favor of this waiver request:

| Option Explored | Pros | Cons | Rejection Rationale |
| :--- | :--- | :--- | :--- |
| **Option 1**: [Description] | [Benefits] | [Drawbacks] | [Why discarded?] |
| **Option 2**: [Description] | [Benefits] | [Drawbacks] | [Why discarded?] |

---

## 4. Security, Compliance, & Risk Analysis

Identify any security, compliance, or operational risks introduced by this deviation, and provide compensating controls:

| Identified Risk | Risk Level | Description of Exposure | Compensating Controls / Mitigations |
| :--- | :---: | :--- | :--- |
| **Risk 1** (e.g., Data exposure) | [High/Med] | [e.g., Temporary log fields contain raw PII] | [e.g., Strict log server access control, automated cleanup script] |
| **Risk 2** (e.g., Vendor latency) | [Medium] | [e.g., Downstream API latency exceeds 500ms] | [e.g., Asynchronous polling, local circuit breakers] |

---

## 5. Actionable Remediation Plan

Detail the concrete engineering steps and timeline to resolve the deviation and restore full compliance with the standard:

| Phase | Milestone / Remediation Step | Target Completion Date | Assigned Resource |
| :--- | :--- | :--- | :--- |
| **Phase 1** | [e.g., Implement local caching adapter] | [YYYY-MM-DD] | Developer A |
| **Phase 2** | [e.g., Refactor backend db query indexes] | [YYYY-MM-DD] | DBA / Lead Dev |
| **Phase 3** | [e.g., Validate latency under load and close waiver]| [YYYY-MM-DD] | QA Engineer |

---

## 6. Review & Decision Sign-offs

### 6.1 Enterprise Architecture Review
*   **Lead Architect Assessment**: [Supportive / Neutral / Against]
*   **Comments**: [Lead architect's comments and conditions]
*   **Signature**: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ (Date: \_\_\_\_\_\_\_\_\_\_)

### 6.2 Security/CISO Review (If Applicable)
*   **Security Assessment**: [Approved / Rejected / Approved with Conditions]
*   **Comments**: [CISO comments and safety guidelines]
*   **Signature**: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ (Date: \_\_\_\_\_\_\_\_\_\_)

### 6.3 Architecture Board Decision
*   **Decision**: [Approved / Conditional Approval / Rejected]
*   **Board Conditions**: [Any specific restrictions or requirements during the waiver period]
*   **Approved Expiration Date**: [YYYY-MM-DD]
*   **Board Chairperson Signature**: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ (Date: \_\_\_\_\_\_\_\_\_\_)
