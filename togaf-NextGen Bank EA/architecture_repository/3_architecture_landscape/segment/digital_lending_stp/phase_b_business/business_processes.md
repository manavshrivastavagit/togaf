# TOGAF Phase B: Straight-Through Processing Business Workflows

This document provides a detailed specification of the six core **Straight-Through Processing (STP) Workflows** that automate the entire lending lifecycle. Each workflow describes the sequence of API interactions, business validation rules, and system behavior.

---

## 1. Identity Verification & KYC Process

This process validates the borrower's identity and performs regulatory Know-Your-Customer checks using Aadhaar e-KYC, NSDL PAN verification, and video face matching.

```mermaid
sequenceDiagram
    autonumber
    actor Customer
    participant App as Mobile App
    participant OS as Onboarding Service
    participant NSDL as NSDL PAN API
    participant UIDAI as UIDAI e-KYC API
    
    Customer->>App: Input PAN & Aadhaar Number
    App->>OS: Submit Registration Details
    OS->>NSDL: Fetch PAN Profile Data
    NSDL-->>OS: Return PAN Status, Full Name, DOB
    OS->>OS: Validate PAN is Active & matches Name input
    OS->>UIDAI: Request e-KYC OTP
    UIDAI-->>Customer: Send SMS OTP
    Customer->>App: Input Aadhaar OTP
    App->>OS: Submit Aadhaar OTP
    OS->>UIDAI: Verify OTP & Request Aadhaar XML
    UIDAI-->>OS: Return Aadhaar Profile (Name, Photo, Address, DOB)
    OS->>OS: Compute Jaro-Winkler Distance (PAN Name vs. Aadhaar Name)
    OS-->>App: Return Identity Verification Success
```

### Key Business Rules & Checks:
*   **PAN Validity**: The PAN status returned by NSDL must be active. Deceased or inactive PAN entries trigger immediate rejection.
*   **Name Matching (Jaro-Winkler)**: Because spelling variations occur between PAN and Aadhaar, the system calculates a name match confidence score. If the Jaro-Winkler distance is **< 0.85**, the application is routed to automated rejection.
*   **Age Restriction**: System validates that the date of birth (DOB) returned by Aadhaar confirms the customer's age is between 18 and 35.

---

## 2. Account Aggregator (AA) Consent & Financial Fetch

This process orchestrates the consent-driven collection of the customer's historical bank statements in compliance with the RBI Data Empowerment and Protection Architecture (DEPA) framework.

```mermaid
sequenceDiagram
    autonumber
    actor Customer
    participant App as Mobile App
    participant CS as Consent Service
    participant AA as Account Aggregator Portal
    participant FIP as Financial Information Provider (Bank)
    
    Customer->>App: Select Bank & Request AA Consent
    App->>CS: Register Consent Request
    CS->>AA: Submit Consent Spec (Purpose: Underwriting, Validity: 30 days)
    AA-->>App: Redirect User to AA Webview
    Customer->>AA: Log in & Approve Consent via OTP
    AA->>CS: Send Consent Approved Token
    CS->>AA: Fetch Encrypted Financial Data
    AA->>FIP: Retrieve Bank Statements
    FIP-->>AA: Deliver Decrypted Data
    AA-->>CS: Transfer Financial Payload (XML/JSON)
    CS->>CS: Decrypt Payload & Trigger Parse Engine
```

### Technical Workflow Details:
1.  **Consent Spec**: The request specifies a strict data-use scope: Bank Statements for the last 6 months. Data fetch is defined as a one-time pull.
2.  **Encryption**: FIP data is encrypted end-to-end using a dynamic key pair. The Account Aggregator acts as a router; it cannot decrypt or view the payload. The decryption key resides exclusively inside NextGen Bank's **Consent Service**.
3.  **Parsing Engine**: Converts raw transaction XML/JSON schemas from various banks into a standardized transaction model (dates, amounts, narrative tokens).

---

## 3. Bureau Scraping & Credit Scorecard Evaluation

This process retrieves credit history from authorized bureaus and executes the underwriting model to approve a credit limit.

```mermaid
sequenceDiagram
    autonumber
    participant OS as Onboarding Service
    participant RS as Risk Engine
    participant Bureau as CIBIL / Experian
    participant DB as Underwriting DB
    
    OS->>RS: Trigger Underwriting (User ID)
    RS->>Bureau: Request Credit Report (PAN, Aadhaar Details)
    Bureau-->>RS: Return Credit Report XML
    RS->>RS: Parse Bureau Tradelines (Active loans, defaults, DPD)
    RS->>RS: Fetch Parsed Bank Transactions
    RS->>RS: Execute Scoring Rules & Decision Scorecard
    RS->>DB: Log Scorecard Run & Decision Records
    RS-->>OS: Return Credit Offer (Approved Limit, Interest Rate)
```

### Underwriting Scorecard Rules:
*   **Bureau Score Filter**: Minimum CIBIL score must be **>= 650**. Customers with lower scores are automatically rejected.
*   **Days Past Due (DPD) Check**: No trade-line can display a DPD value **> 30** within the past 12 months.
*   **Income Verification**: Automated transaction analyzer calculates the average monthly income based on salary salary narratives or consistent deposits.
*   **Debt Service Coverage Ratio (DSCR)**: The calculated monthly EMI for the approved loan limit must not exceed **45%** of the estimated monthly income.

---

## 4. Repayment Mandate Registration (Auto-Debit)

To ensure low credit losses, the loan cannot be disbursed until a binding auto-repayment mandate is registered with the National Payments Corporation of India (NPCI).

```mermaid
sequenceDiagram
    autonumber
    actor Customer
    participant App as Mobile App
    participant LMS as Loan Mgmt System
    participant NPCI as NPCI / UPI Gateway
    participant PaymentApp as UPI Payment App
    
    LMS->>NPCI: Register UPI AutoPay Mandate Request
    NPCI-->>App: Return Deep-Link URI
    App->>PaymentApp: Open Payment App (GPay / PhonePe)
    Customer->>PaymentApp: Enter UPI PIN to Authorize Mandate
    PaymentApp->>NPCI: Confirm Mandate Registration
    NPCI->>LMS: Webhook: Mandate Active (URN Issued)
    LMS->>LMS: Link URN to Loan Account
```

### Mandate Rules:
*   **Mandate Limit**: The mandate is registered for an amount equal to the maximum monthly EMI (plus a 10% safety buffer for late charges).
*   **Bank Account Match**: The bank account registered for the mandate must match the destination bank account verified during the onboarding process.
*   **Alternative Flow**: If UPI AutoPay fails, the system renders an e-NACH registration screen requiring NetBanking or Debit Card OTP authentication.

---

## 5. Loan Agreement Assembly & Aadhaar e-Sign

This process generates the legal contract, displays it to the customer, and registers a digitally signed version with national vaults.

### Workflow Steps:
1.  **Contract Assembly**: The **Loan Management System (LMS)** fetches the customer profile (name, address, PAN), loan parameters (amount, interest, tenure, APR), and Key Fact Statement (KFS) details. These are merged into a standardized PDF/A template.
2.  **e-Sign API Trigger**: The generated document is sent to an authorized e-Sign gateway provider (e.g., NSDL or CDSL).
3.  **Customer Authentication**: The app redirects the user to the secure e-Sign page where they enter their Aadhaar number and the mobile OTP.
4.  **Verification**: The gateway validates the Aadhaar signature against UIDAI databases, signs the PDF, and returns the digitally signed contract along with a cryptographic audit trail.
5.  **NeSL Registration**: The signed agreement is registered with National E-Governance Services Limited (NeSL) as legal evidence of the debt.

---

## 6. Automated Fund Disbursal Release

The final step releases the loan funds directly to the customer's bank account. This is executed only after all validation checks have passed.

```mermaid
flowchart TD
    Start([Disbursal Triggered]) --> Check1{Is e-Sign Valid & NeSL Registered?}
    Check1 -- Yes --> Check2{Is AutoPay Mandate Active?}
    Check2 -- Yes --> Penny{Execute Penny Drop Verification}
    Penny -- Success --> Disburse[Trigger IMPS / UPI Disbursal API]
    Disburse -- Tx Success --> Ledger[Activate Loan & Ledger Account]
    Ledger --> Notify[Send SMS & WhatsApp Confirmation]
    
    Check1 -- No --> Fail([Hold & Flag Exception])
    Check2 -- No --> Fail
    Penny -- Fail --> Fail
```

### Disbursal Checks:
*   **Penny Drop Verification**: A small amount (e.g., 1 INR) is transferred to the destination bank account. The API returns the beneficiary name registered at the bank. The system matches this beneficiary name against the Aadhaar/PAN verified name. If the name match score is below 90%, disbursal is halted.
*   **Payment Hub Routing**: Disbursal is routed through NextGen Bank’s real-time payment hub. High-priority routing utilizes **IMPS** (Immediate Payment Service) or **UPI** for sub-second settlement.
*   **Ledger Activation**: Upon receiving a successful transaction callback from the payment hub, the loan status is updated to `ACTIVE` in the lending ledger database, and the repayment schedule is activated.
