# TOGAF Architecture Requirements Specification

This document details the **Architecture Requirements Specification** for the NextGen Bank digital micro-loan platform. It defines the functional, non-functional, security, and regulatory requirements that the target architecture must satisfy, providing clear metrics for design validation.

---

## 1. Business & Functional Requirements

The business capability requirements are organized by the core service domains. All features must adhere to the **STP-First** principle, which prohibits manual processing tasks.

### 1.1 Onboarding & Identity (REQ-ONB)
* **REQ-ONB-01: Real-time PAN Verification**: The system must verify the borrower's PAN active status and fetch their tax-registered name from income tax databases via partner APIs within 3 seconds.
* **REQ-ONB-02: Aadhaar e-KYC**: Identity verification must utilize UIDAI e-KYC (Aadhaar OTP or biometrics) to download masked Aadhaar XML payloads.
* **REQ-ONB-03: Biometric Liveness check**: To prevent spoofing attacks, the mobile client must capture a dynamic video selfie stream, and the onboarding service must calculate a face-match and liveness score. Face match score must exceed 90% against the Aadhaar photograph.

### 1.2 Consent Management (REQ-CON)
* **REQ-CON-01: DEPA Account Aggregator Integration**: Financial transactions (last 6 months) must be fetched digitally using the RBI-approved Account Aggregator framework. PDF bank statement uploads are prohibited to prevent document tampering.
* **REQ-CON-02: Granular and Revocable Consent**: Borrowers must be presented with granular, un-checked consent notices outlining the purpose and duration of data usage. Borrowers must have the ability to revoke consents via the mobile app.
* **REQ-CON-03: Consent Registry Audit**: The system must log every consent transaction (grant, usage, expiration, revocation) to an immutable audit ledger.

### 1.3 Credit Risk Underwriting (REQ-UWE)
* **REQ-UWE-01: Automated Underwriting**: The Underwriting Engine must fetch Credit Bureau scores (CIBIL/Experian), parse Account Aggregator data, calculate key ratios (Debt Service Coverage Ratio, Average Monthly Balances), and return a decision without human intervention.
* **REQ-UWE-02: Rule Threshold Controls**: Risk policy thresholds (e.g., minimum CIBIL score of 650) must be managed via JSON configuration files, enabling risk officers to change policies without deploying new application code.
* **REQ-UWE-03: Device Binding Fraud Prevention**: The platform must bind a user's profile to a single active cryptographic hardware signature, blocking emulator or duplicate device registrations.

### 1.4 Loan Servicing & Ledger (REQ-LMS)
* **REQ-LMS-01: Double-Entry Accounting**: The LMS must execute double-entry accounting to track loan balances, principal splits, interest accruals, processing fees, tax components, and late charges.
* **REQ-LMS-02: Automated Key Fact Statement (KFS)**: Before offer acceptance, the system must generate a Key Fact Statement containing the Annual Percentage Rate (APR), processing fees, net disbursal amount, and repayment schedule, rendering it to the client app.
* **REQ-LMS-03: Digitally Signed Loan Agreement**: Acceptance of the loan offer must trigger the generation of a PDF/A agreement, signed by the borrower via Aadhaar OTP (NSDL/CDSL gateway) and stored securely.

### 1.5 Payments Hub (REQ-PAY)
* **REQ-PAY-01: Automated Disbursal**: Upon successful signature and mandate setup, the platform must trigger fund release to the borrower's verified bank account via IMPS or UPI within 5 seconds.
* **REQ-PAY-02: Auto-Debits Mandate**: Every loan must have an active auto-repayment mandate registered (UPI AutoPay or e-NACH) prior to disbursal.
* **REQ-PAY-03: Destination Validation**: The Payment Hub must verify that the destination bank account name matches the verified e-KYC name before releasing funds, preventing third-party diversion.

---

## 2. Non-Functional Requirements (NFRs)

These quality-of-service parameters define the technical constraints of the architecture.

### 2.1 Latency & Performance (NFR-PERF)
* **NFR-PERF-01: API Latency**: Core internal microservice APIs (LMS, Consent, Onboarding) must respond in under 200ms at the 95th percentile.
* **NFR-PERF-02: Credit Underwriting Engine Execution**: Risk scorecard calculation and bureau ingestion must complete in under 800ms.
* **NFR-PERF-03: Total Application Processing TAT**: The end-to-end user flow (onboarding to fund disbursement in bank account) must take under 5 minutes.

### 2.2 Scale & Throughput (NFR-SCALE)
* **NFR-SCALE-01: Concurrent Users**: The API Gateway and Kubernetes node pools must auto-scale to support 100,000 concurrent active app sessions.
* **NFR-SCALE-02: Transaction Processing**: The LMS sub-ledger and database cluster must support a peak throughput of 10,000 API requests/minute.

### 2.3 Availability & Disaster Recovery (NFR-AVAL)
* **NFR-AVAL-01: System Uptime**: Target availability for core lending microservices and API gateways is **99.95%** (excluding planned maintenance windows).
* **NFR-AVAL-02: Recovery Point Objective (RPO)**: Customer financial records and ledger entries must be replicated synchronously across regional Availability Zones, guaranteeing an RPO of **< 1 minute**.
* **NFR-AVAL-03: Recovery Time Objective (RTO)**: The Disaster Recovery region (active-passive configuration) must take over within **15 minutes** of primary region failure.

---

## 3. Regulatory & Security Requirements

These mandatory compliance controls govern data handling, privacy, and financial operations.

### 3.1 RBI Digital Lending Guidelines (DLG)
* **NFR-REG-01: Direct Disbursal**: Funds must flow directly from NextGen Bank’s corporate pool account to the borrower's verified account. No intermediary or LSP escrow accounts are allowed.
* **NFR-REG-02: Cooling-Off Period**: The LMS must allow the borrower to exit the loan within a **3-day cooling-off window** (for tenures >= 7 days) without penalty, charging only proportionate principal and interest.
* **NFR-REG-03: Grievance Redressal**: The mobile client must present a direct, un-hidden channel to the Grievance Redressal Officer (GRO) and the RBI Ombudsman contact details.

### 3.2 DPDP Act (Data Privacy) & Security
* **NFR-SEC-01: Cell-Level Encryption**: Restricted Personal Data (PII) including Aadhaar, PAN, names, addresses, and phone numbers must be encrypted in the database at the cell level using AES-256-GCM.
* **NFR-SEC-02: Zero Plaintext Logs**: Application and audit logs must never output customer PII. Hashing (SHA-256) or masking must be applied before log writing.
* **NFR-SEC-03: Data Purging**: In compliance with the "Right to Erasure", raw financial statements and credit bureau files of rejected or closed accounts must be permanently purged from database disks within 30 days of status change.
* **NFR-SEC-04: Secure Enclave Key Management**: Cryptographic keys used for database encryption must be managed in a hardware-backed Cloud HSM, utilizing enveloped key hierarchies.

---

## 4. Requirements Traceability Matrix (RTM)

The following matrix traces requirements from business capabilities through to architectural implementation components (Solution Building Blocks - SBBs).

| Requirement ID | ADM Phase | Logical Building Block (ABB) | Target SBB / Tech Component | Verification Method |
| :--- | :--- | :--- | :--- | :--- |
| **REQ-ONB-03** (Liveness) | Phase B | ABB-ONB-01: Identity Orchestrator | SBB-Go-Onboarding + HyperVerge SDK | Automated integration tests; QA biometric spoof tests. |
| **REQ-CON-02** (AA Consent) | Phase C | ABB-CON-01: Consent Manager | SBB-Node-Consent + Setu AA SDK | Consent UI testing; verification of revocable triggers. |
| **REQ-UWE-01** (Auto-Scoring)| Phase C | ABB-CRD-01: Underwriting Engine | SBB-Python-Risk (FastAPI + XGBoost) | Underwriting batch run validation against manual datasets. |
| **REQ-LMS-01** (Ledger) | Phase C | ABB-LCE-01: Ledger Core | SBB-Java-Fineract (PostgreSQL Aurora) | Accounting validation; double-entry balance checks. |
| **REQ-PAY-03** (Validation) | Phase C | ABB-PAY-01: Payment Hub | SBB-Go-Payment (Sponsor Bank APIs) | Integration tests using mock bank API payloads. |
| **NFR-PERF-01** (Latency) | Phase D | ABB-INF-01: Container Cluster | SBB-AWS-EKS + Istio Service Mesh | Performance stress tests using Apache JMeter / Locust. |
| **NFR-SEC-01** (Encryption) | Phase D | ABB-SEC-02: Data Encryption | SBB-AWS-KMS + CloudHSM | Database storage audits; confirmation of encrypted data dumps. |
| **NFR-REG-02** (Cooling-off) | Phase G | ABB-LCE-01: Ledger Core | SBB-Java-Fineract | Manual verification of loan closure APIs within 3-day window. |
| **NFR-SEC-03** (Purging) | Phase C | ABB-PRG-01: Automated Purge | PostgreSQL Cron jobs (PG_Cron) | Automated database checks verifying file deletions. |
