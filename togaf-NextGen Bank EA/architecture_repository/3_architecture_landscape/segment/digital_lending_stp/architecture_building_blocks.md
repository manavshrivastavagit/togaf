# TOGAF Architecture Building Blocks (ABB) & Solution Building Blocks (SBB) Mapping

In TOGAF, **Architecture Building Blocks (ABBs)** define the logical, vendor-neutral capabilities required, while **Solution Building Blocks (SBBs)** define the physical implementation components (software, products, custom code).

This document serves as the master matrix mapping logical ABBs to physical SBBs for the micro-loan platform.

---

## 1. Building Blocks Mapping Matrix

| Category | Logical Architecture Building Block (ABB) | Physical Solution Building Block (SBB) | Status | Reusability |
| :--- | :--- | :--- | :--- | :--- |
| **Business / App** | **ABB-ONB-01**: Identity & Liveness Orchestrator | **SBB-Go-Onboarding**: In-house Go microservice integrating UIDAI Aadhaar, PAN APIs, and HyperVerge Liveness SDK. | **New** | Specific to Digital Onboarding Unit. |
| **Business / App** | **ABB-CON-01**: Consent Manager (DEPA compliant) | **SBB-Node-Consent**: Custom Node.js microservice integrating Setu AA Gateway and Sahamati specification. | **New** | Can be reused for other digital deposit/credit products. |
| **Business / App** | **ABB-CRD-01**: Underwriting Engine | **SBB-Python-Risk**: Custom FastAPI microservice running XGBoost risk models, CIBIL API parser, and local rule configurations. | **New** | Core Credit Risk asset. |
| **Business / App** | **ABB-LCE-01**: Loan Ledger & Calculation Core | **SBB-Java-Fineract**: Customised wrapper around Apache Fineract (Open Source Core Banking Platform). | **Modified** | Reused from NextGen Bank’s microfinance division, modified for STP. |
| **Business / App** | **ABB-PAY-01**: Payment Hub | **SBB-Go-Payment**: Microservice connecting to Sponsor Bank Host-to-Host UPI/IMPS and Razorpay e-Mandate APIs. | **Reused** | Shared across NextGen Bank payments team. |
| **Security** | **ABB-SEC-01**: Identity & Access Management | **SBB-Keycloak**: Open-source Keycloak server configured with OAuth2 and OpenID Connect (OIDC). | **Reused** | Enterprise IAM component. |
| **Security** | **ABB-SEC-02**: Enveloped Data Encryption | **SBB-AWS-KMS-CloudHSM**: AWS Key Management Service backed by dedicated CloudHSM instances. | **Reused** | Shared bank-wide security infra. |
| **Infrastructure**| **ABB-INF-01**: Container Runtime Cluster | **SBB-AWS-EKS**: Managed Amazon Elastic Kubernetes Service (EKS) running Kubernetes v1.28+. | **New** | Dedicated cluster for Digital Lending. |
| **Infrastructure**| **ABB-INF-02**: Asynchronous Message Broker | **SBB-AWS-MSK**: Managed Amazon Streaming for Apache Kafka. | **New** | Event broker for lending services. |

---

## 2. Building Block Detailed Specifications

### 2.1 Identity & Liveness Orchestrator (ABB-ONB-01)
* **Objective**: Verifies consumer identities in real time while preventing identity theft or deepfake biometric spoofs.
* **Core Interfaces**:
  - `POST /identity/verify-pan`: Verifies PAN active status and retrieves name from income tax database.
  - `POST /identity/aadhaar-kyc`: Validates Aadhaar OTP and downloads XML signature.
  - `POST /identity/liveness-check`: Compares photo from Aadhaar against camera selfie video stream.
* **Implementation Target (SBB-Go-Onboarding)**:
  - Custom microservice written in Go.
  - Third-party SDK integration (HyperVerge/Onfido) for biometric liveness.
  - Interfacing with NSDL/CDSL for PAN checks.

### 2.2 Underwriting Engine (ABB-CRD-01)
* **Objective**: Evaluates credit applications, computes risk ratings, and prices loans without manual review.
* **Core Interfaces**:
  - `POST /risk/underwrite`: Receives consolidated customer variables and returns an approval status, credit limit, and APR tier.
  - `GET /risk/rules`: Administrative endpoint to fetch active rule parameters.
* **Implementation Target (SBB-Python-Risk)**:
  - FastAPI web server.
  - Pandas/Scikit-learn libraries for scoring execution.
  - Rules kept in JSON configuration files, enabling risk officers to change parameters (e.g., CIBIL threshold from 650 to 670) without redeploying code.

### 2.3 Loan Ledger & Calculation Core (ABB-LCE-01)
* **Objective**: Maintains interest accruals, processing fees, payment schedules, and principal/interest splits with banking precision.
* **Core Interfaces**:
  - `POST /ledger/account/create`: Creates a new loan account mapping to the customer profile.
  - `POST /ledger/account/{acc_num}/post-transaction`: Registers repayments or charge events.
  - `GET /ledger/account/{acc_num}/statement`: Returns billing and transaction history.
* **Implementation Target (SBB-Java-Fineract)**:
  - Spring Boot API wrapper.
  - Apache Fineract database schema hosted in Aurora PostgreSQL.
  - Custom Java utility classes for complex billing calculations (e.g., localized processing tax computations).
