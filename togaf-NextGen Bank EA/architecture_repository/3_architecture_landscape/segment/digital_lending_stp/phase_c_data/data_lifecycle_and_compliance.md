# Phase C: Data Architecture - Data Lifecycle and Compliance

This document defines the data lifecycle, storage policies, retention schedules, and purging mechanisms required to ensure compliance with the **Digital Personal Data Protection (DPDP) Act, 2023** (India) and standard financial regulations (RBI, FIU-IND).

---

## 1. DPDP Compliance Framework

Under the DPDP Act 2023, the platform behaves as a **Data Fiduciary**, and customers are **Data Principals**. Key operational mandates include:
1. **Purpose Limitation:** Customer personal data (specifically bank statements and KYC data) must only be processed for the specific purpose (loan underwriting) for which consent was explicitly granted.
2. **Right to Erasure (Right to Be Forgotten):** Once the purpose is served, or consent is withdrawn, or the data life expires, all associated data must be permanently deleted or anonymized unless a legal retention override applies.
3. **Data Minimization:** No excess PII can be stored post-underwriting decision except what is legally required to service active loans.

---

## 2. Retention Matrix

The table below defines data classifications and their respective retention policies.

| Data Category | Data Elements | Retention Period | Post-Retention Action | Legal Override / Justification |
| :--- | :--- | :--- | :--- | :--- |
| **Financial Ledger** | Ledger Entries, Repayments, Disbursements | 10 Years from Loan Closure | Archive to Cold Storage (S3 Glacier) | RBI Master Directions, Prevention of Money Laundering Act (PMLA) |
| **Active Loan Data** | Active Loan Details, Mandates, Outstanding | Lifetime of the Loan | Delete 6 months after loan closure | Loan servicing agreement contract fulfillment |
| **Consent Data** | Consent Logs, Signed Artifacts | 5 Years post-consent expiry | Purge completely | Regulatory evidence of compliance with consent frameworks |
| **Financial Statements (AA)** | Bank Account Statements, Transaction Lists | Underwriting period OR 90 days if loan is not disbursed | Complete Purging (Hard Delete) | DPDP Act (Purpose completed - no legal basis to store if loan is rejected/not taken) |
| **PII Data** | Full Name, Phone, Email, DOB, PAN Hash | 8 Years from customer inactivity / account closure | Cryptographic Anonymization | PMLA and KYC guidelines |
| **Aadhaar Reference** | Tokenized reference keys (UIDAI vault) | 8 Years from account closure | Delete token pointer | UIDAI Aadhaar Act compliance |

---

## 3. PII Archiving and Encryption Strategy

* **Storage Segregation:** All PII is stored in a isolated database schema (`pii_secured_schema`) with row-level security (RLS) enabled.
* **Encryption at Rest:** All PII data fields are encrypted using AES-256-GCM. The key is managed in AWS KMS with rotation enabled every 90 days.
* **Cold Archiving:** Archived ledger records are serialized to Parquet, encrypted via KMS keys, and pushed to Amazon S3 Glacier. Access to Glacier archives requires dual-authorization (M-of-N signature) from the Chief Risk Officer (CRO) and Chief Information Security Officer (CISO).

---

## 4. Purging Scripts & Automation

Purging is managed by a daily Cron Job executing a database stored procedure. The procedure handles two classes of data:
1. Expired AA Data (where `data_life_expiry` has passed and the application did not result in an active loan).
2. Customer deletion requests (for customers without active loans or legal disputes).

### PostgreSQL Stored Procedure for Automatic Data Purge

```sql
CREATE OR REPLACE PROCEDURE purge_expired_consent_data()
LANGUAGE plpgsql
AS $$
DECLARE
    deleted_consent_count INT := 0;
    deleted_underwrite_data_count INT := 0;
BEGIN
    RAISE NOTICE 'Starting expired data purging sequence...';

    -- 1. Identify and purge raw financial statement data extracted from Account Aggregators
    -- where the data life has expired and the loan is NOT active.
    -- (Creates a backup audit entry of the deletion event before purging)
    
    INSERT INTO audit_compliance_log (event_type, description, target_table, records_affected)
    SELECT 
        'AUTO_PURGE_AA_STATEMENTS',
        'Purging encrypted statement data for consent handle: ' || aa_consent_handle,
        'CONSENT_LOG',
        1
    FROM CONSENT_LOG
    WHERE data_life_expiry < CURRENT_TIMESTAMP 
      AND status = 'ACTIVE';

    -- 2. Clear out the cryptographic signed JSON payload (containing raw transactions) 
    -- and update state to EXPIRED
    WITH updated_consents AS (
        UPDATE CONSENT_LOG
        SET signed_consent_artifact = '{}'::jsonb, -- Purge payload content
            status = 'EXPIRED',
            updated_at = CURRENT_TIMESTAMP
        WHERE data_life_expiry < CURRENT_TIMESTAMP
          AND status = 'ACTIVE'
        RETURNING consent_id
    )
    SELECT count(*) INTO deleted_consent_count FROM updated_consents;

    -- 3. Delete raw bank statements cached during underwriting for loan applications
    -- that were rejected, cancelled, or initiated but never disbursed past 90 days.
    WITH deleted_statements AS (
        DELETE FROM raw_underwriting_data
        WHERE application_id IN (
            SELECT application_id 
            FROM LOAN_APPLICATION
            WHERE status IN ('REJECTED', 'CANCELLED', 'INITIATED')
              AND created_at < (CURRENT_TIMESTAMP - INTERVAL '90 days')
        )
        RETURNING application_id
    )
    SELECT count(*) INTO deleted_underwrite_data_count FROM deleted_statements;

    RAISE NOTICE 'Purging completed. Consents expired: %, Raw Statement entries deleted: %', 
                 deleted_consent_count, deleted_underwrite_data_count;
END;
$$;
```

### Audit Log Table Structure

This table records all compliance actions, including user consent revocations and automated purges, ensuring auditability for regulators.

```sql
CREATE TABLE audit_compliance_log (
    audit_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    event_type VARCHAR(50) NOT NULL, -- e.g., 'CONSENT_REVOCATION', 'AUTO_PURGE'
    description TEXT NOT NULL,
    target_table VARCHAR(50) NOT NULL,
    records_affected INT NOT NULL DEFAULT 0,
    performed_by VARCHAR(100) DEFAULT 'SYSTEM_CRON_JOB',
    timestamp TIMESTAMP WITH TIME ZONE DEFAULT CURRENT_TIMESTAMP NOT NULL
);

CREATE INDEX idx_audit_compliance_type ON audit_compliance_log (event_type);
```
