# TOGAF Class: Standards Information Base (SIB)

The **Standards Information Base (SIB)** defines the external regulatory standards, internal design policies, and technology standards with which all system architectures must comply.

---

## 1. Regulatory & Statutory Standards

All digital solutions targeting customer onboarding, transaction ledgering, or data storage must conform to these frameworks:

*   **RBI Digital Lending Guidelines (DLG)**:
    - *Directive*: All loan disbursals and repayments must execute directly between the bank's pool account and the borrower's bank account, with zero pass-through to third-party pool accounts.
    - *Impact*: Direct integration with Sponsor Banks and IMPS/UPI/UPI Auto-Pay is mandatory.
*   **Digital Personal Data Protection (DPDP) Act 2023**:
    - *Directive*: Customer data must only be retrieved under active, explicit, and granular consent, and must be purged once the purpose of collection is completed.
    - *Impact*: Transient underwriting bank statements fetched via Account Aggregator must be purged 30 days post loan-evaluation.
*   **DEPA & ReBIT Specification**:
    - *Directive*: Standardized financial data sharing framework.
    - *Impact*: All consent manager integrations must conform to the ReBIT schema guidelines.

---

## 2. Security & Cryptographic Standards

*   **Identity & Access Control**: OAuth 2.0 with PKCE (Proof Key for Code Exchange) is mandatory for all mobile/client channel authentications.
*   **Database Encryption**: AES-256 encryption at rest. Customer PAN, Aadhaar, and cell numbers must be tokenized at edge ingress.
*   **Network Security**: TLS 1.3 for all public entrypoints; strict mutual TLS (mTLS) via service mesh (Istio) for all service-to-service calls.
*   **Key Custody**: Cryptographic keys must reside inside a Hardware Security Module (HSM) or cloud equivalent (AWS CloudHSM).

---

## 3. Engineering & Technical Standards

*   **API Specification**: OpenAPI Specification (OAS) 3.0 in YAML for REST APIs.
*   **Internal RPC**: gRPC/Protobuf for synchronous inter-service communication.
*   **Message Broker Payload**: Standard JSON structure with metadata header (traceID, timestamp, producer) and payload body for Kafka event streams.
