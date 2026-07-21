# TOGAF Phase A: Business Capabilities Catalog

This document defines the **Business Capability Catalog** for NextGen Bank's **STP Micro-Loan Mobile Platform**. The catalog outlines the key L1 and L2 capabilities required to support digital lending operations, assesses their baseline and target maturity, and specifies their ownership and inputs/outputs.

---

## 1. Business Capability Map (L1 & L2)

The capability map is structured into seven primary L1 capability areas, each decomposed into specialized L2 capabilities.

```
NextGen Bank Digital Lending Business Capabilities
├── 1. Digital Acquisition & Engagement (L1-ACQ)
│   ├── 1.1 Lead Generation & Referral Orchestration (L2-ACQ-01)
│   ├── 1.2 In-App Product Personalization (L2-ACQ-02)
│   └── 1.3 Marketing Campaign Analytics (L2-ACQ-03)
├── 2. Customer Onboarding & KYC (L1-ONB)
│   ├── 2.1 Aadhaar e-KYC Verification (L2-ONB-01)
│   ├── 2.2 PAN & Identity Verification (L2-ONB-02)
│   └── 2.3 Biometric Liveness Capture (L2-ONB-03)
├── 3. Data Consent Management (L1-CON)
│   ├── 3.1 Account Aggregator Consent Lifecycle (L2-CON-01)
│   ├── 3.2 Consent Registry & Cryptographic Audit Logging (L2-CON-02)
│   └── 3.3 User Consent Preference Center (L2-CON-03)
├── 4. Risk Assessment & Underwriting (L1-RISK)
│   ├── 4.1 Credit Bureau Integration & Parsing (L2-RISK-01)
│   ├── 4.2 Financial Statement/Transaction Analysis (L2-RISK-02)
│   ├── 4.3 Device Telemetry Fraud Engine (L2-RISK-03)
│   └── 4.4 Underwriting Scorecard Evaluation (L2-RISK-04)
├── 5. Loan Contract Management (L1-CTR)
│   ├── 5.1 Automated Agreement Assembly (L2-CTR-01)
│   ├── 5.2 Aadhaar e-Sign Orchestration (L2-CTR-02)
│   └── 5.3 Digital Document Custody & NeSL Registration (L2-CTR-03)
├── 6. Payment & Disbursal Orchestration (L1-PAY)
│   ├── 6.1 Repayment Mandate Registration (UPI AutoPay/eNACH) (L2-PAY-01)
│   ├── 6.2 Instant Fund Disbursal (IMPS/NEFT/UPI) (L2-PAY-02)
│   └── 6.3 Repayment Execution Hub (L2-PAY-03)
└── 7. Servicing & Ledger Management (L1-LEDG)
    ├── 7.1 Loan Lifecycle Management (L2-LEDG-01)
    ├── 7.2 Core Ledger & Sub-Ledger Accounting (L2-LEDG-02)
    ├── 7.3 Interest, Penalty & Fees Calculation (L2-LEDG-03)
    └── 7.4 End-of-Day (EOD) Reconciliation (L2-LEDG-04)
```

---

## 2. Business Capability Definitions

### L1-ONB: Customer Onboarding & KYC
*   **Definition**: The capability to identify, verify, and validate a prospective borrower's credentials using digital identity sources.
    *   **L2-ONB-01 Aadhaar e-KYC Verification**: Programmatic verification of name, address, photo, and DOB via UIDAI secure OTP.
        *   *Inputs*: Aadhaar Number, Customer OTP.
        *   *Outputs*: Signed e-KYC XML/JSON payload, KYC Verification Status.
        *   *Business Owner*: Head of Digital Compliance.
    *   **L2-ONB-02 PAN & Identity Verification**: Automated check against the NSDL/Income Tax database to verify identity existence and validity.
        *   *Inputs*: PAN Number, Name, DOB.
        *   *Outputs*: PAN Status (Valid/Active), Name Match Score.
        *   *Business Owner*: Head of Digital Compliance.
    *   **L2-ONB-03 Biometric Liveness Capture**: Real-time camera stream analysis to detect active presence and match faces against UIDAI photographs.
        *   *Inputs*: Mobile Video Stream / Photo Capture.
        *   *Outputs*: Liveness Score (%), Face Match Match Confidence (%).
        *   *Business Owner*: Head of Risk Control.

### L1-CON: Data Consent Management
*   **Definition**: The capability to capture, record, store, and manage user consents for data access and data sharing in compliance with DPDP and DEPA.
    *   **L2-CON-01 Account Aggregator Consent Lifecycle**: Generating and submitting structured consent requests to financial information users (FIUs).
        *   *Inputs*: Customer Mobile, Select Bank, Consent Parameters.
        *   *Outputs*: Consent Handle, Consent Status (Approved/Rejected/Expired).
        *   *Business Owner*: Chief Privacy Officer.
    *   **L2-CON-02 Consent Registry & Cryptographic Audit Logging**: Storing every consent state change in an immutable, signed database ledger.
        *   *Inputs*: Consent State Payload, Timestamp.
        *   *Outputs*: Immutable Transaction Hash, Cryptographic Signature.
        *   *Business Owner*: CISO.

### L1-RISK: Risk Assessment & Underwriting
*   **Definition**: The capability to evaluate a borrower's creditworthiness and default probability using automated data analysis.
    *   **L2-RISK-01 Credit Bureau Integration & Parsing**: Fetching CIBIL/Experian credit reports and parsing historical tradelines.
        *   *Inputs*: Verified Identity (PAN, Aadhaar Name, Phone).
        *   *Outputs*: CIBIL Score, Active Loan Balances, DPD History.
        *   *Business Owner*: Chief Risk Officer.
    *   **L2-RISK-02 Financial Statement/Transaction Analysis**: Parsing bank transaction histories retrieved via Account Aggregators to assess cash flows.
        *   *Inputs*: Encrypted Financial Data (XML/JSON via AA).
        *   *Outputs*: Average Monthly Balance (AMB), Income Estimate, Bounce History.
        *   *Business Owner*: Lead Risk Model Developer.
    *   **L2-RISK-04 Underwriting Scorecard Evaluation**: Executing the automated risk scorecard to determine loan limit approvals and dynamic pricing.
        *   *Inputs*: Parsed Bureau Data, Transaction Analytics, Device Fraud Risk Score.
        *   *Outputs*: Credit Limit (INR), Interest Rate (%), Approval Decision (Accept/Reject).
        *   *Business Owner*: Chief Risk Officer.

### L1-PAY: Payment & Disbursal Orchestration
*   **Definition**: The capability to setup auto-repayment instruments and execute real-time fund releases.
    *   **L2-PAY-01 Repayment Mandate Registration**: Registering UPI AutoPay or eNACH mandates with NPCI.
        *   *Inputs*: Verified Bank Account, IFSC, EMI Amount.
        *   *Outputs*: Mandate Registration Status, Unique Mandate Reference Number (UMRN).
        *   *Business Owner*: Head of Payments & Settlement.
    *   **L2-PAY-02 Instant Fund Disbursal**: Executing real-time bank transfers (IMPS/UPI/NEFT) to verified borrower accounts.
        *   *Inputs*: Disbursal Payload, Destination Account, Amount.
        *   *Outputs*: Bank Transaction ID, Disbursal Confirmation.
        *   *Business Owner*: Head of Payments & Settlement.

### L1-LEDG: Servicing & Ledger Management
*   **Definition**: The capability to maintain the financial record of all loan accounts, perform interest accruals, fees logging, and reconciliations.
    *   **L2-LEDG-02 Core Ledger & Sub-Ledger Accounting**: Managing the double-entry accounting records for principal, interest, and repayments.
        *   *Inputs*: Transactions Feed, Loan Schedules.
        *   *Outputs*: Trial Balance, Sub-Ledger Status.
        *   *Business Owner*: Head of Financial Control.
    *   **L2-LEDG-04 End-of-Day (EOD) Reconciliation**: Performing automated balancing checks between the lending ledger, payment gateway logs, and Core Banking System (CBS) pools.
        *   *Inputs*: LMS ledger records, Payment Gateway success reports, Core Bank accounts reports.
        *   *Outputs*: Discrepancy Registry, Reconciliation Reports.
        *   *Business Owner*: Head of Financial Control.

---

## 3. Capability Maturity Assessment

This table assesses the baseline maturity of NextGen Bank's capabilities and defines target maturity levels for the micro-loan platform:

### Maturity Scale:
1.  **Initial**: Ad-hoc, undocumented, high manual intervention.
2.  **Repeatable**: Process defined, but relies heavily on specific human skills and basic tools.
3.  **Defined**: Standardized, documented, partially integrated.
4.  **Managed**: Quantitatively measured, automated workflows, low manual steps.
5.  **Optimizing**: Continuous improvement, real-time telemetry, automated self-healing.

| Capability ID | Capability Name | Baseline | Target | Critical Gap / Initiative |
| :--- | :--- | :---: | :---: | :--- |
| **L2-ONB-01** | Aadhaar e-KYC Verification | 3 | 5 | Baseline relies on external manual webview portals. Target requires native API integration for OTP validation to lower drop-off. |
| **L2-ONB-03** | Biometric Liveness Capture | 1 | 5 | No baseline capability. Initiative: Procure and integrate a secure native mobile video liveness SDK with anti-spoofing algorithms. |
| **L2-CON-01** | Account Aggregator Consent | 2 | 5 | Baseline requires manual PDF uploads. Target: Integrate with licensed Account Aggregators (Sahamati framework) via APIs. |
| **L2-CON-02** | Consent Registry | 2 | 5 | Baseline logs consent in flat text database files. Target: Deploy a dedicated, cryptographically signed ledger database (e.g., QLDB or signed tables). |
| **L2-RISK-02**| Financial Statement Analysis | 2 | 5 | Baseline uses manual PDF parsing. Target: Automated transactional analyzer parsing AA JSON feeds in real-time. |
| **L2-RISK-04**| Underwriting Scorecard | 3 | 5 | Baseline scorecards run daily as batch scripts. Target: Deploy real-time rule engines (e.g., Python FastAPI/OPA) executing scorecards in < 500ms. |
| **L2-PAY-01** | Repayment Mandate | 2 | 5 | Baseline relies on physical NACH forms. Target: Implement UPI AutoPay (NPCI) and netbanking-based e-NACH mandates. |
| **L2-PAY-02** | Instant Fund Disbursal | 3 | 5 | Baseline transactions processed in batches. Target: Real-time API integration with the bank's IMPS/UPI routing hub. |
| **L2-LEDG-02**| Core Ledger | 3 | 4 | Baseline runs on a legacy core banking system with high latency. Target: Implement an isolated digital lending ledger (e.g., Apache Fineract) syncing to CBS at EOD. |
| **L2-LEDG-04**| EOD Reconciliation | 2 | 5 | Baseline relies on manual Excel file merges by finance operations. Target: Fully automated ETL pipeline reconciling ledger transactions daily. |

---

## 4. Strategic Mapping to Value Stream

```
                   FULLY AUTOMATED VALUE STREAM MAPPING
┌───────────────────┐    ┌───────────────────┐    ┌───────────────────┐
│     ONBOARD       │───>│    UNDERWRITE     │───>│      EXECUTE      │
└───────────────────┘    └───────────────────┘    └───────────────────┘
         │                         │                        │
         ▼                         ▼                        ▼
 ┌───────────────┐        ┌───────────────┐        ┌────────────────┐
 │ L2-ONB-01     │        │ L2-CON-01     │        │ L2-CTR-01      │
 │ Aadhaar eKYC  │        │ AA Consent    │        │ Agreement      │
 ├───────────────┤        ├───────────────┤        ├────────────────┤
 │ L2-ONB-02     │        │ L2-RISK-01    │        │ L2-PAY-01      │
 │ PAN check     │        │ Bureau Fetch  │        │ Repayment Mand │
 ├───────────────┤        ├───────────────┤        ├────────────────┤
 │ L2-ONB-03     │        │ L2-RISK-02    │        │ L2-PAY-02      │
 │ Video Liveness│        │ Trans Analysis│        │ Disbursal Rel  │
 └───────────────┘        └───────────────┘        └────────────────┘
```
Each stage in the value stream is powered by specific L2 capabilities, ensuring that any capability failure is isolated and does not disrupt the entire customer journey.
