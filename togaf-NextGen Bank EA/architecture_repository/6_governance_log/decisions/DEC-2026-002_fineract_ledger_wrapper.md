# Architecture Board Decision: DEC-2026-002

Selection of **Apache Fineract** as the core lending ledger engine.

---

## 1. Metadata & Control

| Field | Details |
| :--- | :--- |
| **Decision ID** | DEC-2026-002 |
| **Title** | Selection of Apache Fineract as Ledger Foundation |
| **Subject** | Ledger buy-vs-build analysis |
| **Date** | 2026-05-12 |
| **Status** | **Approved** |
| **Impact Level** | High (Drives core calculation engine and billing schemas) |

---

## 2. Context & Problem Statement

The Micro-Loan platform requires a sub-ledger system to calculate interest rates, penal charges, amortizations, and balance tracking with high banking precision. The Board evaluated whether to build a custom ledger engine or wrap/re-use an existing platform.

---

## 3. Options Considered

| Option | Pros | Cons | Board Evaluation |
| :--- | :--- | :--- | :--- |
| **Option A: In-House Build** (Go/SQL) | 100% custom control; minimal code footprints. | Extremely high risk of interest calculation rounding bugs; long development time (4+ months). | *Rejected* due to timeline and financial audit risks. |
| **Option B: Apache Fineract Wrapper** (Open Source) | Out-of-the-box support for amortization schemas; proven compliance; active developer community. | Java footprint; bloated schemas containing features we do not use (e.g. physical branch teller modules). | **Selected Option**. The board approved wrapping Fineract inside a clean Spring Boot microservice facade, disabling unused features. |
| **Option C: SaaS Vendor Core** (Mambu / Thought Machine) | Zero operational hosting overhead. | Exorbitant licensing costs per active loan account; high integration latency. | *Rejected* due to TCO model mismatch. |

---

## 4. Implications & Follow-up Actions

1.  **Wrapper Architecture**: Define a clean Spring Boot API wrapper (`go-ledger-facade`) exposing simplified REST endpoints, shielding internal Fineract database structures.
2.  **Hosting footprint**: Deploy Fineract core inside the dedicated AWS EKS cluster, backing it with an Aurora PostgreSQL instance.
3.  **CBS Sync**: Setup EOD transactional batch reconciliations to synchronize daily balance totals from the Fineract ledger to the bank's core systems.

---

## 5. Board Approvers (Consensus Reached)
*   **Chief Enterprise Architect** (Chairperson) - *Approved*
*   **Chief Technology Officer (CTO)** - *Approved*
*   **Principal Data Architect** - *Approved*
*   **Head of Digital Lending (Business Sponsor)** - *Approved*
