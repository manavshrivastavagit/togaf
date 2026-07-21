# TOGAF ADM Complete Reference — All Phases with Objectives, Inputs, Steps & Outputs

**Source:** Visual Paradigm TOGAF ADM Guide-Through  
**URL:** https://circle.visual-paradigm.com/docs/togaf-adm-guide-through/

---

## ADM Overview

The TOGAF Architecture Development Method (ADM) is the core of TOGAF. It describes a method for developing and managing the lifecycle of enterprise architecture. The ADM is:

- **Iterative** — over the whole process, between phases, and within phases
- **Proven** — developed through contributions from many architecture practitioners
- **Generic** — must be tailored to organization-specific needs
- **Continuous** — repeated executions populate the organization's Enterprise Continuum

### ADM Phase Sequence

```
Preliminary → A (Architecture Vision) → B (Business Architecture)
→ C (Information Systems Architectures: Data + Application)
→ D (Technology Architecture) → E (Opportunities & Solutions)
→ F (Migration Planning) → G (Implementation Governance)
→ H (Architecture Change Management)
with Requirements Management running continuously
```

---

## Preliminary Phase

### Purpose
Prepare the organization for successful enterprise architecture projects. Defines "where, what, why, who, and how we do architecture."

### Objectives
1. Determine the Architecture Capability desired by the organization
2. Establish the Architecture Capability

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs (business strategy, drivers)
- Architectural Inputs (existing assets)

### Steps
1. **Scope the Enterprise Organizations Impacted**
   - Identify core, soft, extended, and community impacted units
   - Use ArchiMate diagram with color coding
   - Perform EA Maturity Assessment (radar/spider chart for baseline vs target)
   - Identify key roles and responsibilities (Architecture Board, Sponsor, Manager, Architects, PMs, IT Designers)
   - Fill in RACI Chart
   - Determine constraints (organizational, budget, external/business)
   - Confirm budget requirements

2. **Confirm Governance and Support Frameworks**
   - Draw governance structure diagram (Corporate → Technology → IT → Architecture)
   - Describe support strategy

3. **Define and Establish Enterprise Architecture Team and Organization**

4. **Identify and Establish Architecture Principles**
   - Define principles across 4 categories: Business, Data, Application, Technology
   - Each principle: Name, Statement, Rationale, Implications

5. **Tailor the TOGAF Framework** (and other selected frameworks)

6. **Develop a Strategy and Implementation Plan for Tools and Techniques**

### Outputs / Deliverables
| Deliverable | Description |
|-------------|-------------|
| **Organizational Model for Enterprise** | Defines organization, roles, responsibilities; includes maturity assessment, RACI chart, governance structure |
| **Tailored Architecture Framework** | TOGAF adapted to organization's needs |
| **Initial Architecture Repository** | 6 classes: Metamodel, Capability, Landscape, SIB, Reference Library, Governance Log |
| **Business Principles, Business Goals & Business Drivers** | Provides context for architecture work |
| **Request for Architecture Work** (optional) | Triggers start of ADM cycle; describes business imperatives, requirements, success criteria, timeframe, constraints |
| **Architecture Governance Framework** | Governance structure and processes |

### Key Deliverable Details

**Architecture Repository** contains six classes:
| Class | Description |
|-------|-------------|
| Architecture Metamodel | Organizationally tailored application of architecture framework |
| Architecture Capability | Parameters, structures, processes supporting governance |
| Architecture Landscape | Architectural representation of assets in use/planned |
| Standards Information Base (SIB) | Standards new architectures must comply with |
| Reference Library | Guidelines, templates, patterns |
| Governance Log | Record of governance activity |

**Request for Architecture Work** includes: project background, business imperative, success criteria (short & long term), project timeframe (implementation roadmap), constraints, additional information.

---

## Phase A — Architecture Vision

### Purpose
Initial phase of an ADM architecture development cycle. Defines scope, identifies stakeholders, creates Architecture Vision, and obtains approvals.

### Objectives
1. Develop a high-level aspirational vision of the capabilities and business value to be delivered
2. Obtain approval for a Statement of Architecture Work

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs (business strategy, goals)
- Architectural Inputs (from Preliminary Phase and Repository)

### Steps
1. **Establish the Architecture Project**
2. **Identify Stakeholders, Concerns, and Business Requirements**
3. **Confirm and Elaborate Business Goals, Business Drivers, and Constraints**
4. **Evaluate Capabilities** — Business, IT, and Architecture maturity assessments
5. **Assess Readiness for Business Transformation** — Business Factor Assessment
6. **Define Scope** — dimensions: breadth, depth, time period, architecture domains
7. **Confirm and Elaborate Architecture Principles** (including Business Principles)
8. **Develop Architecture Vision** — Problem definition, change drivers, high-level objectives, solution concept diagram
9. **Define the Target Architecture Value Propositions and KPIs**
10. **Identify the Business Transformation Risks and Mitigation Activities**
11. **Develop Statement of Architecture Work; Secure Approval**

### Outputs / Deliverables
| Deliverable | Description |
|-------------|-------------|
| **Statement of Architecture Work** (approved) | Defines scope and approach; basis for contractual agreement |
| **Architecture Vision** | High-level aspirational view; supports stakeholder communication |
| **Communications Plan** | Enables effective communication to right stakeholders at right time |
| **Capability Assessment** | Baseline and target capability levels; maturity and readiness assessments |
| **Architecture Principles** | Refined from Preliminary Phase |
| **Draft Architecture Definition Document** | Initial version, to be refined in later phases |
| **Refined Business Principles, Goals & Drivers** | Validated and elaborated |
| **Tailored Architecture Framework** | Further refined |

### Key Deliverable Details

**Architecture Vision** includes:
- Problem definition & change drivers
- High-level architecture objectives (business + technology)
- Stakeholders and their concerns
- Project constraints
- Solution Concept Diagram (ArchiMate showing actors, concerns, assessments)

**Communications Plan** includes:
- Stakeholder communication requirements table
- Communication Matrix (purpose, provider, collection, reporting)
- Delivery vehicles and frequency (email, meetings, presentations, etc.)

**Capability Assessment** includes:
- Business Capability Maturity (radar chart, baseline vs target)
- IT Capability Maturity
- Architecture Maturity Assessment
- Transformation Readiness Assessment (Business Factor Assessment)

**Statement of Architecture Work** includes:
- Project description, problem description
- Architecture objectives
- Stakeholders list
- Governance and support strategy
- Risks and assumptions
- Acceptance criteria and procedure
- Architecture project plan and schedule

---

## Phase B — Business Architecture

### Purpose
Develop a Business Architecture to support the agreed Architecture Vision. Describes product/service strategy, organizational, functional, process, information, and geographic aspects.

### Objectives
1. Develop the Target Business Architecture that describes how the enterprise needs to operate to achieve business goals
2. Identify candidate Architecture Roadmap components based on gaps between Baseline and Target Business Architectures

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phase A)

### Steps
1. **Select Reference Models, Viewpoints, and Tools**
2. **Develop Baseline Business Architecture Description** — Model current state using ArchiMate
3. **Develop Target Business Architecture Description** — Model future state
4. **Perform Gap Analysis** — Define gaps between baseline and target (7 potential gap sources)
5. **Define Candidate Roadmap Components**
6. **Resolve Impacts Across the Architecture Landscape**
7. **Conduct Formal Stakeholder Review**
8. **Finalize the Business Architecture**
9. **Create the Architecture Definition Document**

### Outputs / Deliverables

**Core Deliverables:**
- Draft Architecture Definition Document
- Draft Architecture Requirements Specification
- Business Architecture components of an Architecture Roadmap

**Catalogs:**
| Catalog | Description |
|---------|-------------|
| Value Stream catalog | List of value streams |
| Business Capabilities catalog | Business capabilities |
| Value Stream Stages catalog | Stages within value streams |
| Organization/Actor catalog | Organizational units and actors |
| Driver/Goal/Objective catalog | Business drivers, goals, objectives |
| Role catalog | Roles within the organization |
| Business Service/Function catalog | Services and functions |
| Location catalog | Business locations |
| Process/Event/Control/Product catalog | Business processes |
| Contract/Measure catalog | Contracts and measures |

**Matrices:**
| Matrix | Description |
|--------|-------------|
| Value Stream/Capability matrix | Maps value streams to capabilities |
| Strategy/Capability matrix | Maps strategy to capabilities |
| Capability/Organization matrix | Maps capabilities to organizations |
| Business Interaction matrix | Shows business interactions |
| Actor/Role matrix | Maps actors to roles |

**Diagrams:**
| Diagram | Description |
|---------|-------------|
| Business Model diagram | High-level business model |
| Business Capability Map | Map of business capabilities |
| Value Stream Map | End-to-end value delivery |
| Organization Map | Organizational structure |
| Business Footprint diagram | Business functions by location |
| Business Service/Information diagram | Services and information |
| Functional Decomposition diagram | Decomposition of functions |
| Product Lifecycle diagram | Product stages |
| Goal/Objective/Service diagram | Goals to services mapping |
| Business Use-Case diagram | Business use cases |
| Organization Decomposition diagram | Organization breakdown |
| Process Flow diagram | Business process flows |
| Event diagram | Business events |

### Key Deliverable Details

**Architecture Definition Document (Phase B)** includes:
- Stakeholder responsibilities for business architecture
- Baseline Business Architecture (ArchiMate diagram)
- Target Business Architecture (ArchiMate diagram)
- Gap Analysis (diagram + gap sources: not addressed, partially addressed, intentionally omitted, new, eliminated, concerns added, concerns addressed)
- Impact Analysis (organizational impact of transition)
- Finalized form: objectives, stakeholders, constraints, compliance, risks, assumptions, issues

**Architecture Requirements Specification (Phase B)** includes:
- Quantitative statements of implementation requirements
- Business domain requirements with constraints, assumptions, and success measures

---

## Phase C — Information Systems Architectures

### Purpose
Develop Data and Application Architectures. Enables effective use of data and shows how IT systems meet business goals.

### Data Architecture Objectives
1. Develop the Target Data Architecture that enables the Business Architecture and the Architecture Vision
2. Identify candidate Architecture Roadmap components based on gaps between Baseline and Target Data Architectures

### Application Architecture Objectives
1. Develop the Target Application Architecture that enables the Business Architecture and Architecture Vision
2. Identify candidate Architecture Roadmap components based on gaps between Baseline and Target Application Architectures

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phases A, B)

### Steps (Data Architecture)
1. **Select Reference Models, Viewpoints, and Tools**
2. **Develop Baseline Data Architecture Description**
3. **Develop Target Data Architecture Description**
4. **Perform Gap Analysis**
5. **Define Candidate Roadmap Components**
6. **Resolve Impacts Across the Architecture Landscape**
7. **Conduct Formal Stakeholder Review**
8. **Finalize the Data Architecture**
9. **Create the Architecture Definition Document**

*(Same step structure applies for Application Architecture)*

### Outputs / Deliverables

**Core Deliverables:**
- Draft Architecture Definition Document
- Draft Architecture Requirements Specification
- Data/Application Architecture components of Architecture Roadmap

**Data Architecture Catalogs:**
| Catalog | Description |
|---------|-------------|
| Data Entity/Data Component catalog | Data entities and components |

**Data Architecture Matrices:**
| Matrix | Description |
|--------|-------------|
| Data Entity/Business Function matrix | Maps data to business functions |
| Application/Data matrix | Maps applications to data |

**Data Architecture Diagrams:**
| Diagram | Description |
|---------|-------------|
| Conceptual Data diagram | High-level data concepts |
| Logical Data diagram | Logical data model |
| Data Dissemination diagram | Data flow between entities |
| Data Security diagram | Data security and controls |
| Data Migration diagram | Data migration paths |
| Data Lifecycle diagram | Data through its lifecycle |

**Application Architecture Catalogs:**
- Application Portfolio catalog

**Application Architecture Matrices:**
- Application/Organization matrix
- Application/Function matrix
- Application Interaction matrix

**Application Architecture Diagrams:**
- Application Communication diagram
- Application and User Location diagram
- Application Use-Case diagram
- Enterprise Manageability diagram
- Process/Application Realization diagram
- Software Engineering diagram
- Application Migration diagram
- Software Distribution diagram

---

## Phase D — Technology Architecture

### Purpose
Develop the Technology Architecture covering hardware, software, and communications technology.

### Objectives
1. Develop the Target Technology Architecture that enables the Architecture Vision, target business, data, and application building blocks to be delivered through technology components and services
2. Identify candidate Architecture Roadmap components based on gaps between Baseline and Target Technology Architectures

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phases A, B, C)

### Steps
1. **Select Reference Models, Viewpoints, and Tools** (e.g., TOGAF TRM)
2. **Develop Baseline Technology Architecture Description**
3. **Develop Target Technology Architecture Description**
4. **Perform Gap Analysis**
5. **Define Candidate Roadmap Components**
6. **Resolve Impacts Across the Architecture Landscape**
7. **Conduct Formal Stakeholder Review**
8. **Finalize the Technology Architecture**
9. **Create the Architecture Definition Document**

### Outputs / Deliverables

**Core Deliverables:**
- Draft Architecture Definition Document
- Draft Architecture Requirements Specification
- Technology Architecture components of Architecture Roadmap

**Catalogs:**
| Catalog | Description |
|---------|-------------|
| Technology Standards catalog | Approved technology standards |
| Technology Portfolio catalog | Technology portfolio inventory |

**Matrices:**
| Matrix | Description |
|--------|-------------|
| Application/Technology matrix | Maps applications to technology |

**Diagrams:**
| Diagram | Description |
|---------|-------------|
| Environments and Locations diagram | Technology environments by location |
| Platform Decomposition diagram | Platform breakdown |
| Processing diagram | Processing architecture |
| Networked Computing/Hardware diagram | Hardware and computing |
| Network and Communications diagram | Network topology |

---

## Phase E — Opportunities and Solutions

### Purpose
Identify delivery vehicles (projects, programs, portfolios) that effectively deliver the Target Architecture. Concentrates on **how** to deliver.

### Objectives
1. Generate the initial complete version of the Architecture Roadmap based on gap analysis from Phases B, C, D
2. Determine whether an incremental approach is required and identify Transition Architectures
3. Define the overall solution building blocks to finalize the Target Architecture

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phases A–D)

### Steps
1. **Determine/Confirm Key Corporate Change Attributes** — Implementation Factor Assessment
2. **Determine Business Constraints for Implementation**
3. **Review and Consolidate Gap Analysis Results from Phases B to D** — Consolidated Gaps, Solutions & Dependencies Matrix
4. **Review Consolidated Requirements Across Related Business Functions**
5. **Consolidate and Reconcile Interoperability Requirements**
6. **Refine and Validate Dependencies**
7. **Confirm Readiness and Risk for Business Transformation**
8. **Formulate Implementation and Migration Strategy** — Strategic direction (Greenfield/Revolutionary/Evolutionary), sequencing approach
9. **Identify and Group Major Work Packages** — WBS diagram, WBS Dictionary, Work Package Portfolio
10. **Identify Transition Architectures** — ArchiMate diagram showing Baseline → Transition → Target plateaus
11. **Create the Architecture Roadmap & Implementation and Migration Plan** — Migration Roadmap timeline

### Outputs / Deliverables

**Core Deliverables:**
| Deliverable | Description |
|-------------|-------------|
| **Architecture Roadmap** | Lists increments of change on a timeline from baseline to target |
| **Implementation and Migration Plan (v0.1)** | Initial schedule for implementation |
| **Capability Assessments** | Updated from Phase A |
| Draft Architecture Definition Document | Updated |
| Draft Architecture Requirements Specification | Updated |

**Diagrams:**
| Diagram | Description |
|---------|-------------|
| Project Context diagram | Project scope and context |
| Benefits diagram | Business benefits of the architecture |

### Key Deliverable Details

**Architecture Roadmap (Phase E)** includes:
- Implementation Factor Assessment table
- Consolidated Gaps, Solutions & Dependencies Matrix
- Work Breakdown Structure (WBS) diagram
- WBS Dictionary (definition, deliverables, cost, resources, milestones per work package)
- Work Package Portfolio
- Transition Architecture diagram (ArchiMate)
- Migration Roadmap timeline (work package bars, milestones, investment points)

**Implementation and Migration Plan (Phase E v0.1)** includes:
- Strategic Implementation Direction (Greenfield, Revolutionary, Evolutionary)
- Implementation sequencing approach (Quick win, Achievable targets, Value chain)

---

## Phase F — Migration Planning

### Purpose
Finalize a detailed Implementation and Migration Plan. Move from Baseline to Target Architecture in cooperation with portfolio and project managers.

### Objectives
1. Finalize the Architecture Roadmap and supporting Implementation and Migration Plan
2. Ensure coordination with the enterprise's overall change portfolio
3. Ensure business value and cost of work packages and Transition Architectures is understood by stakeholders

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phase E)

### Steps
1. **Confirm Management Framework Interactions for the Implementation and Migration Plan** — Coordinate with other management frameworks
2. **Assign a Business Value to Each Work Package**
3. **Estimate Resource Requirements, Project Timings, and Availability/Delivery Vehicle**
4. **Prioritize the Migration Projects** — Through cost/benefit assessment and risk validation
5. **Confirm Architecture Roadmap and Update Architecture Definition Document**
6. **Complete the Implementation and Migration Plan**
7. **Complete the Architecture Development Cycle and Document Lessons Learned**

### Outputs / Deliverables

**Core Deliverables:**
| Deliverable | Description |
|-------------|-------------|
| **Implementation and Migration Plan (v1.0)** | Refined, finalized schedule |
| **Finalized Architecture Definition Document** | Completed AD Doc |
| **Finalized Architecture Requirements Specification** | Completed requirements |
| **Finalized Architecture Roadmap** | Completed roadmap |
| **Re-Usable Architecture Building Blocks** | ABBs for future use |
| **Implementation Governance Model** | Governance processes for implementation |
| **Requests for Architecture Work** | For new ADM iteration (if any) |
| **Change Requests for Architecture Capability** | From lessons learned |

**Additional Deliverables (from sub-pages):**
| Deliverable | Description |
|-------------|-------------|
| **Architecture Contract (Business Users)** | Signed intent from business users to conform to architecture |
| **Architecture Contract (Development Partners)** | Signed intent with partner organizations |
| **Architecture Change Request** | Submitted when original definition is unsuitable |

### Key Deliverable Details

**Implementation Governance Model** includes processes for:
- Policy Management and Take-On
- Compliance (assessments against SLAs, OLAs, standards, regulations)
- Dispensation (time-bound alternative routes for non-compliant areas)
- Monitoring and Reporting (performance management)
- Business Control (compliance with business policies)
- Environment Management (repository-based governance)

**Architecture Contract (Business Users)** — Signed statement of intent covering:
- Continuous monitoring, adherence to principles/standards
- Risk identification
- Accountability
- Formal governance understanding

**Architecture Contract (Development Partners)** — Signed agreement with partners covering:
- Deliverables, quality, fitness-for-purpose
- Collaboration processes
- Governance during development

**Architecture Change Request** — Submitted when:
- Original Architecture Definition is unsuitable/insufficient
- External factors open opportunities to extend/refine
- Assessed and approved by Architecture Board

---

## Phase G — Implementation Governance

### Purpose
Provide architectural oversight of implementation. Govern and manage architecture contracts and monitor implementation work for conformance.

### Objectives
1. Ensure conformance with the Target Architecture by implementation projects
2. Perform appropriate Architecture Governance functions for the solution and implementation-driven Architecture Change Requests

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phase F)

### Steps
1. **Confirm Scope and Priorities for Deployment with Development Management**
2. **Identify Deployment Resources and Skills**
3. **Guide Development of Solutions Deployment**
4. **Perform Enterprise Architecture Compliance Reviews** — Review against checklists
5. **Implement Business and IT Operations**
6. **Perform Post-Implementation Review and Close the Implementation**

### Outputs / Deliverables

| Deliverable | Description |
|-------------|-------------|
| **Architecture Contract (signed)** | Formal agreement architecture↔implementation |
| **Compliance Assessments** | Results of compliance reviews |
| **Change Requests** | Implementation-driven change requests |
| **Architecture-compliant solutions deployed** | Verified compliant implementations |

### Key Deliverable Details

**Compliance Assessment** includes reviews against these checklists:
1. Hardware and Operating System Checklist
2. Software Services and Middleware Checklist
3. Applications Checklist
4. Information Management Checklist
5. Security Checklist
6. System Management Checklist
7. System Engineering Checklist
8. Methods and Tools Checklist

Each checklist documents review results, non-compliances, and actions.

**Architecture Change Request (Phase G)** — Same process as Phase F; triggered during implementation governance when issues arise or changes are needed.

---

## Phase H — Architecture Change Management

### Purpose
Establish procedures for managing change to the new architecture. Ensure the architecture achieves its original target business value.

### Objectives
1. Ensure that the architecture lifecycle is maintained
2. Ensure that the Architecture Governance Framework is executed

### Inputs
- Reference Materials External to the Enterprise
- Non-Architectural Inputs
- Architectural Inputs (from Phase G)

### Steps
1. **Establish Value Realization Process**
2. **Deploy Monitoring Tools**
3. **Manage Risks**
4. **Provide Analysis for Architecture Change Management**
5. **Develop Change Requirements to Meet Performance Targets**
6. **Manage Governance Process**
7. **Activate the Process to Implement Change**

### Change Classification
| Change Type | Description | Action |
|-------------|-------------|--------|
| **Simplification** | Simplifying/streamlining | Minor update |
| **Incremental** | Additions (e.g., new server) | Minor update |
| **Re-architecting** | New requirements not in original scope | New ADM cycle |

### Outputs / Deliverables

| Deliverable | Description |
|-------------|-------------|
| **Architecture updates** | For maintenance changes |
| **Changes to architecture framework and principles** | For maintenance changes |
| **New Request for Architecture Work** | To initiate new ADM cycle for major changes |
| **Statement of Architecture Work** | Updated if necessary |
| **Architecture Contract** | Updated if necessary |
| **Compliance Assessments** | Updated if necessary |

---

## Requirements Management (Continuous)

### Position in ADM
The Requirements Management phase is a continuous, central process that runs throughout the entire ADM cycle. It:
- Stores and manages requirements
- Manages the flow of requirements into and out of relevant ADM phases
- Tracks change to requirements
- Ensures requirements are addressed in all phases

### Key Activities
- Receive requirements from all ADM phases
- Assess impact of new/changed requirements
- Feed requirements back to appropriate phases
- Maintain the Consolidated Requirements Repository

---

## Quick Reference: All ADM Outputs

| Phase | Key Outputs |
|-------|-------------|
| **Preliminary** | Organizational Model for EA, Tailored Architecture Framework, Initial Architecture Repository, Business Principles/Goals/Drivers, Request for Architecture Work (optional), Architecture Governance Framework |
| **Phase A** | Statement of Architecture Work, Architecture Vision, Communications Plan, Capability Assessment, Architecture Principles, Draft Architecture Definition Document, Refined Business Principles/Goals/Drivers |
| **Phase B** | Draft Architecture Definition Document, Draft Architecture Requirements Specification, Business Architecture Roadmap components, Business Catalogs (10), Matrices (5), Diagrams (13) |
| **Phase C** | Draft Architecture Definition Document, Draft Architecture Requirements Specification, Data Architecture Roadmap components, Data Catalogs (1), Matrices (2), Diagrams (6), Application Architecture Catalogs/Matrices/Diagrams |
| **Phase D** | Draft Architecture Definition Document, Draft Architecture Requirements Specification, Technology Architecture Roadmap components, Technology Catalogs (2), Matrices (1), Diagrams (5) |
| **Phase E** | Architecture Roadmap, Implementation & Migration Plan v0.1, Capability Assessments, Project Context diagram, Benefits diagram |
| **Phase F** | Implementation & Migration Plan v1.0, Finalized Architecture Definition Document, Finalized Architecture Requirements Specification, Finalized Architecture Roadmap, Re-Usable ABBs, Implementation Governance Model, Architecture Contracts (Business Users + Development Partners), Architecture Change Requests |
| **Phase G** | Signed Architecture Contracts, Compliance Assessments, Change Requests, Architecture-compliant solutions deployed |
| **Phase H** | Architecture updates, Framework/Principles changes, New Request for Architecture Work, Updated Statement of Architecture Work/Contracts/Compliance Assessments |
| **Requirements Mgmt** | Consolidated Requirements Repository, Requirements Impact Assessments |

---

## Cross-Phase Summary

### Common Steps Across Phases B, C, D (Architecture Development)
1. Select Reference Models, Viewpoints, and Tools
2. Develop Baseline Architecture Description
3. Develop Target Architecture Description
4. Perform Gap Analysis
5. Define Candidate Roadmap Components
6. Resolve Impacts Across the Architecture Landscape
7. Conduct Formal Stakeholder Review
8. Finalize the Architecture
9. Create/Update the Architecture Definition Document

### Common Input Sources for All Phases
| Source | Description |
|--------|-------------|
| Reference Materials External to the Enterprise | Industry standards, reference models, best practices |
| Non-Architectural Inputs | Business strategy, goals, drivers, constraints |
| Architectural Inputs | Outputs from previous phases, Architecture Repository |

### Key Techniques Used Across ADM
| Technique | Used In |
|-----------|---------|
| Gap Analysis | Phases B, C, D |
| Business Scenarios | Phase A |
| Stakeholder Management | Phase A, all phases |
| Risk Management | All phases |
| Capability-Based Planning | Phases E, F |
| Business Transformation Readiness | Phase A, E |
| Migration Planning | Phases E, F |
| Interoperability Analysis | Phase E |
| Architecture Compliance Review | Phase G, H |

---

*Complete reference compiled from Visual Paradigm Community Circle TOGAF ADM Guide-Through documentation.*
