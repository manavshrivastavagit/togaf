# TOGAF Phase G & Phase H: Implementation Governance, Architecture Change Management

This document defines the governance rules, regulatory checklists, and change management processes to ensure the platform remains compliant, secure, and performant over time.

---

## 1. Phase G: Implementation Governance

### 1.1 Architecture Contract Compliance
All feature teams (Mobile, Platform, Underwriting, Core Ledger) must sign off on the Architecture Contract. Compliance is checked automatically during build pipelines and through quarterly architecture audits.

### 1.2 Regulatory Compliance Checklist (Mandatory)

#### 1.2.1 RBI Digital Lending Guidelines (DLG) Compliance
To comply with the RBI's regulations on digital lending platforms:
* **No Intermediary Fund Flows**: All funds must flow directly from NextGen Bank's pool account to the borrower's verified bank account. Third-party gateways or LSPs (Lending Service Providers) must never touch the funds.
* **Key Fact Statement (KFS)**: Before the loan agreement is signed, the mobile app must display the KFS in a standard format. This includes the Annual Percentage Rate (APR), processing fees, penalty interest charges, and the net disbursed amount.
* **Cooling-Off Period**: Borrowers must be given a cooling-off period of at least **3 days** (for loans with tenure of 7 days or more) to exit the loan by repaying the principal and proportionate APR without penalty.
* **Grievance Redressal**: The mobile app must feature a dedicated, single-tap screen displaying the contact details of the Grievance Redressal Officer (GRO) and the RBI Ombudsman.

#### 1.2.2 DPDP Act (Data Privacy) Compliance
To comply with India's Digital Personal Data Protection Act:
* **Granular Consent Notice**: The mobile app must display a clear, multilingual notice detailing exactly what data is collected (e.g., identity, bank transactions) and for what purpose. Consents must not be pre-checked.
* **Right to Erasure**: A customer whose application is rejected, or who has fully closed their loan, has the right to request erasure of their PII. The platform must trigger the automated purge pipeline (as defined in the Data Architecture).
* **Consent Log**: Every consent action (opt-in, opt-out, revocation) must register a cryptographically signed transaction in the immutable Consent Log.

---

## 2. Phase H: Architecture Change Management

### 2.1 Change Management Process
As new technologies emerge or regulatory guidelines change, the platform architecture will evolve. The change process follows these steps:

```
[Request for Architecture Change (RFC)] 
                │
                ▼
        [Impact Analysis] ──► (Assess Business, Data, App, Tech impact)
                │
                ▼
      [Architecture Board] ──► (Approve, Reject, or request modification)
                │
                ▼
        [Implementation] ──► (Update task.md & architecture files)
```

### 2.2 Change Classification Matrix

| Change Level | Description | Example | Governance Action |
| :--- | :--- | :--- | :--- |
| **Minor Change** | Localized, non-breaking modifications that do not alter the system integration map. | Updating risk model coefficients; upgrading Redis version. | Approved by Dev Lead; logged in Git commit history. |
| **Major Change** | Modifications impacting interfaces between microservices or data schemas. | Upgrading external API integration to a new version (e.g., NeSL API v2); altering database schema. | Requires RFC; reviewed and signed off by the Enterprise Architect. |
| **Strategic Change** | Major structural shifts affecting business models, regulatory compliance, or core technology. | Moving from hybrid cloud to multi-cloud; replacing the core ledger engine. | Requires full Architecture Board approval, board presentation, and update to target architecture blueprints. |

---

## 3. Operational Metrics & Service Level Agreements (SLAs)

To ensure the platform operates reliably, the following operational SLAs and KPIs are monitored:

### 3.1 Performance KPIs
* **End-to-End Application Processing Time**: Target: **< 5 minutes** (from onboarding start to fund disbursement).
* **API Response Latency**: Target: **< 200ms** for 95% of internal microservice requests.
* **System Availability (Uptime)**: Target: **99.95%** for core microservices and API gateways.

### 3.2 Credit & Operations KPIs
* **Auto-Rejection Rate**: Percentage of applications automatically filtered out (to evaluate scorecard accuracy).
* **Straight-Through Processing (STP) Ratio**: Target: **100%** (zero manual touchpoints).
* **First Payment Default (FPD)**: Monitoring credit risk effectiveness.
* **Mandate Success Rate**: Percentage of auto-debits executed successfully on the monthly billing date.
