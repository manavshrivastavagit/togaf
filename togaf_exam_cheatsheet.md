# TOGAF® Enterprise Architecture Foundation - Quick Revision Cheatsheet

This cheatsheet provides a high-density, condensed reference of key concepts, templates, criteria, and ADM phase details essential for last-minute revision before the TOGAF® Foundation exam.

> [!TIP]
> * For the full list of definitions, refer to the [TOGAF Exam Glossary](file:///Users/manavshrivastava/Documents/github/resume/togaf/togaf_exam_glossary.md).
> * For detailed study notes, see the [TOGAF Exam Preparation Topics Guide](file:///Users/manavshrivastava/Documents/github/resume/togaf/togaf_exam_preparation_topics.md).

---

## 1. Core Core Concepts & Definitions

* **Enterprise:** Any collection of organizations that have common goals. Can comprise partner/supplier/customer networks, multiple organizations, or a subset. Understood as a system.
* **Building Block (BB):** A package of functionality defined to meet business needs across an organization, recognizable by domain experts. It is potentially reusable and replaceable, has defined boundaries, and its specification is loosely coupled to its implementation.
* **Architecture View:** A representation of a system from the perspective of a related set of concerns. Meaningful to stakeholders.
* **Architecture Viewpoint:** The vantage point/perspective that determines what can be seen (defines conventions/schemas to construct views). It is generic and reusable.
* **Draft Deliverable:** Under development, no formal review/approval.
* **Approved Deliverable:** Formally reviewed and approved. May still evolve in later phases under formal change control.

---

## 2. The BDAT Architecture Domains
1. **Business (B):** Strategy, governance, organization, key business processes.
2. **Data (D):** Structure of conceptual, logical, physical data assets and data management resources.
3. **Application (A):** Blueprint for individual applications to deploy, their interactions, and business process relations.
4. **Technology (T):** Digital architecture, logical software and hardware infrastructure capabilities, and standards.

---

## 3. Scoping, Landscape Levels & Abstraction

### The 4 Dimensions of Scoping
1. **Enterprise Scope (Breadth):** What part of the enterprise is covered?
2. **Level of Detail (Depth):** How much architecture is "enough" (vs. design/dev)?
3. **Architecture Domains:** Which of B, D, A, or T are included?
4. **Time Period:** What is the planning horizon for the Architecture Vision?

### Landscape Levels
1. **Strategic Architecture:** Direction setting at executive level.
2. **Segment Architecture:** Roadmaps at program or portfolio level.
3. **Capability Architecture:** Roadmaps for capability increments.

### Abstraction Levels (Layering)
* **Contextual:** Environment, scope, goals, objectives.
* **Conceptual:** Requirements, service models.
* **Logical:** Implementation-independent components.
* **Physical:** Implementation allocation alternatives.

---

## 4. ADM Phases Cheat-Sheet

```
[Preliminary] -> [Phase A: Vision] -> [Phase B: Business] -> [Phase C: Info Systems] -> [Phase D: Tech] 
                                                                                         |
[Phase H: Change Mgmt] <- [Phase G: Gov] <- [Phase F: Migration] <- [Phase E: Opp & Sol] <-+
  ^
  |-- (Requirements Management runs continuously across all phases)
```

| Phase | Core Objective | Key Deliverables Created/Modified |
| :--- | :--- | :--- |
| **Preliminary** | Establishes Capability, tailors framework, defines principles. | Architecture Principles, Request for Architecture Work (output) |
| **Phase A** | Sets scope, identifies stakeholders, establishes vision & project. | Architecture Vision, Statement of Architecture Work, Communications Plan, Req. Spec (draft) |
| **Phase B** | Develops Baseline & Target Business Architecture. | Business Architecture, Req. Spec (Business draft) |
| **Phase C** | Develops Baseline & Target Data & Application Architectures. | Data & Application Architectures, Req. Spec (Data/App draft) |
| **Phase D** | Develops Baseline & Target Technology Architecture. | Technology Architecture, Req. Spec (Technology draft) |
| **Phase E** | Conducts initial implementation planning & identifies delivery vehicles. | Opp. & Solutions roadmap, implementation strategy |
| **Phase F** | Finalizes detailed Implementation and Migration Plan. | Migration Plan, Request for Architecture Work (migration terms) |
| **Phase G** | Provides architectural oversight of the implementation. | Implementation governance oversight, Req. Spec (input for conformance) |
| **Phase H** | Establishes procedures for managing architecture change. | Change management procedures, Change Requests |
| **Req. Mgmt** | Operates continuous requirements intake, validation, and update. | Architecture Requirements Specification (populated/updated) |

---

## 5. Templates & Criteria Quick-Reference

### Architecture Principles Template
1. **Name:** Essence of the principle (easy to remember).
2. **Statement:** Unambiguous statement of the fundamental rule.
3. **Rationale:** Business benefit of adhering to the rule; trade-offs.
4. **Implications:** Resource, cost, activity requirements; answers *"How does this affect me?"*.

### Good Principle Set Criteria
* **Complete:** Covers every situation perceived.
* **Consistent:** Flexible interpretations without contradiction.
* **Stable:** Enduring, yet accommodates changes.
* **Understandable:** Clear and unambiguous intentions.
* **Robust:** Enables high-quality decisions in complex situations.

### SMART Business Scenario Outcomes
* **S**pecific: Defines what needs to be done.
* **M**easurable: Clear metrics for success.
* **A**ctionable: Segmented problem, provides a basis for solution plans.
* **R**ealistic: Solvable within physical, time, and cost constraints.
* **T**ime-bound: Clear statement of when opportunity expires.

### Business Scenario Elements
* Real business problem.
* Business & technology environment.
* Desired outcome(s).
* Human actor(s).
* Computer actor(s).
* > [!WARNING]
  > Omitting any of these 5 elements risks an incomplete solution.

---

## 6. Critical Deliverables & ADM Touchpoints

* **Request for Architecture Work:** Sent by sponsoring organization to trigger ADM cycle. Created in Preliminary, Phase F, and H. Input to A-E.
* **Communications Plan:** Created in Phase A; used as input in B, C, D, E, F.
* **Architecture Requirements Specification:** Quantitative companion to the qualitative Architecture Definition Document. Drafted in A, populated in B, C, D, used/finalized in G and H, managed continuously via Requirements Management.
* **Business Principles, Goals, Drivers:** Confirmed in Phase A; used as inputs to validate and select resources in B, C, and D.
