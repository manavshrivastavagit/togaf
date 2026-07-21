# TOGAF Phase A: Statement of Architecture Work

This document serves as the formal **Statement of Architecture Work** for the NextGen Bank **Straight-Through Processing (STP) Micro-Loan Mobile Platform**. It defines the business context, objectives, scope, constraints, and architecture plan, acting as a binding agreement between the NextGen Bank Architecture Board and the Digital Lending Unit (DLU).

---

## 1. Document Control & Sign-off

| Title | Name | Role | Date | Signature |
| :--- | :--- | :--- | :--- | :--- |
| **Sponsor** | Rajesh Mehta | Chief Executive Officer (CEO) | 2026-05-21 | *Signed (e-Sign)* |
| **Reviewer** | Dr. Arvinder Singh | Chief Technology Officer (CTO) | 2026-05-21 | *Signed (e-Sign)* |
| **Reviewer** | Sandeep Patel | Chief Risk Officer (CRO) | 2026-05-21 | *Signed (e-Sign)* |
| **Author** | Manav Shrivastava | Lead Enterprise Architect | 2026-05-21 | *Signed (e-Sign)* |

---

## 2. Project Context & Business Case

### 2.1 Problem Statement
Traditional retail lending processes at NextGen Bank require physical document submission, manual credit underwriting, and in-person verification, leading to approval turn-around times (TAT) of 3 to 7 business days. This process is:
* Inefficient and costly, yielding an average customer acquisition cost (CAC) of ₹2,500.
* Incompatible with the expectations of the digitally-native customer segment (Gen-Z and Millennials), who expect instant processing.
* Unable to scale to capture the rapidly growing micro-loan market (10k to 10 Lakh INR).

### 2.2 Project Objective
Establish a cloud-native, mobile-first lending platform that executes the entire loan lifecycle from customer onboarding to final loan closure with **100% automated straight-through processing (STP)** and zero manual operational touchpoints.
* **Target TAT**: < 5 minutes.
* **Target CAC**: < ₹75 (a 97% reduction).
* **Target Scale**: Up to 100,000 application assessments per day.

---

## 3. Scope of Work

### 3.1 In-Scope Components
1. **Digital Acquisition Frontend**: Responsive iOS/Android mobile client apps supporting identity verification, liveness checks, and consent triggers.
2. **Identity & KYC Orchestrator**: Real-time integration with India Stack (UIDAI Aadhaar e-KYC, DigiLocker, CDSL/NSDL PAN databases, and HyperVerge biometric liveness API).
3. **DEPA Consent Manager**: Middleware integration connecting to Account Aggregator (AA) networks for digital financial statement ingestion.
4. **Autonomous Underwriting Engine**: Python-based machine learning (XGBoost) scoring models, fraud scorecards, and credit bureau integrations.
5. **Decoupled Loan Management System (LMS)**: Apache Fineract double-entry ledger acting as the digital sub-ledger, with automated EOD sync to the core bank ledger.
6. **Payment Hub Connection**: Real-time IMPS/NEFT disbursal interface and NPCI auto-debit registration (UPI AutoPay/e-NACH).

### 3.2 Out-of-Scope Components
* Physical document management and branch-based loan applications.
* Credit card management and physical collateral management (secured lending).
* Direct changes to the Core Banking System (CBS) real-time ledger schema (to protect CBS stability).
* Non-regulated lending lines or peer-to-peer (P2P) lending models.

---

## 4. Architecture Project Plan & Milestones

The architectural design and implementation phases are organized into four parallel work packages spanning a 9-month delivery timeline.

```
Month 1       Month 2       Month 3       Month 4       Month 5       Month 6       Month 7       Month 8       Month 9
[─── WP-01: Onboarding Core (TA-1) ───]
              [─── WP-02: Underwriting & Bureau (TA-2) ───]
                            [─── WP-03: LMS Ledger & Payment Hub ───]
                                          [─── WP-04: DevSecOps & Audit (Target) ───]
```

### 4.1 Major Milestones & Deliverables

| Phase | Milestone Description | Target Date | ADM Phase | Deliverable |
| :--- | :--- | :--- | :--- | :--- |
| **M1** | Architecture Vision & SOW Approval | Month 1 | Phase A | Approved Statement of Architecture Work (this document). |
| **M2** | Baseline & Target Architecture Blueprints | Month 2 | Phase B, C, D | Complete Business, Data, Application, and Technology designs. |
| **M3** | Transition Architecture 1 (TA-1) Launch | Month 4 | Phase E | Digital KYC implemented; manual statement underwriting enabled. |
| **M4** | Transition Architecture 2 (TA-2) Launch | Month 6 | Phase E | Automated underwriting implemented with human override active. |
| **M5** | Full Target Architecture Production Rollout | Month 9 | Phase F & G | 100% automated STP enabled; regulatory compliance signed off. |

---

## 5. Architectural Constraints

To ensure compatibility with enterprise standards and regulatory requirements, the design must operate within the following boundaries:

### 5.1 Regulatory & Compliance Constraints
* **Data Residency**: All customer PII, financial statements, and ledger records must reside within servers physically located in India (RBI DLG & DPDP Act compliance).
* **Direct Fund Flow**: Third-party lending service providers (LSPs) must not touch customer funds. Funds must flow directly from the bank's pool account to the borrower's account.
* **Right to Erasure**: The data storage layer must support dynamic, audited purging of rejected customer records within 30 days of application denial.

### 5.2 Technical & Performance Constraints
* **Legacy Core Banking Latency**: Core Banking System (CBS) APIs have a latency of > 2.5 seconds and cannot support mobile traffic spikes. The lending platform must decoupled using a dedicated sub-ledger database (PostgreSQL Aurora) and sync asynchronously.
* **API Latency**: End-to-end processing of risk scorecards and fraud checks must take < 800ms.
* **Security Standards**: All internal microservice communication must use mTLS (Mutual TLS). Encryption of PII at-rest must rely on enveloped keys managed by an HSM.

### 5.3 Schedule & Budget Constraints
* **Timeline**: The platform must go live with Transition Architecture 1 within 120 days.
* **Resource Limit**: Budget is capped at ₹5 Crores for CAPEX (software licensing, infrastructure setup, cloud credits) and ₹1.5 Crores annual OPEX.

---

## 6. RACI Matrix (Roles & Responsibilities)

The following matrix maps key enterprise roles to the deliverables of the TOGAF Architecture Development Method (ADM) phases:

| ADM Phase / Deliverable | Board / Sponsor | Enterprise Architect | CTO / IT Lead | Chief Risk Officer | Chief Compliance | Security Lead (CISO) |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| **Phase A: Vision & SOW** | **A** | **R** | **C** | **C** | **C** | **I** |
| **Phase B: Business Architecture**| **I** | **R** | **C** | **A** | **C** | **I** |
| **Phase C: IS Architecture** | **I** | **R** | **A** | **I** | **C** | **C** |
| **Phase D: Tech Architecture** | **I** | **R** | **A** | **I** | **I** | **C** |
| **Phase E & F: Migration / Roadmap**| **A** | **R** | **R** | **C** | **C** | **I** |
| **Phase G: Compliance Audits** | **I** | **C** | **R** | **I** | **A** | **R** |
| **Phase H: Architecture Contract**| **A** | **R** | **R** | **I** | **C** | **C** |

> **R** = Responsible (does the work) | **A** = Accountable (final sign-off / answerable) | **C** = Consulted (inputs gathered) | **I** = Informed (updated on outcome)
