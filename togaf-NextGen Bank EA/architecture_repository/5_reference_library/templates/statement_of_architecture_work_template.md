# TOGAF Deliverable Template: Statement of Architecture Work

The **Statement of Architecture Work** is the formal agreement between the sponsor and the architecture organization defining the scope, deliverables, timeline, resources, and governance for an architecture development project.

---

## 1. Document Control & Approvals

| Field | Description |
| :--- | :--- |
| **Document Title** | Statement of Architecture Work |
| **Project/Initiative** | [Project Name] |
| **Sponsoring Executive** | [Sponsor Name / Title] |
| **Lead Architect** | [Architect Name / Title] |
| **Date** | [YYYY-MM-DD] |
| **Version** | [0.1, 1.0, etc.] |

### Executive Sign-Off
By signing below, the Sponsor and Lead Architect agree to the scope of work, deliverables, and timelines outlined in this document.

*   **Sponsor Signature**: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ (Date: \_\_\_\_\_\_\_\_\_\_)
*   **Lead Architect Signature**: \_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_\_ (Date: \_\_\_\_\_\_\_\_\_\_)

---

## 2. Project Background & Strategic Context

### 2.1 Executive Summary
[Provide a summary of the business challenges driving this architecture project and what the resulting architecture aims to achieve.]

### 2.2 Alignment with Corporate Strategy
[Reference specific corporate strategic goals, KPIs, or policies that this work package supports.]

---

## 3. Architecture Project Objectives

The core objectives of this architecture engagement are:
*   **Objective 1**: [Describe objective e.g., define target cloud integration patterns]
*   **Objective 2**: [Describe objective e.g., establish GDPR data lifecycle models]
*   **Objective 3**: [Describe objective e.g., analyze business capabilities for a new segment]

---

## 4. Scope of Work

The boundaries of this architecture project are defined below:

```
┌─────────────────────────────────────────────────────────────────────────────┐
┌──────────────────────────────────────────┬──────────────────────────────────┐
│ IN-SCOPE                                 │ OUT-OF-SCOPE                     │
├──────────────────────────────────────────┼──────────────────────────────────┤
│ - [Define systems/domains to design]     │ - [Define systems/domains excluded]│
│ - [e.g., Application integration layer]  │ - [e.g., Core database refactor] │
│ - [e.g., Security & IAM flow profiles]   │ - [e.g., End-user UI screens]    │
└──────────────────────────────────────────┴──────────────────────────────────┘
```

---

## 5. Stakeholders & Roles (RACI Matrix)

The key stakeholders and their responsibilities in this project are defined using the RACI framework:
*   **R**esponsible: Those who do the work to achieve the task.
*   **A**ccountable: The one who approves the work (must be only one per task).
*   **C**onsulted: Those whose inputs are sought; two-way communication.
*   **I**nformed: Those who are kept up-to-date; one-way communication.

| Deliverable / Task | Sponsoring Executive | Lead Architect | Security Team | Business Stakeholders | Development Team |
| :--- | :---: | :---: | :---: | :---: | :---: |
| **Architecture Vision** | **A** | **R** | **C** | **C** | **I** |
| **Business Architecture** | **I** | **R** | **I** | **C** | **I** |
| **Data Architecture** | **I** | **R** | **C** | **C** | **I** |
| **Application & Tech Arch** | **I** | **R** | **C** | **I** | **R** |
| **Migration Roadmap** | **A** | **R** | **I** | **C** | **C** |
| **Conformance Review** | **A** | **R** | **C** | **I** | **C** |

---

## 6. Workplan & Key Milestones

The proposed schedule for completing the ADM phases of this project:

| Milestone / Gate | Phase / Activity | Deliverables | Target Date |
| :--- | :--- | :--- | :--- |
| **Gate 1** | Preliminary / Phase A | Architecture Vision, Scope definition | [YYYY-MM-DD] |
| **Gate 2** | Phases B, C, D | Architecture Definition Document (ADD) | [YYYY-MM-DD] |
| **Gate 3** | Phases E & F | Gap Analysis, Migration Roadmap | [YYYY-MM-DD] |
| **Gate 4** | Phase G | Conformance Review & Deployment Sign-off | [YYYY-MM-DD] |

---

## 7. Deliverables & Outputs

The following formal TOGAF deliverables will be produced:
1.  **Architecture Vision**: Strategic overview, stakeholder map.
2.  **Architecture Definition Document (ADD)**: Business, Data, Application, and Technology baseline & target models.
3.  **Architecture Requirements Specification**: Functional and non-functional requirements.
4.  **Transition Architecture & Migration Roadmap**: Gaps, work packages, roadmap.
5.  **Architecture Contract**: Conformance checklist, SLA alignments.
