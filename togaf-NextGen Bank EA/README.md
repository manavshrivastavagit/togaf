# NextGen Bank: Enterprise Architecture Repository
## Straight-Through Processing (STP) Micro-Loan Platform

Welcome to the Enterprise Architecture (EA) Repository for NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform** (loans up to 10 Lakh INR). 

This workspace is structured in compliance with the **TOGAF Standard (Version 10 / Standard ADM)**. All architectural blueprints, compliance charters, standards, and deliverable templates are cataloged in a formal TOGAF Architecture Repository structure.

---

## 🧭 Repository Map

The architecture repository is divided into six core classes under the [architecture_repository/](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/README.md) directory:

```
togaf/
├── README.md (This Landing Portal)
└── architecture_repository/
    ├── README.md (Master Repository Index)
    ├── 1_architecture_metamodel/
    │   └── architecture_principles.md (Core guiding principles)
    ├── 2_architecture_capability/
    │   └── governance_framework.md (Architecture Board charter)
    ├── 3_architecture_landscape/
    │   └── segment/
    │       └── digital_lending_stp/ (Active Micro-Loan Segment Architecture)
    ├── 4_standards_information_base/
    │   └── README.md (Regulatory & Technical standards list)
    ├── 5_reference_library/
    │   ├── templates/ (TOGAF Approved Deliverable Templates)
    │   └── README.md (Reusable patterns list)
    └── 6_governance_log/
        └── README.md (Waivers & Audits log indices)
```

---

## 🏛️ Digital Lending STP Segment Architecture

All phase deliverables (Phases A through H) detailing the mobile micro-loan platform are housed under the Segment Architecture:
*   **Access the Segment Index**: **[Digital Lending STP Segment Architecture](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/README.md)**

This includes:
- **Vision**: System boundaries, capability models, and scope definitions.
- **Business**: Customer origination sequences, e-KYC, underwriting flows, and BPMN models.
- **Data**: Database models, DEPA account aggregator consent payloads, and DPDP lifecycle purging.
- **Application**: Go/Node/FastAPI microservices portfolio, Swagger/OpenAPI 3.0 APIs, and Saga patterns.
- **Technology**: Kubernetes deployment topologies, KMS encryption, and liveness threat defense systems.
- **Roadmap**: Gap analysis, build-vs-buy evaluations, work packages, and transitions.
- **Governance**: RBI DLG audits, change control protocols, and operational KPIs.

---

## 📐 TOGAF Approved Deliverable Templates

For future projects, a library of nine reusable, professional Markdown templates conforming to the TOGAF Standard has been established:
*   **Access the Templates**: **[Reference Library Templates](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/README.md#1-togaf-approved-deliverable-templates)**

Templates included:
1.  [Architecture Principles](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_principles_template.md)
2.  [Statement of Architecture Work](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/statement_of_architecture_work_template.md)
3.  [Architecture Vision](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_vision_template.md)
4.  [Architecture Definition Document (ADD)](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_definition_document_template.md)
5.  [Architecture Requirements Specification](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_requirements_specification_template.md)
6.  [Transition Architecture & Migration Roadmap](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/transition_architecture_roadmap_template.md)
7.  [Architecture Contract](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_contract_template.md)
8.  [Architecture Waiver Request](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_waiver_request_template.md)
9.  [Compliance Assessment](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/compliance_assessment_template.md)
