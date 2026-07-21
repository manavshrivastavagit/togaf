# TOGAF 9 Certification Exam Study Guide & Repository Mapping

This guide serves as a study and compliance reference, mapping the **TOGAF 9 Certification Syllabus** (Part 1 and Part 2) directly to the design artifacts implemented in NextGen Bank's Straight-Through Processing (STP) Micro-Loan Platform repository.

---

## 🎓 TOGAF 9 Part 1 (Foundation) Syllabus Reference

The Part 1 exam consists of **40 multiple-choice questions** mapping to the following 11 core focus areas. Below is a summary of each focus area and how they are represented in this architecture repository:

### 1. Basic Concepts (3 Questions)
*   **Concepts**: Definitions of Architecture, the TOGAF standard, why an enterprise architecture is needed, and the role of an architect.
*   **Repository Example**: 
    - [README.md](../../README.md): Explains the setup of an enterprise architecture repository and its business value for scaling the digital lending platform.

### 2. Core Concepts (3 Questions)
*   **Concepts**: The Architecture Development Method (ADM) cycle, Architecture Deliverables, Architecture Artifacts, and Building Blocks.
*   **Repository Example**:
    - [Repository Master Index](../README.md): Classifies deliverables into TOGAF-compliant directories (Metamodel, Capability, Landscape, SIB, Reference Library, Governance Log).

### 3. Introduction to the ADM (3 Questions)
*   **Concepts**: The phases of the ADM (Preliminary through Phase H), the core objectives of each phase, and the role of Requirements Management.
*   **Repository Example**:
    - Interactive **Visual ADM Explorer** on the portal home page, which visually maps files in this codebase to each ADM phase.

### 4. The Enterprise Continuum and Tools (4 Questions)
*   **Concepts**: The Enterprise Continuum, the Architecture Continuum, the Solutions Continuum, and the Architecture Repository.
*   **Repository Example**:
    - [ArchiMate & EAM Models Index](archimate_models/README.md): Illustrates how architectural concepts are structured hierarchically from generic foundations to organization-specific segments.

### 5. ADM Phases (9 Questions)
*   **Concepts**: Detailed knowledge of the steps, inputs, and outputs of Preliminary Phase through Phase H.
*   **Repository Example**:
    - [Segment Overview](../3_architecture_landscape/segment/digital_lending_stp/README.md): Links the complete lifecycle outputs of the digital lending platform stage-by-stage.

### 6. ADM Guidelines and Techniques (6 Questions)
*   **Concepts**: Iterations, simplifying the ADM, business scenarios, risk management, and gap analysis.
*   **Repository Example**:
    - [Gap Analysis Matrix](../3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md): Details the gap analysis technique for mapping baseline systems to target cloud microservices.

### 7. Architecture Governance (4 Questions)
*   **Concepts**: The Architecture Board, Architecture Contracts, Compliance Assessments, and the Governance Log.
*   **Repository Example**:
    - [Governance Framework](../2_architecture_capability/governance_framework.md): Details the NextGen Bank Architecture Board charter and stage-gate process.
    - [Architecture Contract](../3_architecture_landscape/segment/digital_lending_stp/architecture_contract.md): Establishes the formal contract between the Architecture Board and the implementation teams.

### 8. Architecture Views, Viewpoints, and Stakeholders (2 Questions)
*   **Concepts**: Stakeholder management, system views, viewpoints, and the separation of concerns.
*   **Repository Example**:
    - [Stakeholder Power Grid](../3_architecture_landscape/segment/digital_lending_stp/phase_a_vision/stakeholder_management.md): Defines the stakeholder classification grid and communication channels.

### 9. Building Blocks (2 Questions)
*   **Concepts**: Architecture Building Blocks (ABBs) vs. Solution Building Blocks (SBBs), and the building block lifecycle.
*   **Repository Example**:
    - [Logical BABBs Catalog](../3_architecture_landscape/segment/digital_lending_stp/phase_b_business/business_building_blocks.md): Documents the business-focused building blocks for identity, underwriting, and disbursals.
    - [Building Blocks Matrix](../3_architecture_landscape/segment/digital_lending_stp/architecture_building_blocks.md): Formally maps ABBs to target SBBs (e.g. Keycloak, Temporal, AWS EKS).

### 10. ADM Deliverables (2 Questions)
*   **Concepts**: Key deliverables produced throughout the ADM (SOW, Architecture Vision, Architecture Definition Document, Roadmap).
*   **Repository Example**:
    - [Reference Library Templates Index](README.md#1-togaf-approved-deliverable-templates): Catalog of 9 standard deliverable templates available for new projects.

### 11. TOGAF Reference Models (2 Questions)
*   **Concepts**: The Technical Reference Model (TRM) and the Integrated Information Infrastructure Reference Model (III-RM).
*   **Repository Example**:
    - [Strategic Landscape Index](../3_architecture_landscape/strategic/README.md): Identifies standard banking reference models utilized by NextGen Bank.

---

## 👔 TOGAF 9 Part 2 (Certified) Syllabus Reference

The Part 2 examination consists of **8 scenario-based questions** assessing practical application of the ADM. Candidates are evaluated on their ability to analyze complex scenarios and select the best architectural decision.

The questions are drawn from the following 8 topic areas, mapped to the codebase:

### Scenario Area 1: Project Establishment (Preliminary, Phase A, Requirements Management)
*   **Objective**: Setting up the scope, defining governance constraints, identifying stakeholders, and drafting initial statements of work.
*   **Repository Alignment**:
    - [Statement of Work (SOW)](../3_architecture_landscape/segment/digital_lending_stp/statement_of_architecture_work.md): Approving scope boundaries for micro-loan limits.
    - [Prelim & Phase A Vision](../3_architecture_landscape/segment/digital_lending_stp/preliminary_and_phase_a_vision.md): Documenting the core business scenario.

### Scenario Area 2: Architecture Definition (Phases B, C, D)
*   **Objective**: Defining baseline and target models for Business, Data, Application, and Technology domains, highlighting differences.
*   **Repository Alignment**:
    - [Phase B Business Arch](../3_architecture_landscape/segment/digital_lending_stp/phase_b_business_architecture.md) & [Process Flows](../3_architecture_landscape/segment/digital_lending_stp/bpmn_and_process_flows.md) (BPMN/Sequence).
    - [Phase C Data Arch](../3_architecture_landscape/segment/digital_lending_stp/phase_c_data_architecture.md) & [Tables Schema](../3_architecture_landscape/segment/digital_lending_stp/phase_c_data/data_dictionary_and_models.md).
    - [Phase C Application Arch](../3_architecture_landscape/segment/digital_lending_stp/phase_c_application_architecture.md) & [Microservices Portfolio](../3_architecture_landscape/segment/digital_lending_stp/phase_c_application/microservices_portfolio.md).
    - [Phase D Technology Arch](../3_architecture_landscape/segment/digital_lending_stp/phase_d_technology_architecture.md) & [Deployment Topology](../3_architecture_landscape/segment/digital_lending_stp/phase_d_technology/deployment_topology.md).

### Scenario Area 3: Transition Planning (Phases E and F)
*   **Objective**: Sequencing projects, analyzing building blocks, evaluating build-vs-buy, assessing risks, and constructing the migration timeline.
*   **Repository Alignment**:
    - [Transition Arch (TA1/TA2)](../3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md): Managing migration from legacy ledger integrations to wrap-around layers.
    - [Migration Roadmap Timeline](../3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/migration_roadmap.md): Detailing work packages and phases.

### Scenario Area 4: Governance (Phases G and H)
*   **Objective**: Formulating implementation rules, monitoring developer compliance, handling design waivers, and coordinating change requests (RFCs).
*   **Repository Alignment**:
    - [Waiver Registry Log](../6_governance_log/waivers/README.md): Granting conditional waivers for API mock latencies.
    - [Change Management Governance](../3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/change_management_governance.md): Controlling configuration drifts.

### Scenario Area 5: Adapting the ADM
*   **Objective**: Tailoring the ADM steps to fit specific organizational needs (e.g. Agile delivery, regulatory compliance, mergers).
*   **Repository Alignment**:
    - [Governance Framework](../2_architecture_capability/governance_framework.md): Customizing the ADM gates to fit bi-weekly sprint cadences.

### Scenario Area 6: Architecture Content Framework
*   **Objective**: Organizing architectural metadata, content metamodels, and deliverables into a structured repository.
*   **Repository Alignment**:
    - [1. Metamodel Index](../1_architecture_metamodel/README.md): Restricting data entities to follow DPDP and banking regulatory catalogs.

### Scenario Area 7: TOGAF Reference Models
*   **Objective**: Implementing standard reference structures like the Technical Reference Model (TRM) to guide software choices.
*   **Repository Alignment**:
    - [Standards Index (SIB)](../4_standards_information_base/README.md): Mandating standard networking (TLS 1.3), container orchestration (Kubernetes), and authorization (OAuth 2.0/OIDC).

### Scenario Area 8: Architecture Capability Framework
*   **Objective**: Establishing an architecture team, specifying skills, assigning roles, and structuring board governance.
*   **Repository Alignment**:
    - [Governance Framework](../2_architecture_capability/governance_framework.md#1-architecture-board-charter): Assigning roles for the Chief Architect, Security Officer, and Compliance Leads.
