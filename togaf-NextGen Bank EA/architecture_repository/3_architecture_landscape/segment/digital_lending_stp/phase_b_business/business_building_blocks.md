# TOGAF Phase B: Business Architecture Building Blocks (BABBs)

This document contains the **Business Architecture Building Block (BABB) Catalog** for NextGen Bank's **STP Micro-Loan Mobile Platform**. These building blocks represent reusable business capabilities, processes, and rules that govern the platform's operational integrity and regulatory compliance.

---

## 1. Overview of BABBs

In the TOGAF ADM, Business Architecture Building Blocks (BABBs) define *what* business functions and rules are required. They form the logical requirements that later map to Application Architecture Building Blocks (AABBs) and Technology Architecture Building Blocks (TABBs) during Phase C and Phase D.

---

## 2. Business Architecture Building Block Catalog

---

### 2.1 Onboarding & Identity Verification (BABB-ONB-01)

*   **Description**: Orchestrates customer identity verification, duplicate registration detection, and liveness checks using India Stack APIs and biometric engines.
*   **Target Performance SLA**: Complete verification in < 15 seconds.
*   **Associated Business & Compliance Rules**:
    *   **Rule-ONB-01 (Age Verification)**: The applicant must be between **18 and 35 years of age** based on the verified date of birth returned from Aadhaar.
    *   **Rule-ONB-02 (Name Matching)**: The name returned from NSDL (PAN check) and UIDAI (Aadhaar check) must match. If spelling differences exist, the Jaro-Winkler distance score must be **>= 0.85**.
    *   **Rule-ONB-03 (Biometric Match)**: The real-time camera face capture must match the UIDAI photograph with a confidence level **>= 90%** as calculated by the face-match engine.
    *   **Rule-ONB-04 (Liveness Threshold)**: The biometric liveness stream must return an anti-spoofing rating **>= 95%** to prevent static photo or video playbacks.

---

### 2.2 Consent Orchestration & Compliance (BABB-CON-01)

*   **Description**: Governs the generation, capture, logging, and lifecycle of customer consents for data retrieval, storage, and processing. Ensures alignment with the DPDP Act and the DEPA framework.
*   **Target Performance SLA**: Consent registration response < 2 seconds.
*   **Associated Business & Compliance Rules**:
    *   **Rule-CON-01 (Granularity)**: Blanket consent is prohibited. Separate consent flags must be collected for: (a) credit bureau queries, (b) bank statement retrieval, (c) notifications via WhatsApp/SMS, and (d) marketing cross-sell.
    *   **Rule-CON-02 (Data Minimization)**: Underwriting data (historical bank transactions) can only be accessed once and stored for a maximum of **30 days** following application decisioning.
    *   **Rule-CON-03 (Revocability)**: Customers must have access to an in-app console to revoke consent. Revocation of underwriting consent on active loans is blocked; revocation on closed loans or rejected applications must trigger an automated deletion of all historical transaction logs within 48 hours.
    *   **Rule-CON-04 (Immutable Audit Trail)**: Every consent approval, modification, or revocation must be recorded in an immutable ledger with a digital signature of the consent payload.

---

### 2.3 Credit Assessment & Underwriting (BABB-RISK-01)

*   **Description**: Automates risk assessment by analyzing financial statements, credit bureaus, and alternative device telemetry. Resolves approvals, limits, and dynamic pricing.
*   **Target Performance SLA**: Underwriting execution < 30 seconds.
*   **Associated Business & Compliance Rules**:
    *   **Rule-RISK-01 (CIBIL Floor)**: The primary applicant must have a CIBIL score **>= 650**.
    *   **Rule-RISK-02 (Delinquency Filter)**: The applicant must have zero (0) Days Past Due (DPD) events greater than 30 days in their bureau record over the past 12 months.
    *   **Rule-RISK-03 (Debt Service Coverage Ratio - DSCR)**: Total monthly obligations (existing EMIs + proposed NextGen Bank EMI) must not exceed **45%** of the estimated monthly net income.
    *   **Rule-RISK-04 (Cheque Bounce Limit)**: The bank transactions parsed via Account Aggregator must show **fewer than 2 cheque bounces or auto-debit failures** due to insufficient funds in the last 6 months.

---

### 2.4 Repayment Mandate & Payment Hub (BABB-PAY-01)

*   **Description**: Orchestrates the automated setup of repayment instruments and the instant disbursement of loan funds to verified customer bank accounts.
*   **Target Performance SLA**: Mandate registration callback < 5 seconds; IMPS disbursement < 10 seconds.
*   **Associated Business & Compliance Rules**:
    *   **Rule-PAY-01 (Mandate Pre-requisite)**: No loan funds can be disbursed until a valid NPCI UPI AutoPay or e-NACH mandate status returns `ACTIVE`.
    *   **Rule-PAY-02 (Beneficiary Verification)**: Prior to disbursal, a **Penny Drop Test** must be executed on the destination account. The name returned by the beneficiary bank must match the Aadhaar verified name with a score **>= 90%**.
    *   **Rule-PAY-03 (Account Consistence)**: The account used for repayment mandate registration must be identical to the destination bank account for fund disbursal.
    *   **Rule-PAY-04 (Direct Fund Flow)**: In compliance with the RBI DLG, all fund releases must flow directly from NextGen Bank’s corporate pool account to the borrower’s bank account, with zero routing via intermediary accounts.

---

### 2.5 Loan Servicing & Sub-Ledger (BABB-LEDG-01)

*   **Description**: Maintains the financial state of all active loan agreements, executing interest accruals, processing EMI allocations, and reconciling daily balances.
*   **Target Performance SLA**: Batch processing of end-of-day balances < 2 hours.
*   **Associated Business & Compliance Rules**:
    *   **Rule-LEDG-01 (Double-Entry Balance)**: Every payment or interest debit must generate a dual-ledger entry balancing assets and liabilities. Direct manual edits to ledger balances are prohibited.
    *   **Rule-LEDG-02 (Payment Allocation Order)**: Repayments received must be allocated in the following priority order: (1) Penalties/Overdue Charges, (2) Interest Overdue, (3) Current Interest, (4) Principal Overdue, (5) Current Principal.
    *   **Rule-LEDG-03 (Automated Reconciliation)**: An automated EOD batch job must reconcile the lending sub-ledger against the payment gateway transaction logs and the bank's core banking pool account. Any discrepancy must raise an alert to the Financial Operations dashboard.

---

## 3. Business Rule Decision Matrix

This matrix maps core business rules to their policy owners and validation endpoints:

| Rule ID | Policy Domain | Policy Owner | System Validation Endpoint |
| :--- | :--- | :--- | :--- |
| **Rule-ONB-02** | KYC / Identity | Head of digital Compliance | Onboarding Service (NSDL/UIDAI fuzzy match) |
| **Rule-CON-02** | Privacy | Chief Privacy Officer | Consent Service (Data Purge Cron Job) |
| **Rule-RISK-01**| Credit Risk | Chief Risk Officer | Risk Engine (Bureau API Parser) |
| **Rule-RISK-03**| Underwriting | Lead Underwriter | Risk Engine (DSCR calculator) |
| **Rule-PAY-02** | Settlements | Head of Payments | Payment Hub (Penny Drop API) |
| **Rule-LEDG-02**| Financial Control| Chief Financial Officer | Loan Management System Ledger |

---

## 4. BABB to Phase C/D ABB Mapping

To maintain traceability across the TOGAF ADM, this table maps Phase B Business Building Blocks to subsequent Phase C (Application/Data) and Phase D (Technology) Building Blocks:

| Business Building Block (BABB) | Phase C Application ABB (AABB) | Phase C Data ABB | Phase D Technology ABB (TABB) |
| :--- | :--- | :--- | :--- |
| **BABB-ONB-01** Onboarding | Onboarding Service, Liveness SDK | Customer Master DB | Managed Kubernetes, WAF |
| **BABB-CON-01** Consent | Consent Orchestrator | Consent Audit DB, QLDB | KMS, Cloud HSM |
| **BABB-RISK-01** Underwriting | Scorecard Engine, Bureau Client | Risk Profile Cache (Redis) | Python Underwriting Cluster |
| **BABB-PAY-01** Payment Hub | Payment Orchestration Service | Settlement Logs | Istio Service Mesh, mTLS |
| **BABB-LEDG-01** Ledger | LMS Core (Fineract wrapper) | Sub-Ledger DB (Postgres) | EOD Batch Processor, Vault |
