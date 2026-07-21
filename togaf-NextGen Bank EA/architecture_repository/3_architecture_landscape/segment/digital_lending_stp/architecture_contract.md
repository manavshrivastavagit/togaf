# TOGAF Phase G: Architecture Contract

This document establishes the **Architecture Contract** between the **NextGen Bank Architecture Board** and the **Digital Lending Unit (DLU) Implementation Teams** (Mobile App, Platform Engineering, Credit Underwriting, and Ledger Core). It defines the criteria, assessment procedures, and waiver processes to ensure the straight-through processing (STP) micro-loan platform is built and operated in strict conformance with the approved target architecture.

---

## 1. Scope & Contracting Parties

This contract applies to all software development, deployment, security auditing, and operational management activities related to the **Micro-Loan Mobile Platform**.

The contracting parties are:
* **The Architecture Board**: Represented by the Lead Enterprise Architect and Chief Technology Officer. Accountable for assessing architecture conformance and approving waivers.
* **The Implementation Teams**: Represented by the Digital Lending Unit (DLU) Delivery Lead and Technical Leads for Mobile, Platform, Underwriting, and Ledger teams. Responsible for implementing the Solution Building Blocks (SBBs) in conformance with this contract.

---

## 2. Architectural Conformance Criteria

The implementation must conform to the following architectural rules. Deviations without an approved waiver will block deployment to production environments.

### 2.1 Service Decoupling & API Gateway Routing
* All external customer requests must route through the **Kong API Gateway**. Direct exposure of internal microservices (Onboarding, Underwriting, LMS, Payments) to the public internet is prohibited.
* Direct database sharing or cross-database queries between microservices is prohibited. Inter-service data sharing must rely on REST APIs, gRPC, or Apache Kafka events.

### 2.2 Security & Data Privacy
* **mTLS (Mutual TLS)**: Enforced by the Istio service mesh, mTLS is mandatory for all network traffic between internal microservices. Plaintext HTTP communication within the cluster is blocked.
* **PII Encryption**: Restricted personal data (PII) must be encrypted at the database cell level using enveloped data encryption keys (DEKs) wrapped by keys managed in the Cloud HSM. Database logs or dumps must never store plaintext PII.
* **Device Binding**: All API requests from the mobile client must include a cryptographic device signature bound to the user's active session.

### 2.3 Financial Operations (Ledger Integration)
* Direct write operations to the Core Banking System (CBS) from the mobile client or frontend microservices are prohibited.
* The digital ledger (LMS Apache Fineract) must serve as the primary sub-ledger. Aggregated accounting entries must be synced asynchronously to CBS via daily end-of-day (EOD) batch pipelines using transactional outbox events.

---

## 3. Conformance Assessment Process

To ensure conformance is measured throughout the software development lifecycle (SDLC), the following checks are enforced:

### 3.1 Automated Pipeline Checks (Continuous Integration)
* **Code Scans**: CI/CD pipelines run automated SonarQube quality gates. Code failing vulnerability checks (e.g., hardcoded credentials, SQL injection risks) is auto-rejected.
* **Container Audits**: Container image scanning (Trivy) is executed for every build. Base images containing critical vulnerabilities (CVEs) fail the build.

### 3.2 Architecture Reviews (Milestone-based)
* A formal **Architecture Conformance Review** must be conducted prior to the launch of each Transition Architecture (TA-1 and TA-2) and the final target state.
* The review will be performed by the Lead Enterprise Architect using the Architecture Review Checklist.

---

## 4. Architecture Review Checklist

Implementation leads must provide evidence of conformance for each checklist item prior to production sign-off.

| Check ID | Architectural Directive | Target Metric / Evidence Required | Conformance (Yes/No) | Reviewer Signature |
| :--- | :--- | :--- | :--- | :--- |
| **CK-SEC-01** | Are all customer PII fields encrypted at rest using enveloped KMS keys? | Encryption code check; database schema dump showing ciphertext fields. | | |
| **CK-SEC-02** | Is inter-service communication secured via mTLS? | Istio configuration audit verifying peer authentication mode set to STRICT. | | |
| **CK-SEC-03** | Are application logs verified to contain zero customer PII? | Log scanner output verifying no phone, Aadhaar, PAN, or name leaks. | | |
| **CK-API-01** | Are all public API endpoints routed through the Kong API Gateway? | DNS and routing table configs showing only gateway IP in public subnet. | | |
| **CK-PAY-01** | Are disbursal destination accounts validated against verified e-KYC names? | Payment Hub code verification showing destination name check. | | |
| **CK-REG-01** | Does the system feature a 3-day penalty-free cooling-off closure API? | LMS loan lifecycle code audit; test case verifying zero-penalty payoff. | | |
| **CK-DATA-01**| Is rejected customer data permanently purged within 30 days of application denial? | Purge script code audit; database retention cron logs. | | |

---

## 5. Architecture Waiver Process

In situations where technical debt, partner dependencies, or extreme schedule pressure prevents conformance, teams must submit an **Architecture Waiver Request**.

### 5.1 Waiver Criteria
* **Temporary Waiver**: Granted for a limited time (max 180 days) when an implementation detail deviates from target architecture but does not introduce critical security risks. A clear remediation plan is required.
* **Permanent Waiver**: Granted only under exceptional circumstances when target architecture guidelines cannot be met due to hardware/legacy constraints, and a secure alternative control is established.

### 5.2 Waiver Request & Review Workflow

```
[1. Submission] DLU Tech Lead submits Waiver Request detailing deviation, rationale, and impact.
                     │
                     ▼
[2. Impact Analysis] Enterprise Architect reviews security, financial, and regulatory impact.
                     │
                     ▼
[3. Evaluation] Architecture Board reviews request and remediation plan.
                     ├── Approved ──► [4a. Update Waiver Log & task.md]
                     └── Rejected ──► [4b. Escalate for Remediation / Block Deployment]
```

### 5.3 Escalation Path
* If a waiver is rejected by the Architecture Board, the DLU Lead may escalate to the CTO.
* If a waiver involving regulatory compliance (RBI DLG) or data security is rejected, it cannot be overridden, and deployment is blocked until conformance is achieved.

---

## 6. Signatories

By signing below, all parties agree to adhere to the directives of this contract and the associated review and waiver processes.

* **Rajesh Mehta** (Sponsor / CEO): *Signed (e-Sign)*
* **Dr. Arvinder Singh** (CTO): *Signed (e-Sign)*
* **Manav Shrivastava** (Lead Enterprise Architect): *Signed (e-Sign)*
* **DLU Delivery Lead**: ____________________
* **Mobile Tech Lead**: ____________________
* **Underwriting Tech Lead**: ____________________
* **Platform Tech Lead**: ____________________
