# TOGAF Class: Reference Library

The **Reference Library** contains reusable design assets, templates, guidelines, and patterns to accelerate the design and execution of new architectures.

---

## 📐 1. TOGAF Approved Deliverable Templates

These templates conform to the TOGAF Standard v10 and should be copied as the starting point for any new architecture project:

1.  **[Architecture Principles Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_principles_template.md)**: Format for establishing principles with statement, rationale, and implications.
2.  **[Statement of Architecture Work Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/statement_of_architecture_work_template.md)**: Agreement defining scope, timeline, milestones, and RACI.
3.  **[Architecture Vision Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_vision_template.md)**: High-level vision, stakeholders, boundaries, and value case.
4.  **[Architecture Definition Document (ADD) Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_definition_document_template.md)**: Base container for detailed Business, Data, Application, and Technology designs.
5.  **[Architecture Requirements Specification Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_requirements_specification_template.md)**: Quantitative requirements list and Traceability Matrix (RTM).
6.  **[Transition Architecture & Roadmap Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/transition_architecture_roadmap_template.md)**: Gap analysis, work packages, roadmap schedules, and transitions (TA-1, TA-2).
7.  **[Architecture Contract Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_contract_template.md)**: Governance agreement on conformance and performance SLAs.
8.  **[Architecture Waiver Request Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/architecture_waiver_request_template.md)**: Request form for temporary or permanent standards deviation.
9.  **[Compliance Assessment Template](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/templates/compliance_assessment_template.md)**: Audit checklist and scorecard for reviewing implementations.

---

## 🎨 2. Architectural & Integration Patterns

Refer to these established patterns in `patterns/` for microservices design:
*   **Transactional Outbox Pattern**: Used to guarantee message delivery from database-to-Kafka without dual-write failures.
*   **Saga Pattern**: Orchestrates distributed transactions across microservices (e.g., matching e-KYC status, liveness check, and scorecard execution).
*   **Resilience Circuit Breaker**: Prevents cascade failures when third-party partner APIs (e.g., Credit Bureau, Aadhaar OTP) experience high latency or down-time.
