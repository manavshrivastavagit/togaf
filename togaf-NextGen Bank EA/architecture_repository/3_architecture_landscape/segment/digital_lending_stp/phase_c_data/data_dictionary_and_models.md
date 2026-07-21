# Phase C: Data Architecture - Data Dictionary & Relational Models

This document specifies the relational database schema, data dictionary, and physical data models for the core tables driving the digital lending platform. The target database is PostgreSQL (version 15+).

---

## 1. CUSTOMER

Holds primary profile information for registered applicants. It does not store raw Aadhaar numbers; instead, it uses a pointer to a secure Aadhaar Vault.

### Schema Definition
```sql
CREATE TYPE customer_status AS ENUM ('PENDING_VERIFICATION', 'ACTIVE', 'SUSPENDED', 'BLOCKED');

CREATE TABLE CUSTOMER (
    cust_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    pan_mask VARCHAR(10) NOT NULL CHECK (pan_mask ~ '^[A-Z]{5}[0-9]{4}[A-Z]{1}$'),
    pan_hash VARCHAR(64) NOT NULL, -- SHA-256 hash of PAN for deduplication
    aadhaar_vault_ref UUID UNIQUE NOT NULL, -- Reference to Tokenized Vault (PII Compliant)
    full_name VARCHAR(150) NOT NULL,
    email VARCHAR(255) NOT NULL UNIQUE CHECK (email ~* '^[A-Za-z0-9._%-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,4}$'),
    phone VARCHAR(15) NOT NULL UNIQUE CHECK (phone ~ '^\+[1-9]\d{1,14}$'), -- E.164 format
    dob DATE NOT NULL,
    status customer_status NOT NULL DEFAULT 'PENDING_VERIFICATION',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_customer_pan_hash ON CUSTOMER (pan_hash);
CREATE INDEX idx_customer_phone ON CUSTOMER (phone);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `cust_id` | `UUID` | PRIMARY KEY | Unique identifier for each customer. |
| `pan_mask` | `VARCHAR(10)` | NOT NULL | Permanent Account Number (PAN) masked or verified representation. |
| `pan_hash` | `VARCHAR(64)` | NOT NULL, INDEX | Salted SHA-256 hash of the PAN for identity deduplication. |
| `aadhaar_vault_ref` | `UUID` | UNIQUE, NOT NULL | Tokenized pointer to the secure Aadhaar Vault matching UIDAI compliance. |
| `full_name` | `VARCHAR(150)` | NOT NULL | Customer's full name as per official identity documents. |
| `email` | `VARCHAR(255)` | UNIQUE, NOT NULL | Customer email address, validated via regex. |
| `phone` | `VARCHAR(15)` | UNIQUE, NOT NULL | E.164 formatted mobile phone number. |
| `dob` | `DATE` | NOT NULL | Date of Birth (used for age eligibility calculations). |
| `status` | `customer_status` | NOT NULL | Enum state of customer lifecycle (`PENDING_VERIFICATION`, `ACTIVE`, `SUSPENDED`, `BLOCKED`). |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | Timestamp of record creation in UTC. |
| `updated_at` | `TIMESTAMP WITH TZ` | NOT NULL | Timestamp of last modification in UTC. |

---

## 2. LOAN_APPLICATION

Captures the intent of a customer to apply for a loan, along with underwriting decisions and credit details.

### Schema Definition
```sql
CREATE TYPE application_status AS ENUM (
    'INITIATED', 'CONSENT_PENDING', 'UNDERWRITING', 'APPROVED', 'REJECTED', 'DISBURSED', 'CANCELLED'
);

CREATE TABLE LOAN_APPLICATION (
    application_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    cust_id UUID NOT NULL REFERENCES CUSTOMER (cust_id) ON DELETE RESTRICT,
    amount_requested NUMERIC(15, 2) NOT NULL CHECK (amount_requested > 0),
    amount_approved NUMERIC(15, 2) CHECK (amount_approved >= 0),
    interest_rate_offered NUMERIC(5, 2) CHECK (interest_rate_offered >= 0.00 AND interest_rate_offered <= 100.00),
    tenure_months INT NOT NULL CHECK (tenure_months BETWEEN 3 AND 120),
    underwriting_score INT CHECK (underwriting_score BETWEEN 300 AND 900), -- Credit score range
    status application_status NOT NULL DEFAULT 'INITIATED',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_loan_app_cust ON LOAN_APPLICATION (cust_id);
CREATE INDEX idx_loan_app_status ON LOAN_APPLICATION (status);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `application_id` | `UUID` | PRIMARY KEY | Unique identifier for the loan application. |
| `cust_id` | `UUID` | FOREIGN KEY, NOT NULL | References `CUSTOMER(cust_id)`. |
| `amount_requested` | `NUMERIC(15,2)`| NOT NULL | Total principal amount requested by the applicant. |
| `amount_approved` | `NUMERIC(15,2)`| NULL | Final approved principal amount after underwriting. |
| `interest_rate_offered`| `NUMERIC(5,2)` | NULL | Annual interest rate percentage offered. |
| `tenure_months` | `INT` | NOT NULL | Term of the loan in months (min 3, max 120). |
| `underwriting_score` | `INT` | NULL | Calculated internal or bureau underwriting score. |
| `status` | `application_status`| NOT NULL | Application state (`INITIATED`, `CONSENT_PENDING`, `UNDERWRITING`, etc.). |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | Timestamp when application was initiated. |
| `updated_at` | `TIMESTAMP WITH TZ` | NOT NULL | Last status or application detail update. |

---

## 3. CONSENT_LOG

Stores details of user consent fetched via the India Stack Account Aggregator (AA) network, complying with the Data Empowerment and Protection Architecture (DEPA).

### Schema Definition
```sql
CREATE TYPE consent_status AS ENUM ('INITIATED', 'ACTIVE', 'REVOKED', 'EXPIRED');

CREATE TABLE CONSENT_LOG (
    consent_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    cust_id UUID NOT NULL REFERENCES CUSTOMER (cust_id) ON DELETE RESTRICT,
    aa_consent_handle VARCHAR(255) NOT NULL UNIQUE, -- AA transaction reference
    status consent_status NOT NULL DEFAULT 'INITIATED',
    consent_start TIMESTAMP WITH TIME ZONE NOT NULL,
    consent_expiry TIMESTAMP WITH TIME ZONE NOT NULL,
    data_life_expiry TIMESTAMP WITH TIME ZONE NOT NULL,
    signed_consent_artifact JSONB NOT NULL, -- Digital signature validated JSON artifact
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_consent_log_cust ON CONSENT_LOG (cust_id);
CREATE INDEX idx_consent_log_handle ON CONSENT_LOG (aa_consent_handle);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `consent_id` | `UUID` | PRIMARY KEY | Unique identifier for internal consent records. |
| `cust_id` | `UUID` | FOREIGN KEY, NOT NULL | References `CUSTOMER(cust_id)`. |
| `aa_consent_handle` | `VARCHAR(255)`| UNIQUE, NOT NULL | Consent identifier generated by the Account Aggregator (AA). |
| `status` | `consent_status` | NOT NULL | Consent state (`INITIATED`, `ACTIVE`, `REVOKED`, `EXPIRED`). |
| `consent_start` | `TIMESTAMP WITH TZ`| NOT NULL | Timestamp when the consent validity period starts. |
| `consent_expiry` | `TIMESTAMP WITH TZ`| NOT NULL | Timestamp when consent for fetching data expires. |
| `data_life_expiry` | `TIMESTAMP WITH TZ`| NOT NULL | Maximum time limit for holding fetched financial data (purging deadline). |
| `signed_consent_artifact`| `JSONB` | NOT NULL | Complete cryptographically signed consent JSON from AA. |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | Internal timestamp of consent log initialization. |
| `updated_at` | `TIMESTAMP WITH TZ` | NOT NULL | Internal timestamp of last consent update. |

---

## 4. LOAN_ACCOUNT

Tracks disbursed loans, outstanding balances, payment terms, and lifecycle status.

### Schema Definition
```sql
CREATE TYPE loan_account_status AS ENUM ('ACTIVE', 'DELINQUENT', 'CLOSED', 'WRITTEN_OFF');

CREATE TABLE LOAN_ACCOUNT (
    loan_account_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    application_id UUID NOT NULL UNIQUE REFERENCES LOAN_APPLICATION (application_id) ON DELETE RESTRICT,
    cust_id UUID NOT NULL REFERENCES CUSTOMER (cust_id) ON DELETE RESTRICT,
    principal_amount NUMERIC(15, 2) NOT NULL CHECK (principal_amount > 0),
    current_outstanding NUMERIC(15, 2) NOT NULL CHECK (current_outstanding >= 0),
    interest_rate NUMERIC(5, 2) NOT NULL CHECK (interest_rate >= 0.00 AND interest_rate <= 100.00),
    tenure_months INT NOT NULL CHECK (tenure_months > 0),
    disbursement_date TIMESTAMP WITH TIME ZONE,
    status loan_account_status NOT NULL DEFAULT 'ACTIVE',
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_loan_acc_cust ON LOAN_ACCOUNT (cust_id);
CREATE INDEX idx_loan_acc_status ON LOAN_ACCOUNT (status);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `loan_account_id` | `UUID` | PRIMARY KEY | Unique identifier for the active loan account. |
| `application_id` | `UUID` | UNIQUE, FOREIGN KEY, NOT NULL | References `LOAN_APPLICATION(application_id)`. |
| `cust_id` | `UUID` | FOREIGN KEY, NOT NULL | References `CUSTOMER(cust_id)`. |
| `principal_amount` | `NUMERIC(15,2)`| NOT NULL | Disbursed principal amount. |
| `current_outstanding`| `NUMERIC(15,2)`| NOT NULL | Total remaining unpaid amount (principal + accrued interest). |
| `interest_rate` | `NUMERIC(5,2)` | NOT NULL | Active annual interest rate percentage. |
| `tenure_months` | `INT` | NOT NULL | Active repayment period length in months. |
| `disbursement_date` | `TIMESTAMP WITH TZ`| NULL | UTC timestamp when loan funds were transferred. |
| `status` | `loan_account_status`| NOT NULL | Status of loan account (`ACTIVE`, `DELINQUENT`, `CLOSED`, `WRITTEN_OFF`). |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | Timestamp of record creation. |
| `updated_at` | `TIMESTAMP WITH TZ` | NOT NULL | Timestamp of last modification. |

---

## 5. LOAN_LEDGER

The double-entry ledger tracking all financial transactions (disbursement, repayments, interest accruals, waivers) for auditing and compliance.

### Schema Definition
```sql
CREATE TYPE ledger_entry_type AS ENUM ('DISBURSEMENT', 'REPAYMENT', 'INTEREST_ACCRUAL', 'LATE_FEE', 'WAIVER');
CREATE TYPE ledger_status AS ENUM ('PENDING', 'POSTED', 'FAILED');

CREATE TABLE LOAN_LEDGER (
    ledger_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    loan_account_id UUID NOT NULL REFERENCES LOAN_ACCOUNT (loan_account_id) ON DELETE RESTRICT,
    entry_type ledger_entry_type NOT NULL,
    amount NUMERIC(15, 2) NOT NULL, -- Negative for repayments, positive for disbursements/accruals
    balance_after NUMERIC(15, 2) NOT NULL CHECK (balance_after >= 0),
    txn_timestamp TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    narration VARCHAR(255) NOT NULL,
    status ledger_status NOT NULL DEFAULT 'PENDING',
    saga_correlation_id UUID NOT NULL, -- Tie transactions to Saga Orchestrator workflows
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_ledger_loan_acc ON LOAN_LEDGER (loan_account_id);
CREATE INDEX idx_ledger_saga ON LOAN_LEDGER (saga_correlation_id);
CREATE INDEX idx_ledger_timestamp ON LOAN_LEDGER (txn_timestamp DESC);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `ledger_id` | `UUID` | PRIMARY KEY | Unique identifier for the ledger entry. |
| `loan_account_id` | `UUID` | FOREIGN KEY, NOT NULL | References `LOAN_ACCOUNT(loan_account_id)`. |
| `entry_type` | `ledger_entry_type`| NOT NULL | Type of transaction (`DISBURSEMENT`, `REPAYMENT`, etc.). |
| `amount` | `NUMERIC(15,2)`| NOT NULL | Transaction value. Debit is negative; credit is positive. |
| `balance_after` | `NUMERIC(15,2)`| NOT NULL | Running balance of outstanding loan after application of transaction. |
| `txn_timestamp` | `TIMESTAMP WITH TZ`| NOT NULL | Time the transaction occurred. |
| `narration` | `VARCHAR(255)`| NOT NULL | Description of the entry (e.g., "eNACH Auto-debit May 2026"). |
| `status` | `ledger_status` | NOT NULL | Double-entry post verification status (`PENDING`, `POSTED`, `FAILED`). |
| `saga_correlation_id`| `UUID` | NOT NULL | Transaction correlation identifier for saga verification. |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | System recording timestamp. |

---

## 6. REPAYMENT_MANDATE

Stores payment authorization setups (e.g., eNACH, UPI AutoPay) used for automatic debit of EMIs.

### Schema Definition
```sql
CREATE TYPE mandate_type AS ENUM ('ENACH', 'UPI_AUTOPAY', 'SI_CARDS');
CREATE TYPE mandate_status AS ENUM ('PENDING_AUTH', 'ACTIVE', 'FAILED', 'REVOKED');

CREATE TABLE REPAYMENT_MANDATE (
    mandate_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    loan_account_id UUID NOT NULL REFERENCES LOAN_ACCOUNT (loan_account_id) ON DELETE RESTRICT,
    mandate_ref_no VARCHAR(100) NOT NULL UNIQUE, -- NPCI/Bank reference number
    mandate_type mandate_type NOT NULL,
    mandate_status mandate_status NOT NULL DEFAULT 'PENDING_AUTH',
    max_amount NUMERIC(15, 2) NOT NULL CHECK (max_amount > 0),
    bank_account_no VARCHAR(34) NOT NULL, -- Masked or encrypted
    bank_ifsc VARCHAR(11) NOT NULL CHECK (bank_ifsc ~ '^[A-Z]{4}0[A-Z0-9]{6}$'),
    created_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL,
    updated_at TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_mandate_loan_acc ON REPAYMENT_MANDATE (loan_account_id);
CREATE INDEX idx_mandate_ref ON REPAYMENT_MANDATE (mandate_ref_no);
```

### Data Dictionary

| Column Name | Data Type | Constraints | Description |
| :--- | :--- | :--- | :--- |
| `mandate_id` | `UUID` | PRIMARY KEY | Unique identifier for mandate entry. |
| `loan_account_id` | `UUID` | FOREIGN KEY, NOT NULL | References `LOAN_ACCOUNT(loan_account_id)`. |
| `mandate_ref_no` | `VARCHAR(100)`| UNIQUE, NOT NULL | NPCI UMRN (Unique Mandate Reference Number) or UPI mandate ID. |
| `mandate_type` | `mandate_type` | NOT NULL | Automated mandate execution system (`ENACH`, `UPI_AUTOPAY`, `SI_CARDS`). |
| `mandate_status` | `mandate_status`| NOT NULL | Status of mandate registration (`PENDING_AUTH`, `ACTIVE`, `FAILED`, `REVOKED`). |
| `max_amount` | `NUMERIC(15,2)`| NOT NULL | Maximum per-transaction debit authorization allowed. |
| `bank_account_no` | `VARCHAR(34)` | NOT NULL | Masked/encrypted target bank account number for auto-debit. |
| `bank_ifsc` | `VARCHAR(11)` | NOT NULL | IFSC of the target bank branch, verified using NPCI standards. |
| `created_at` | `TIMESTAMP WITH TZ` | NOT NULL | Mandate initiation timestamp. |
| `updated_at` | `TIMESTAMP WITH TZ` | NOT NULL | Last mandate modification timestamp. |
