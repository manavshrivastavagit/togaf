# Segment Architecture: Digital Lending STP

This folder contains the complete suite of **Enterprise Architecture (EA)** blueprints and deliverables for NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform**.

The architecture conforms to the **TOGAF Standard (v10)** and details the baseline, target, gap analysis, migration roadmap, and governance parameters across all standard ADM phases.

---

## 🧭 Document Index & Navigation

### 1. Vision & Strategy (Phases Preliminary & A)
*   **[Statement of Architecture Work](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/statement_of_architecture_work.md)**: Formal scope, deliverables milestones, RACI matrix, and sponsor sign-off.
*   **[Preliminary & Phase A Vision](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/preliminary_and_phase_a_vision.md)**: Organizational scope, strategic objectives, stakeholder map, capability model, and trade-offs.
*   **[Stakeholder Communications Plan](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/stakeholder_communications_plan.md)**: Communications matrix, reporting formats, and escalation procedures.
*   **[Architecture Vision (Detailed)](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_a_vision/architecture_vision.md)**: System boundaries, context map, target domains, metrics, and risks.
*   **[Stakeholder Management Matrix](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_a_vision/stakeholder_management.md)**: Map, power/interest grids, and stakeholder engagement records.
*   **[Business Capability Model](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_a_vision/business_capabilities.md)**: Detailed L1/L2 capabilities and maturity assessment metrics.
*   **[Architecture Requirements Specification](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/architecture_requirements_specification.md)**: Functional/NFR requirements, regulatory mappings, and Requirements Traceability Matrix (RTM).

---

### 2. Business Architecture (Phase B)
*   **[Phase B Business Architecture](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_b_business_architecture.md)**: Actor roles, capability mapping, STP pipelines, and Business Building Blocks (BABBs).
*   **[BPMN and Process Flows](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/bpmn_and_process_flows.md)**: Swimlane diagrams for origination, EOD repayments, and exception collections.
*   **[Customer Journey and STP Screens](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_b_business/customer_journey_and_stp.md)**: UI layout mapping, liveness verification checks, exception routing, and drop-off persistence.
*   **[Business Processes Sequence Diagrams](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_b_business/business_processes.md)**: Sequential calls for e-KYC, consent fetch, scoring, e-Sign, and disbursals.
*   **[Business Building Blocks Matrix](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_b_business/business_building_blocks.md)**: Detailed BABBs descriptions and regulatory rules mapping.

---

### 3. Information Systems Architecture (Phase C)
*   **[Phase C Data Architecture](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_data_architecture.md)**: Schema overview, DEPA consent payloads, and data compliance policies.
*   **[Data Dictionary and Models](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_data/data_dictionary_and_models.md)**: PostgreSQL table structures, keys, constraints, and indexes.
*   **[DEPA Consent Payloads](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_data/depa_consent_architecture.md)**: Account Aggregator session key crypto and consent structures.
*   **[Data Lifecycle & Compliance](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_data/data_lifecycle_and_compliance.md)**: DPDP data retention policies and SQL purge scripts.
*   **[Phase C Application Architecture](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_application_architecture.md)**: Microservices layout, OpenAPI specifications, and integration resilience.
*   **[Microservices Portfolio](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_application/microservices_portfolio.md)**: Portfolio definitions, configuration parameters, and API routing schemas.
*   **[API OpenAPI 3.0 Specs](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_application/api_specifications.md)**: Swagger/YAML spec specifications for onboarding, consent, payments.
*   **[Resilience and Integration Patterns](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_c_application/resilience_and_patterns.md)**: Transactional outbox table schemas, Saga orchestration diagrams, and circuit breakers.
*   **[ABB to SBB Master Matrix](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/architecture_building_blocks.md)**: Logical Architecture Building Blocks mapped to physical Solution Building Blocks.

---

### 4. Technology Architecture (Phase D)
*   **[Phase D Technology Architecture](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_d_technology_architecture.md)**: Infrastructure topology, VPC networking, mTLS security, and Cloud HSM key wrapping policies.
*   **[Deployment Topology Specification](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_d_technology/deployment_topology.md)**: Managed EKS nodes, VPC subnets, and AWS Direct Connect leased line parameters.
*   **[Security Architecture & KMS](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_d_technology/security_architecture.md)**: OIDC with Keycloak/PKCE flows and AWS KMS policy definitions.
*   **[Fraud Defense & Biometrics](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_d_technology/fraud_defense_system.md)**: Device binding validation, geolocation checks, and mule account filters.

---

### 5. Migration & Planning (Phases E & F)
*   **[Phase E-F Migration Roadmap Overview](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration_roadmap.md)**: Consolidated gap analysis summary, roadmap, and repository compliance.
*   **[Gap Analysis and Solutions](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md)**: Detailed gap evaluations and buy-vs-build matrices.
*   **[Transition Architectures Description](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md)**: Phase gate details and flow charts for TA-1 and TA-2.
*   **[Migration Roadmap & Projects](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/migration_roadmap.md)**: Work package definitions (WP-01 to WP-04) and project schedules.
*   **[TCO Financial Model](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/tco_financial_model.md)**: Sizing charges, AWS infrastructure pricing, and CAPEX/OPEX vs traditional branch comparisons.

---

### 6. Governance & Compliance (Phases G & H)
*   **[Phase G-H Governance Overview](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance.md)**: Compliance metrics, change workflows, and operational SLAs.
*   **[Compliance Guidelines & RBI Audit](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/compliance_guidelines.md)**: DLG and DPDP audit checklists.
*   **[Architecture Contract](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/architecture_contract.md)**: Agreement defining compliance requirements and SLAs.
*   **[Change Management Governance](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/change_management_governance.md)**: RFC template, change board scope, and reviews.
*   **[SLAs and Prometheus KPIs](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/slas_and_kpis.md)**: Technical SLAs and dashboard metric maps.
