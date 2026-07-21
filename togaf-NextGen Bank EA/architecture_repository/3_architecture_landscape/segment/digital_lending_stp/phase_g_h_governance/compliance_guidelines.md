# TOGAF Phase G & H: Regulatory Compliance Guidelines

This document details the mandatory compliance audits, code verification processes, and functional checks to satisfy the **Reserve Bank of India (RBI) Digital Lending Guidelines (DLG)** and India's **Digital Personal Data Protection (DPDP) Act 2023** on NextGen Bank's micro-loan platform.

---

## 1. RBI Digital Lending Guidelines (DLG) Audit Checklist

All systems, APIs, and client interfaces must pass these checks prior to production deployment.

### 1.1 Direct Fund Flows (No Intermediaries)
* **Rule**: All loan disbursements and repayments must execute directly between NextGen Bank's pool account and the borrower's verified bank account. No Lending Service Provider (LSP) or third-party intermediary pool accounts are permitted to hold or touch funds.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DLG-DF-01** | Payment gateway routing validation. | Code review of the Payment Hub API routing configuration. Verify that beneficiary bank accounts map directly to the customer's validated bank account. | Ledger & Settlement Team | **Mandatory** |
| **DLG-DF-02** | Settlement destination verification. | Query database logs for transactions to ensure no intermediate nodal/escrow account routes are present in the transaction chain. | Compliance / Auditor | **Mandatory** |
| **DLG-DF-03** | Third-party service fee billing. | Confirm that any fees payable to LSPs (e.g., marketing fee, tech fee) are paid directly by NextGen Bank, and not deducted from the customer's loan disbursement amount. | Ledger & Settlement Team | **Mandatory** |

---

### 1.2 Key Fact Statement (KFS) Disclosure
* **Rule**: A standardized Key Fact Statement (KFS) must be displayed to the customer in the mobile app and sent via email/SMS *prior* to execution of the loan agreement. The KFS must list the Annual Percentage Rate (APR), interest rate, fees, default interest charges, and the net disbursed amount.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DLG-KF-01** | KFS UI validation. | Automated UI testing to confirm that the KFS is displayed on a single, non-dismissible screen before the "e-Sign Contract" button becomes active. | Onboarding & Consent Team | **Mandatory** |
| **DLG-KF-02** | APR Calculation accuracy. | Unit tests validating that the APR calculation includes all fees (processing fee, documentation charges) using the standard IRR formula. | Risk & Underwriting Team | **Mandatory** |
| **DLG-KF-03** | KFS Document Persistence. | Verify that a PDF copy of the generated KFS is written to the customer's account repository and dispatched via registered email immediately after loan booking. | Onboarding & Consent Team | **Mandatory** |

---

### 1.3 Mandatory Cooling-Off / Look-Back Period
* **Rule**: Borrowers must be given a cooling-off period of at least **3 days** (for loan tenures of 7 days or more) to exit the loan by paying the principal and proportionate APR without penalty.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DLG-CO-01** | Exit logic execution. | Verify the LMS config allows a customer to trigger a "Prepayment with Zero Penalty" in the mobile app within 72 hours of disbursal. | Ledger & Settlement Team | **Mandatory** |
| **DLG-CO-02** | Moratorium & Interest billing. | Ensure that interest charged during the cooling-off period is strictly pro-rata (proportionate APR) and does not contain hidden pre-payment fees. | Ledger & Settlement Team | **Mandatory** |

---

### 1.4 Grievance Redressal Mechanism
* **Rule**: The platform must designate a Grievance Redressal Officer (GRO) and display their contact info (name, email, phone) and the RBI Ombudsman details prominently in the app.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DLG-GR-01** | In-app Help & Support Link. | Verify the presence of a "Grievance Support" link on the Account settings page, linking directly to the GRO details. | Onboarding & Consent Team | **Mandatory** |
| **DLG-GR-02** | Turnaround tracking (30 days). | Check support ticketing system rules. If a complaint is not resolved within 30 days, the ticket must automatically escalate to the compliance officer and trigger an email to the customer with instructions on reaching the RBI Ombudsman. | Platform Engineering Team | **Mandatory** |

---

## 2. DPDP Act 2023 Compliance Checklist

All data collection, processing, and storage flows must adhere to the data privacy rules of the DPDP Act.

### 2.1 Granular, Bilingual Consent Notice
* **Rule**: Data collection must be preceded by a clear notice detailing the specific categories of personal data collected and the precise purpose of processing. The notice must be available in English and scheduled scheduled regional languages.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DPDP-CN-01** | Granular check-boxes (No pre-checks). | UI walkthrough. Verify that Aadhaar e-KYC, Credit Bureau, and Account Aggregator data sharing consents require individual, active toggles by the user. | Onboarding & Consent Team | **Mandatory** |
| **DPDP-CN-02** | Notice Versioning. | Verify that consent notices are version-controlled in the database, logging which notice version the customer agreed to. | Onboarding & Consent Team | **Mandatory** |
| **DPDP-CN-03** | Language support. | Perform localization test verifying notice displays correctly in English and local languages. | Onboarding & Consent Team | **Mandatory** |

---

### 2.2 Right to Erasure & Data Retention
* **Rule**: A customer has the right to request erasure of their personal data. The bank must purge this data once the processing purpose is fulfilled, unless retention is mandated by other statutory laws (e.g., PMLA record retention for 5 years).

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DPDP-RE-01** | Purge Pipeline validation. | Run a mock erasure request for a rejected customer. Check databases to ensure PII records are cleared, leaving only anonymized transaction hashes for reporting. | Onboarding & Consent Team | **Mandatory** |
| **DPDP-RE-02** | Statutory Hold Check. | Verify that the purge script blocks data deletion requests for customers with active loans or loans closed less than 5 years ago (per PMLA guidelines). | Ledger & Settlement Team | **Mandatory** |

---

### 2.3 Cryptographically Signed Consent Log
* **Rule**: Every consent event (grant, update, revocation) must be recorded in an immutable, cryptographically signed ledger.

| Audit ID | Audit Requirement | Verification Method | Responsible Team | Target Status |
| :--- | :--- | :--- | :--- | :--- |
| **DPDP-CL-01** | SHA-256 Hashing. | Inspect the Consent Registry database. Verify that each record contains a SHA-256 hash of the `(CustomerID + Consent Notice ID + Timestamp + Consent Status)` signed by the system private key. | Platform Engineering Team | **Mandatory** |
| **DPDP-CL-02** | Revocation propagation. | Verify that revoking a consent (e.g., removing AA access) instantly triggers API calls to the middleware (Decentro) to delete the active data-sharing token. | Onboarding & Consent Team | **Mandatory** |

---

## 3. Compliance Verification & Sign-off Gateways

No code release is deployed to production without clearing the automated and manual sign-offs:

1. **Automated CI/CD Scan**: SonarQube rules check that no plaintext PII fields are exposed in console log lines or stored in temporary data schemas.
2. **Legal & Compliance Review**: The Chief Compliance Officer must review and sign off on all text modifications in the KFS template or Consent notice screens.
3. **CISO Signature**: Penetration testing of API gateway token validation, mTLS certificates, and cryptographic key configurations must receive an A+ grade from the security team.

---

## 4. References & Linked Artifacts

* **Gap Analysis & Solutions**: [gap_analysis_and_solutions.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md)
* **Transition Architectures**: [transition_architectures.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md)
* **Change Management Governance**: [change_management_governance.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/change_management_governance.md)
* **SLAs and KPIs**: [slas_and_kpis.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/slas_and_kpis.md)
