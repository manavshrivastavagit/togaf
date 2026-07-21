# TOGAF Preliminary Phase: Architecture Principles

This document defines and expands upon the core architectural principles that govern the design, construction, and evolution of NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform**. These principles are mandatory for all development teams, platform engineers, and security specialists.

---

## Principle 1: Straight-Through Processing First (STP-First)

### 1.1 Statement
The digital lending platform must execute the entire loan lifecycle—from customer acquisition and identity verification to risk underwriting, document signing, mandate registration, fund disbursal, and repayment processing—with 100% automated digital workflows and zero manual back-office tasks or human intervention.

### 1.2 Rationale
*   **Customer Experience**: The target demographic (Gen Z and Millennials) demands instant credit. Any manual queue or human verification introduces delays, leading to drop-offs.
*   **Operational Scalability**: Manual verification creates linear operational cost scaling. An automated, zero-touch process allows the bank to scale from 1,000 to 1,000,000 active loans without expanding the operations team.
*   **Consistency & Auditability**: System-driven logic removes human bias, fraud risks (e.g., collusion, manual override of risk policies), and operational errors.

### 1.3 Technology Implications
*   **Event-Driven Workflows**: The architecture must utilize a distributed workflow orchestrator (e.g., Temporal, Camunda, or AWS Step Functions) to manage long-running transactional states.
*   **Strict Outlier Rejection**: Application paths that fail automated validations (e.g., liveness checks or identity matching thresholds) must be routed to automated rejection or dynamic fallback screens, never to manual operations queues.
*   **Self-Healing Integrations**: All third-party integration points (bureau, e-KYC, payment networks) must implement automated retries, dynamic back-off, circuit breakers, and alternative fallbacks to survive partner system downtimes.
*   **Rule Engine Separation**: Credit scoring, fraud flags, and limits must be evaluated by a declarative business rule engine (e.g., Drools, JSON rules, or OPA) separated from the core microservice logic, allowing rapid policy updates.

### 1.4 Business Implications
*   **Role Transformation**: Operations staff shift from processing loan applications to auditing system performance, adjusting credit scorecards, and monitoring portfolio metrics.
*   **Product Simplification**: Loan products must be designed with simple rules, transparent terms, and standardized repayment models. Complex customized underwriting negotiations are deprecated.
*   **Real-Time Financial Reporting**: Financial reconciliation and End-of-Day (EOD) ledger reporting must be fully automated to support continuous transaction volumes.

---

## Principle 2: API-First & Interoperable Ecosystem

### 2.1 Statement
All platform capabilities must be built as independent, modular microservices that communicate exclusively via versioned, secure APIs (REST, gRPC, or GraphQL). External integration points must leverage standardized open APIs to participate seamlessly in the India Stack (Aadhaar, DigiLocker, NPCI, Account Aggregator, NeSL).

### 2.2 Rationale
*   **Rapid Integration**: The modern digital finance ecosystem relies heavily on third-party fintech distribution channels, credit data providers, and regulatory interfaces. Standardized APIs minimize partner onboarding times.
*   **Decoupling & Agility**: By avoiding direct database links or monolithic code bases, independent stream-aligned teams can build, test, and deploy services without coordinating global releases.
*   **Infrastructure Adaptability**: APIs isolate core banking systems (CBS) from high-volume mobile customer traffic, protecting legacy ledgers from transaction spikes.

### 2.3 Technology Implications
*   **Design-First Contracts**: API specifications (OpenAPI 3.0 or Protobuf files) must be drafted, reviewed, and approved before writing code. These contracts serve as mock environments for frontend and partner development.
*   **API Gateway & Security**: All API traffic must route through a centralized API Gateway (e.g., Kong, Apigee) which enforces rate limiting, routing, SSL termination, and OAuth2 token validation.
*   **Strict Database Isolation**: Direct database access across microservice boundaries is prohibited. Services must expose APIs or publish messages to shared message brokers (Kafka/RabbitMQ) for data sharing.
*   **Version Control**: APIs must adhere to Semantic Versioning (SemVer) guidelines. Legacy versions of APIs must remain supported for a minimum transition period (e.g., 90 days) with deprecated headers exposed.

### 2.4 Business Implications
*   **Ecosystem Monetization**: The bank can expose its digital lending capabilities as APIs to external partners (e.g., e-commerce checkouts, fintech aggregators) for Embedded Finance opportunities.
*   **Reduced Vendor Lock-In**: Standardized APIs enable swapping out vendors (e.g., shifting from one credit score provider to another) with minimal code changes.
*   **Time-to-Market**: New features and partner integrations can be released in days rather than months.

---

## Principle 3: Compliance & Privacy by Design (Security/DPDP/DLG)

### 3.1 Statement
Data security, customer privacy, and regulatory compliance (specifically the Digital Personal Data Protection Act (DPDP) and the RBI Digital Lending Guidelines (DLG)) must be integrated as core, non-negotiable architectural requirements from inception, rather than treated as post-development auditing checks.

### 3.2 Rationale
*   **Regulatory Penalty Risk**: Non-compliance with RBI digital lending circulars or DPDP data handling provisions exposes the bank to heavy fines, class-action lawsuits, and suspension of operational licenses.
*   **Customer Trust**: Young consumers are highly sensitive to data misuse, spam communications, and security breaches. Building transparent privacy controls fosters brand loyalty.
*   **Zero-Trust Security**: Standardizing security at the perimeter is insufficient. Inside the platform, all nodes, services, and transactions must verify credentials, permissions, and consent tokens.

### 3.3 Technology Implications
*   **Cryptographically Logged Consent**: Customer consent must be explicit, granular, purpose-bound, and revocable. Consent states must be recorded in an immutable, cryptographically chained audit log (Consent Registry).
*   **PII Encryption & Tokenization**: Personally Identifiable Information (PII) must be encrypted at rest (using AES-256 with KMS envelope encryption), in transit (TLS 1.3), and in use. Credit card numbers, Aadhaar, and PAN must be tokenized, with raw values stored in restricted, isolated databases.
*   **Direct Fund Flow Compliance**: The payment hub must ensure that all fund transfers route directly from NextGen Bank's pool account to the verified borrower's bank account, completely bypassing any intermediary/LSP (Lending Service Provider) pool accounts.
*   **Automated Data Erasure**: System tasks must automatically purge user transactional data (gathered via Account Aggregators or bureaus) 30 days after application rejection or upon loan closure and consent revocation.

### 3.4 Business Implications
*   **Pricing Transparency**: A Key Fact Statement (KFS) containing APR, interest rates, processing fees, and charge breakdowns must be programmatically generated and displayed to the customer before signing.
*   **Consent Management Dashboard**: The mobile application must provide customers with a self-service panel to view, download, or revoke active data consent states.
*   **Auditable Operations**: The compliance officer must have access to automated audit trails proving that every data pull was supported by valid customer consent.

---

## Principle 4: Mobile-First & Dynamic Experience

### 4.1 Statement
The primary delivery channel is the mobile application. The mobile frontend, application APIs, and network protocols must be optimized for dynamic, low-latency, and fluid user experiences, even under constrained network conditions (2G/3G speeds) or on low-end mobile devices.

### 4.2 Rationale
*   **Demographic Alignment**: Target users live on mobile devices. Slow loads, complex forms, or screen freezes trigger instant app uninstalls and customer acquisition loss.
*   **Network Heterogeneity**: In Tier 2 and Tier 3 regions, network connectivity is highly variable. The platform must remain responsive and secure during intermittent connectivity drops.

### 4.3 Technology Implications
*   **Server-Driven UI (SDUI)**: Screen layouts, form fields, and step sequences must be controlled via JSON payloads returned from the backend, enabling the bank to update onboarding flows and offer screens instantly without waiting for App Store/Play Store updates.
*   **Payload Optimization**: Implement response compression (Brotli/Gzip), protocol optimization (gRPC/HTTP/2 for API gateway communication), and strict data minimization (do not fetch fields unused by the UI).
*   **Progressive Web Apps (PWA) / Hybrid Architectures**: Optimize state machines to cache non-sensitive configuration data (e.g., list of banks, state directories) locally in Secure Storage.
*   **Asynchronous UX Actions**: High-latency actions (such as underwriting scores and bureau fetches) must use asynchronous polling, WebSockets, or push notifications, replacing static blocking loaders with dynamic progress screens.

### 4.4 Business Implications
*   **Higher Funnel Conversion**: A seamless, fast mobile interface reduces onboarding drop-off rates and lowers the Customer Acquisition Cost (CAC).
*   **Inclusive Reach**: Optimizations enable NextGen Bank to acquire credit-worthy customers in rural areas with poor connectivity.
*   **Rapid UI Experiments**: Product managers can run A/B tests on UI screens by editing server-side configurations without submitting new app builds to stores.
