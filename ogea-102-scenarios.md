# OGEA-102 TOGAF Enterprise Architecture Part 2 — 100 Scenario-Based Questions

**Exam:** OGEA-102 | **Cert:** TOGAF Enterprise Architecture Practitioner  
**TOGAF Version:** 10th Edition | **Questions:** 8 scenario sets in 120 min  
**Difficulty:** Practitioner — scenario analysis, application, judgment

---

## How to Use These Questions

Each question presents a **realistic business scenario** followed by a question asking you to apply TOGAF concepts. Scenarios test your ability to determine:
- Which ADM phase/technique is most appropriate
- What deliverable to produce in a given situation
- How to handle governance, compliance, and change management
- How to apply architecture principles, viewpoints, and reference models
- How to manage stakeholders, risks, and transformation readiness

**Sources:** OG0-092 classic scenarios (ITExams, ExamTopics), OGEA-102 practice questions from GitHub repos (xde013/togaf, Gana-Dube/togaf-exam-hub, sutharsuresh/togaf-part-2), and original scenarios modeled on real exam patterns.

---

## SECTION 1: Classic OG0-092 Scenarios (Q1–15)

### Q1 — Rollins Manufacturing: Architecture Principles

**Scenario:** Rollins Manufacturing is a major automotive supplier headquartered in Cleveland, Ohio with plants in Chicago, Sao Paulo, Stuttgart, Yokohama, and Seoul. Each plant operates its own MRPII system, production scheduling, and custom applications. Rollins is implementing lean manufacturing. A common ERP system in Cleveland will replace these. Plant managers are concerned about security and reliability of a central system. The Architecture Review Board approved a Request for Architecture Work. The Common ERP Deployment project team has been formed to develop an Architecture Vision. The Chief Engineer wants to know how concerns can be addressed.

**Your role:** Lead Enterprise Architect.

**Question:** One of the earliest initiatives was the definition of IT principles and architecture principles aligned with enterprise principles. These now need to be updated. Which set of principles is most appropriate for guiding the team to define a robust solution?

- A. Common-use Applications, Data is Shared, Data is Accessible, Data is Secure, Interoperability, Control Technical Diversity
- B. Business Continuity, Service-orientation, Data is Accessible, Data is Secure, Responsive Change Management
- C. Maximize Benefit to the Enterprise, Business Continuity, Common-use Applications, Data is Shared, Data is Accessible, Data is Secure
- D. Information Management is Everybody's Business, IT Responsibility, Data Trustee, Technology Independence, Responsive Change Management

**Answer: C**

---

### Q2 — Global Mobile: Capability-Based Planning

**Scenario:** Global Mobile is a telecom company formed through mergers. Customer service systems are not fully integrated. ARPU and retention are below industry average. Customers are switching to competitor Air Light. The Board approved funding for a multi-million Euro conversion to a packaged Customer Service System, expected to take five years. The Board also requires at least 30% savings through Green initiatives (energy efficiency, virtualization, telecommuting). TOGAF 9 is the basis for EA.

**Your role:** Consultant to advise the Chief Architect.

**Question:** What approach should be used for implementation planning?

- A. Conventional implementation planning — Capability-Based Planning is difficult for horizontal Green initiative scope
- B. Capability-Based Planning — appropriate for enterprise-wide plan with horizontal scope; metrics aggregated at enterprise level
- C. Capability-Based Planning focuses on business outcomes; Green initiative is technical infrastructure; use SDLC
- D. Capability-Based Planning is for public sector/defense only; not appropriate for private sector

**Answer: B**

---

### Q3 — AGEX Inc.: Preliminary Phase / Security

**Scenario:** AGEX is a global commodities trading company grown through acquisitions. Each BU maintains its own applications. Implementing a single ERP system. The Corporate Board is concerned about managing customer information meeting legal requirements across countries. The CIO formed an EA department and a cross-functional Architecture Review Board. TOGAF 9 selected.

**Your role:** Chief Architect.

**Question:** What approach should be taken in the Preliminary Phase to address the Board's concern?

- A. Evaluate implications in terms of regulatory and security policy requirements. Update security policy, communicate across org. Allocate security architecture team. Assess security implications.
- B. Evaluate implications and impact on business goals. Issue Request for Architecture Work. Allocate security architect to oversee ERP implementation.
- C. Start by clarifying the Board's intent. Understand implications of regulatory requirements and impact on business goals. Propose a security architect/team to develop comprehensive security architecture.
- D. Evaluate impacts on business goals. Update current security policy. Allocate security architect for all domains.

**Answer: A**

---

### Q4 — Zephyr Enterprises: Architecture Contract

**Scenario:** Zephyr Enterprises develops wind turbine blades with facilities in Palm Springs, Omaha, and Winnipeg. A mature EA organization using TOGAF 9 recently completed an architecture project defining a standard Automated Test System controller. The Manufacturing Architecture Board approved implementation. An Architecture Contract was developed. The Chief Engineer wants a uniform process at each site to ensure consistency.

**Your role:** Lead Architect for this activity.

**Question:** What approach should be adopted to address the Chief Engineer's concern?

- A. Create Architecture Contract. For external: legal contract. For internal: MOU. If deviation, modify contract to allow customization. Issue new Request for Architecture Work.
- B. Create Architecture Contract. For external: legal contract. For internal: MOU. If deviation, grant dispensation for local customization.
- C. Create Architecture Contract. For external: legal contract. For internal: MOU. ARB reviews all deviations and considers whether to grant dispensation.
- D. Create Architecture Contract. Address project objectives, effectiveness metrics, acceptance criteria, risk management. Schedule compliance reviews. ARB reviews deviations and considers dispensations.

**Answer: C**

---

### Q5 — Vittronics Ltd. (SPICE): Risk Mitigation

**Scenario:** Vittronics Ltd. is a medical device manufacturer in the MHPM market. The EA group has been developing SPICE — a Secure Private Immersive Collaborative Environment for researchers to share clinical trial information. The SPICE project completed Business, IS, and Technology Architecture phases. A Business Transformation Readiness Assessment in Phase A identified risks — researchers are resisting due to patient data privacy concerns.

**Your role:** Lead Architect for SPICE.

**Question:** How should this resistance be managed in the implementation planning phases?

- A. In Phase E, create an overall solutions strategy. Check consensus before proceeding.
- B. Return to Phase A, brainstorm technical solution for residual risks. In Phase D, develop ABB for security risks. Select SBBs. Revise Requirements Impact Statement.
- C. In Phase E, review the Business Transformation Readiness Assessment, identify/classify/mitigate risks. If mitigated, define high-level solutions strategy with Transition Architectures.
- D. In Phase E, determine approach to implementing strategic direction that addresses risks.

**Answer: C**

---

### Q6 — Florian Flowers BV: Stakeholder Views

**Scenario:** Florian Flowers BV is an international agricultural company headquartered in Rotterdam with centers in 60+ countries. Subject to various legal/regulatory requirements including GMO compliance. The Governing Board wants to be informed about compliance-impacting projects. Legal staff and auditors need to analyze architectures. Research needs to verify architecture is appropriate. TOGAF 9 mandated.

**Your role:** Lead Consultant.

**Question:** What approach enables developing an architecture addressing all parties' needs?

- A. Create models ensuring compliance. Stakeholders view models to see concerns addressed.
- B. Use a consistent uniform modeling approach across all projects.
- C. For powerful/interested groups, create special reports summarizing key features.
- D. Develop stakeholder map, define views addressing each group's concerns, create models for each view.

**Answer: A**

---

### Q7 — Armstrong Defense Industries: Viewpoints

**Scenario:** Armstrong Defense Industries, prime contractor for Dreadnought UAS, has grown by acquisition inheriting redundant procurement processes and systems. CEO wants preferred supplier program. Need Baseline and Target Architectures addressing stakeholder concerns. No existing architectural assets. Prefer package applications. Project completed Architecture Context iteration and starts Architecture Definition iteration. Using TOGAF iterative ADM.

**Your role:** Lead Architect.

**Question:** Which architecture viewpoints are most appropriate?

- A. Early iterations: Baseline Process catalog, Technology Portfolio catalog, Data diagram. Later: Target Actor/Process/Data catalog, System/Technology matrix, Data Dissemination diagram.
- B. Early iterations: Target Business Service/Function catalog + Business Interaction matrix, Product Lifecycle diagrams, Target Application Communication diagrams + Interaction matrix, Target Data Entity/Business Function matrix.
- C. Early iterations: Target Business Service/Function catalog + Organization/Actor catalog, Data Lifecycle diagrams, Target Application Communication diagrams, Target System/Data matrix.
- D. Early iterations: Baseline Organization/Actor catalog, System/Function matrix, Data Entity/Data Component catalog. Later: Target Organization/Actor catalog, Application Communication diagrams, System/Data matrix.

**Answer: B**

---

### Q8 — St. Croix Consulting: Risk Assessment

**Scenario:** St. Croix Consulting expanded from accounting to IT/Business Services. Engagement management is challenging. EA team created framework, principles, Architecture Vision, and four domain Architecture Definitions for a five-year vision. Senior management is concerned the architecture is too ambitious and may not produce sufficient value.

**Your role:** Chief Enterprise Architect.

**Question:** What approach should assess risks and value before preparing the Implementation Plan?

- A. Apply interoperability analysis. Finalize Roadmap and Migration Plan.
- B. Gather solution information. Analyze Solution Architecture using state evolution table.
- C. Create consolidated gap analysis. Gather solution information. Analyze with state evolution table. Apply interoperability analysis.
- D. Apply Business Transformation Readiness Assessment and Business Value Assessment.

**Answer: C**

---

### Q9 — Zephyr Enterprises (Compliance): Compliance Assessment

**Scenario:** Same Zephyr Enterprises. You are conducting Compliance Assessments at each plant. At Omaha, the Distributed Data Acquisition System uses proprietary RPC with kernel mode threads instead of user mode threads as specified. All other respects meet requirements.

**Your role:** Compliance Assessor.

**Question:** How should compliance be described?

- A. All features per spec except RPC. Describe as conformant.
- B. Many features in common, RPC uses features not covered by spec. Describe as consistent.
- C. RPC has no features in common with spec. Describe as consistent.
- D. RPC not implemented per spec. Describe as non-conformant.

**Answer: D**

---

### Q10 — Rollins Manufacturing (Initiation): Business Scenarios

**Scenario:** Same Rollins Manufacturing. The project team assembles. Participants voice concerns about the sweeping scope. Multiple recommendations are put forward.

**Your role:** Lead Enterprise Architect.

**Question:** Which recommendation best enables the team to evaluate approaches and clarify requirements?

- A. Hold interviews using business scenario technique to identify and document architecture characteristics from business requirements.
- B. Research vendor literature, conduct briefings with approved suppliers. Define preliminary Target Architecture Vision. Build consensus.
- C. Create Baseline and Target Architectures for each plant. Gap analysis validates approach.
- D. Conduct pilot project for short-listed vendors. Develop complete requirements.

**Answer: A**

---

### Q11 — AGEX Inc. (Security Architecture): Security Approach

**Scenario:** AGEX Inc. (same as Q3). The Board is concerned about data security across countries. You need to develop a security architecture approach during the Preliminary Phase.

**Your role:** Chief Architect.

**Question:** Which action should be taken first in the Preliminary Phase regarding security?

- A. Create a comprehensive security architecture as a separate domain
- B. Identify and document the security policy requirements, assess regulatory implications, and plan for security integration across all domains
- C. Outsource security architecture to an external consultant
- D. Defer security considerations to Phase D

**Answer: B**

---

### Q12 — Florian Flowers (Viewpoints): Viewpoint Design

**Scenario:** Florian Flowers (same as Q6). Different stakeholder groups have different concerns about the new architecture. The research team needs to see data models. Legal needs compliance verification. Operations needs process models.

**Your role:** Lead Consultant.

**Question:** What is the recommended approach to address multiple stakeholder concerns?

- A. Create one comprehensive model that addresses all concerns
- B. Identify stakeholder groups, define a viewpoint for each group's concerns, and create views from those viewpoints
- C. Focus only on the most powerful stakeholder group
- D. Create separate models for each individual stakeholder

**Answer: B**

---

### Q13 — Global Mobile (Green Initiative): Transition Planning

**Scenario:** Global Mobile (same as Q2). The Green initiative requires 30% cost savings. The program will take five years. The Chief Architect needs to plan implementation.

**Your role:** Consultant to the Chief Architect.

**Question:** How should Transition Architectures be used?

- A. Implement all changes at once to maximize savings
- B. Define Transition Architectures that deliver incremental business value while moving toward the Target Architecture
- C. Skip Transition Architectures as they add overhead
- D. Create a single Transition Architecture at the midpoint

**Answer: B**

---

### Q14 — Vittronics (Security Architecture): Security Integration

**Scenario:** Vittronics (same as Q5). The SPICE project includes sensitive clinical trial data. Security architecture has been defined but researchers are still concerned about privacy.

**Your role:** Lead Architect.

**Question:** How should security be addressed in the architecture?

- A. Security is a separate domain addressed only after all other domains
- B. Security should be integrated into each ADM phase as a cross-cutting concern
- C. Security is addressed only in Phase D Technology Architecture
- D. Security is only the IT department's responsibility

**Answer: B**

---

### Q15 — Armstrong Defense (Stakeholders): Concern Resolution

**Scenario:** Armstrong Defense (same as Q7). Six specific stakeholder concerns have been identified about procurement processes, applications, data sharing, and integration.

**Your role:** Lead Architect.

**Question:** What is the correct approach to ensuring these concerns are addressed?

- A. Address all concerns in Phase A only
- B. Use stakeholder management and architecture views to map each concern to specific viewpoints and address them throughout the ADM
- C. Prioritize concerns by stakeholder power and address only the top 3
- D. Defer concerns to implementation phase

**Answer: B**

---

## SECTION 2: Autonomous Driving & Automotive Scenarios (Q16–30)

### Q16 — Autonomous Driving: Security Architecture

**Scenario:** A company developing Level 5 autonomous driving technology is building a swarm data platform. Multiple vehicle manufacturers and data providers will contribute data and consume analytics services. The platform must handle V2X communication, real-time sensor data, and machine learning model updates. Partners have different security standards. Data sovereignty regulations vary by country. The CISO is concerned about data leakage and unauthorized model access.

**Your role:** Chief Enterprise Architect.

**Question:** What is the best approach to address risk and security considerations?

- A. Define a single comprehensive security policy that all partners must comply with
- B. Create a security domain model, establish a security federation with contractual arrangements, and undertake a risk assessment for each data asset class
- C. Delegate security to each partner independently
- D. Focus only on encryption of data in transit

**Answer: B**

---

### Q17 — Autonomous Driving: Partner Integration

**Scenario:** Same autonomous driving company. Each partner uses different data formats, communication protocols, and security mechanisms. The architecture must enable seamless data sharing while protecting intellectual property.

**Your role:** Chief Enterprise Architect.

**Question:** Which TOGAF technique should be prioritized in Phase E?

- A. Gap Analysis
- B. Interoperability Analysis
- C. Business Scenarios
- D. Capability-Based Planning

**Answer: B**

---

### Q18 — Autonomous Driving: ADM Selection

**Scenario:** Same autonomous driving company. The EA team is new and has never used TOGAF before. The CEO wants a working data platform within 12 months. There is pressure to skip architecture and start building.

**Your role:** Chief Enterprise Architect.

**Question:** What is the most appropriate approach?

- A. Skip architecture and start building immediately
- B. Execute a tailored ADM cycle, starting with the Preliminary Phase to establish framework and principles, then iterate through phases focusing on critical architecture domains
- C. Execute the full ADM without tailoring
- D. Use a waterfall SDLC instead of TOGAF

**Answer: B**

---

### Q19 — Automotive Manufacturer: Battery Pack Deployment

**Scenario:** A multinational automotive manufacturer has completed a pilot for a new battery pack production process at one plant. The pilot was successful. The Chief Engineer now needs to deploy the same process at 12 plants worldwide. Each plant has different equipment vendors, local regulations, and workforce skills. The Chief Engineer wants consistency in quality and safety but recognizes local adaptations are necessary.

**Your role:** Lead Architect for deployment.

**Question:** Which approach best balances consistency with local adaptation?

- A. Design a single detailed solution and mandate it at all plants
- B. Allow each plant to implement independently
- C. Use Architecture Contracts with compliance reviews and a dispensation process for justified local variations
- D. Defer all architecture decisions to plant managers

**Answer: C**

---

### Q20 — Automotive Manufacturer: Architecture Contract Implementation

**Scenario:** Same automotive manufacturer. Architecture Contracts have been developed for each plant. The Omaha plant needs a deviation because local safety regulations require different emergency shutdown procedures than the standard design.

**Your role:** Lead Architect.

**Question:** What is the correct governance process?

- A. Allow Omaha to implement the deviation without review
- B. The plant manager approves the deviation
- C. Submit an Architecture Change Request to the Architecture Board describing the regulatory requirement and proposed solution
- D. Update the standard architecture to include both options

**Answer: C**

---

### Q21 — Electric Vehicle Startup: Rapid Architecture

**Scenario:** An electric vehicle startup is growing rapidly. They need to establish an architecture practice but have limited resources and no existing EA capability. The CTO wants to use TOGAF but is concerned about overhead.

**Your role:** Chief Architect.

**Question:** What is the most pragmatic approach to the Preliminary Phase?

- A. Implement full TOGAF Architecture Capability as specified
- B. Tailor the framework to the startup's needs, define essential architecture principles, and establish lightweight governance proportionate to the organization's size
- C. Skip the Preliminary Phase entirely
- D. Hire a large EA team before starting any architecture work

**Answer: B**

---

### Q22 — Electric Vehicle Startup: ADM Tailoring

**Scenario:** Same EV startup. They need to define their first architecture for a new battery management system. The timeline is aggressive.

**Your role:** Chief Architect.

**Question:** How should the ADM be tailored?

- A. Follow all ADM phases in strict sequence
- B. Use an iterative approach, focusing on the minimum viable architecture artifacts needed for governance, and iterate as the product evolves
- C. Only execute Phase D (Technology Architecture)
- D. Execute Phase A and Phase G only

**Answer: B**

---

### Q23 — Automotive Tier 1 Supplier: M&A Integration

**Scenario:** A tier 1 automotive supplier acquires a software company to gain autonomous driving capabilities. The acquired company has a startup culture with agile development. The acquirer has a mature TOGAF-based EA practice. The two companies need to integrate their architecture approaches.

**Your role:** Chief Enterprise Architect.

**Question:** How should the architecture integration be approached?

- A. Mandate the acquirer's TOGAF process on the acquired company
- B. Let the acquired company continue independently
- C. Use Architecture Partitioning to allow different approaches while establishing integration points and governance for cross-cutting concerns
- D. Abandon TOGAF for a lighter framework

**Answer: C**

---

### Q24 — Automotive Tier 1 Supplier: Phase Selection

**Scenario:** Same supplier. The acquisition integration needs to address business processes, IT systems, data models, and technology platforms. The CEO wants a unified target state within 18 months.

**Your role:** Chief Enterprise Architect.

**Question:** Which ADM phase should start this integration work?

- A. Phase A: Architecture Vision
- B. Preliminary Phase
- C. Phase H: Architecture Change Management
- D. Phase G: Implementation Governance

**Answer: B** (A new architecture cycle begins with the Preliminary Phase)

---

### Q25 — Automotive Manufacturer: Global Standards

**Scenario:** The automotive manufacturer from Q19 needs to define global technology standards for its new battery production equipment. Different regions have different equipment vendors, but data must be consolidated globally.

**Your role:** Lead Architect.

**Question:** Which Architecture Repository component should be prioritized?

- A. Governance Log
- B. Standards Information Base (SIB) to define approved technology standards
- C. Architecture Landscape
- D. Architecture Metamodel

**Answer: B**

---

### Q26 — Electric Vehicle Startup: Stakeholder Management

**Scenario:** The EV startup has multiple stakeholder groups with conflicting interests: engineering wants cutting-edge technology, finance wants cost control, manufacturing wants proven reliability, and marketing wants fast time-to-market.

**Your role:** Chief Architect.

**Question:** What is the best approach to manage these conflicting stakeholder concerns?

- A. Prioritize engineering since they build the product
- B. Use stakeholder analysis to map concerns, develop architecture views addressing each group, and present trade-offs for decision
- C. Focus on cost control since the company is a startup
- D. Let the CEO resolve all conflicts

**Answer: B**

---

### Q27 — Automotive Tier 1 Supplier: Risk Management

**Scenario:** The supplier's architecture integration project carries significant risk: the acquired company's key engineers may leave, technology platforms are incompatible, and the integration timeline is aggressive.

**Your role:** Chief Enterprise Architect.

**Question:** When should risk management be applied?

- A. Only in Phase A during initial risk assessment
- B. Only in Phase F during migration planning
- C. Risk management should be applied in all ADM phases
- D. Risk management is the project manager's responsibility

**Answer: C**

---

### Q28 — Autonomous Driving: Data Architecture

**Scenario:** The autonomous driving company needs to manage petabytes of sensor data from test vehicles worldwide. Data is used for training AI models, regulatory compliance, and incident analysis. Different data types have different retention and security requirements.

**Your role:** Chief Enterprise Architect.

**Question:** Which Phase C artifact is most important to develop first?

- A. Application Communication diagram
- B. Data Entity/Data Component catalog to classify and define all data assets
- C. Technology Portfolio catalog
- D. Business Footprint diagram

**Answer: B**

---

### Q29 — Electric Vehicle Startup: Architecture Vision

**Scenario:** The EV startup has raised Series B funding and needs to scale production. Investors want to see a clear technology roadmap. The CTO needs to communicate the architecture vision to the board, engineering team, and manufacturing partners.

**Your role:** Chief Architect.

**Question:** What is the primary purpose of the Architecture Vision in this context?

- A. It provides a detailed technical specification
- B. It provides a high-level aspirational view to gain stakeholder buy-in and align expectations
- C. It replaces the business plan
- D. It defines the project budget

**Answer: B**

---

### Q30 — Automotive Manufacturer: Requirements Management

**Scenario:** The battery pack deployment project encounters new regulatory requirements halfway through implementation. The requirements affect the design of the battery management system.

**Your role:** Lead Architect.

**Question:** How should these new requirements be handled?

- A. Ignore them since the architecture is already approved
- B. Feed them into the Requirements Management process, assess impact, and determine if they warrant a change request or a new ADM cycle
- C. Implement them immediately without assessment
- D. Defer them to the next architecture cycle

**Answer: B**

---

## SECTION 3: Financial Services & Insurance Scenarios (Q31–45)

### Q31 — Global Bank: Digital Transformation

**Scenario:** A global bank with operations in 50 countries wants to transform its digital banking platform. The current architecture has grown through 30 years of acquisitions and mergers, resulting in over 200 applications. The CEO wants a unified customer experience. The CRO is concerned about regulatory compliance. The COO is concerned about operational risk during transition. The bank has no formal EA practice.

**Your role:** Chief Enterprise Architect (newly hired).

**Question:** What is the first step?

- A. Start designing the target digital platform immediately
- B. Execute the Preliminary Phase to establish EA capability, governance, and principles
- C. Hire a system integrator to build the platform
- D. Conduct a pilot project with a new mobile banking app

**Answer: B**

---

### Q32 — Global Bank: Architecture Principles

**Scenario:** Same bank. The Preliminary Phase is underway. Stakeholders have conflicting priorities: security wants strict controls, marketing wants rapid feature delivery, operations wants stability, and finance wants cost reduction.

**Your role:** Chief Enterprise Architect.

**Question:** What is the correct approach to defining architecture principles?

- A. Let each department define its own principles
- B. Define principles that balance all concerns, with rationale and implications clearly documented; get Architecture Board approval
- C. Prioritize security principles over all others
- D. Use generic principles from the TOGAF standard without customization

**Answer: B**

---

### Q33 — Insurance Company: Legacy Modernization

**Scenario:** A large insurance company has a 40-year-old mainframe policy administration system. It is costly to maintain, difficult to change, and skilled mainframe staff are retiring. The company wants to modernize but has 5 million active policies that must remain operational.

**Your role:** Enterprise Architect.

**Question:** Which ADM approach best addresses this situation?

- A. Big-bang replacement of the mainframe
- B. Define Transition Architectures that incrementally replace functionality while maintaining operations
- C. Keep the mainframe and build a facade layer
- D. Outsource the mainframe operations

**Answer: B**

---

### Q34 — Insurance Company: Architecture Roadmap

**Scenario:** Same insurance company. Modernization is planned over 3 years. The legacy mainframe has dependencies with 40+ downstream systems. Regulatory reporting depends on mainframe data.

**Your role:** Enterprise Architect.

**Question:** What is the most important output of Phase E for this project?

- A. Architecture Vision
- B. Architecture Roadmap showing Transition Architectures with work packages sequenced by dependency and business value
- C. Technology Architecture diagrams
- D. Architecture Principles

**Answer: B**

---

### Q35 — Fintech Startup: EA for Regulated Industry

**Scenario:** A fintech startup has grown rapidly and now needs to comply with financial regulations (PCI-DSS, KYC, AML). They have no formal EA. Regulators require evidence of controlled IT processes and architecture governance. The startup culture is agile and resistant to process.

**Your role:** EA Consultant.

**Question:** How should EA be established without killing the startup culture?

- A. Implement full TOGAF with all governance boards immediately
- B. Tailor the ADM to focus on compliance-critical architecture domains first, with lightweight governance that can mature over time
- C. Tell the startup they cannot use agile with TOGAF
- D. Focus only on Phase G: Implementation Governance

**Answer: B**

---

### Q36 — Investment Bank: Data Architecture

**Scenario:** An investment bank needs to consolidate trading data from 15 different systems into a single data platform for analytics and regulatory reporting. Each system has different data models, formats, and quality levels.

**Your role:** Enterprise Architect.

**Question:** Which Phase C activity is most critical?

- A. Application Communication diagrams
- B. Data Entity/Business Function matrix and Data Migration diagram to understand data lineage and transformation needs
- C. Technology Portfolio catalog
- D. Business Footprint diagram

**Answer: B**

---

### Q37 — Investment Bank: Gap Analysis

**Scenario:** Same investment bank. The baseline data architecture has significant gaps compared to the target. Some data entities exist in multiple systems with inconsistent definitions. Some required data is not captured anywhere.

**Your role:** Enterprise Architect.

**Question:** What is the purpose of Gap Analysis in this context?

- A. To identify which systems to decommission
- B. To identify data entities that are missing, redundant, or need to be created in the target architecture
- C. To calculate the project budget
- D. To assign work to project teams

**Answer: B**

---

### Q38 — Retail Bank: Phase B Approach

**Scenario:** A retail bank wants to redesign its mortgage origination process to reduce processing time from 30 days to 5 days. The current process involves multiple handoffs between branches, underwriting, legal, and settlements.

**Your role:** Enterprise Architect.

**Question:** Which Phase B artifacts are most important to develop?

- A. Technology Standards catalog
- B. Process Flow diagrams, Business Service/Function catalog, and Value Stream map
- C. Networked Computing diagram
- D. Application Communication diagram

**Answer: B**

---

### Q39 — Insurance Company: Compliance Assessment

**Scenario:** Same insurance company. During Phase G, a compliance review finds that the new customer portal stores credit card numbers in violation of PCI-DSS standards specified in the architecture.

**Your role:** Enterprise Architect.

**Question:** What is the correct action?

- A. Allow the portal to go live and fix later
- B. Document the non-compliance, require the project team to remediate before go-live, and report to the Architecture Board
- C. Update the architecture to allow credit card storage
- D. Ignore the issue since it's a minor implementation detail

**Answer: B**

---

### Q40 — Global Bank: Architecture Change

**Scenario:** Same global bank. Six months after completing the target architecture, a major new regulation (open banking) requires the bank to expose APIs to third-party providers. This was not in the original architecture scope.

**Your role:** Chief Enterprise Architect.

**Question:** How should this be handled in Phase H?

- A. Classify as re-architecting and initiate a new ADM cycle
- B. Classify as incremental and implement within existing architecture
- C. Ignore the regulation
- D. Defer until the next annual planning cycle

**Answer: A**

---

### Q41 — Insurance Company: Migration Planning

**Scenario:** Same insurance company. The legacy modernization program has 47 identified work packages. There is budget for only 15 in the fiscal year.

**Your role:** Enterprise Architect.

**Question:** What is the best prioritization approach in Phase F?

- A. Implement the easiest work packages first
- B. Use Capability-Based Planning to prioritize work packages that deliver the most critical business capabilities first
- C. Implement the most expensive work packages first
- D. Let each business unit prioritize its own work packages

**Answer: B**

---

### Q42 — Fintech Startup: Agile Alignment

**Scenario:** Same fintech startup. The development teams use Scrum with two-week sprints. They need architecture guidance but cannot wait for months of architecture work.

**Your role:** EA Consultant.

**Question:** How should the ADM align with agile development?

- A. Complete all ADM phases before any development starts
- B. Use Phase G Implementation Governance with compliance reviews at each sprint boundary to provide architectural oversight while allowing agile development
- C. Skip architecture for agile teams
- D. Use only Phase A for agile projects

**Answer: B**

---

### Q43 — Retail Bank: Business Transformation Readiness

**Scenario:** The retail bank's mortgage transformation project is struggling. Staff are resistant to new processes, branch managers fear losing authority, and the IT team is overwhelmed. The project sponsor wants to know if the organization is ready for this change.

**Your role:** Enterprise Architect.

**Question:** Which technique should be used?

- A. Gap Analysis
- B. Business Transformation Readiness Assessment
- C. Capability-Based Planning
- D. Interoperability Analysis

**Answer: B**

---

### Q44 — Investment Bank: Solution Building Blocks

**Scenario:** The investment bank's data consolidation project needs to select specific technology products. The architecture defines logical components (ABBs) for data ingestion, storage, processing, and analytics.

**Your role:** Enterprise Architect.

**Question:** What is the relationship between ABBs and SBBs in Phase E?

- A. ABBs replace SBBs
- B. ABBs define what is needed; SBBs are specific products or implementations that realize the ABBs
- C. SBBs are defined before ABBs
- D. ABBs and SBBs are the same

**Answer: B**

---

### Q45 — Insurance Company: Governance

**Scenario:** The insurance company's modernization program involves multiple vendors and internal teams. The Architecture Board needs to ensure consistent decision-making.

**Your role:** Enterprise Architect.

**Question:** What is the most important governance mechanism for this multi-vendor program?

- A. Detailed project plans
- B. Architecture Contracts with each vendor and internal team, with compliance reviews at key milestones
- C. Regular status meetings
- D. Vendor scorecards

**Answer: B**

---

## SECTION 4: Healthcare & Life Sciences Scenarios (Q46–60)

### Q46 — Pharmaceutical Company: Clinical Trial Platform

**Scenario:** A pharmaceutical company is developing a global clinical trial platform. Trials run across 30 countries with different regulatory requirements. Data privacy laws (GDPR, HIPAA, China PIPL) impose conflicting requirements. Researchers need real-time data sharing. The regulatory affairs department needs audit trails.

**Your role:** Enterprise Architect.

**Question:** What is the most critical concern to address in Phase A?

- A. Technology platform selection
- B. Stakeholder analysis to identify all regulatory, research, and compliance concerns across jurisdictions
- C. Project budget
- D. Vendor selection

**Answer: B**

---

### Q47 — Pharmaceutical Company: Data Security

**Scenario:** Same pharmaceutical company. Patient data must be protected. Regulations require data localization in some countries. Researchers need global access to anonymized data.

**Your role:** Enterprise Architect.

**Question:** How should security architecture be addressed?

- A. Security is a Phase D concern only
- B. Security should be addressed in every ADM phase, with specific security viewpoints and risk assessments integrated throughout
- C. Security is the IT department's responsibility
- D. Security is addressed only after implementation

**Answer: B**

---

### Q48 — Hospital Network: Integration Architecture

**Scenario:** A hospital network with 15 hospitals is implementing an integrated Electronic Health Records (EHR) system. Each hospital currently uses different EHR systems. Patient safety depends on data accuracy and availability. Clinical staff are resistant to changing systems.

**Your role:** Enterprise Architect.

**Question:** What is the most important consideration in Phase B?

- A. Technology Architecture
- B. Stakeholder concerns about patient safety, clinical workflow changes, and data accuracy
- C. Budget constraints
- D. Vendor product features

**Answer: B**

---

### Q49 — Hospital Network: Migration Strategy

**Scenario:** Same hospital network. The EHR migration is high-risk — any data loss or system downtime could impact patient safety. The project team proposes a big-bang cutover.

**Your role:** Enterprise Architect.

**Question:** What migration strategy should be recommended?

- A. Big-bang cutover as proposed
- B. Phased migration with Transition Architectures, pilot at one hospital first, then incremental rollout with parallel running where needed
- C. Keep all existing systems
- D. Skip migration planning

**Answer: B**

---

### Q50 — Biotechnology Company: Research Collaboration

**Scenario:** A biotechnology company is partnering with three academic research institutions to develop a new gene therapy. Each partner has different IT systems, data standards, and security policies. Intellectual property protection is critical.

**Your role:** Enterprise Architect.

**Question:** Which reference model is most relevant?

- A. TRM
- B. III-RM — enabling boundaryless information flow between partners with appropriate security controls
- C. Business Reference Model
- D. Data Reference Model

**Answer: B**

---

### Q51 — Medical Device Manufacturer: Compliance

**Scenario:** A medical device manufacturer must comply with FDA regulations for its Class III implantable devices. The QA system must be validated. The architecture project is developing a new manufacturing execution system.

**Your role:** Enterprise Architect.

**Question:** Which Architecture Repository component should be prioritized?

- A. Governance Log
- B. Standards Information Base (SIB) to capture FDA standards and compliance requirements
- C. Architecture Landscape
- D. Reference Library

**Answer: B**

---

### Q52 — Biotechnology Company: Make vs Buy Decision

**Scenario:** The biotechnology company needs a laboratory information management system (LIMS). Options include building custom, buying commercial, or using open-source. Each has different cost, risk, and compliance implications.

**Your role:** Enterprise Architect.

**Question:** In which phase is the make vs buy decision addressed?

- A. Phase A: Architecture Vision
- B. Phase E: Opportunities and Solutions — identifies solutions and determines build vs buy vs reuse approach
- C. Phase D: Technology Architecture
- D. Phase G: Implementation Governance

**Answer: B**

---

### Q53 — Hospital Network: Phase F Coordination

**Scenario:** The hospital network's EHR program must coordinate with other ongoing initiatives: a new data center, a cybersecurity upgrade, and a telemedicine platform. These are managed by different teams with different timelines.

**Your role:** Enterprise Architect.

**Question:** What is the focus of Phase F in this context?

- A. Finalize the EHR architecture
- B. Coordinate the Implementation and Migration Plan with the enterprise's overall change portfolio and other management frameworks
- C. Conduct compliance reviews
- D. Define architecture principles

**Answer: B**

---

### Q54 — Pharmaceutical Company: Requirements Change

**Scenario:** The pharmaceutical company's clinical trial platform is in development. A new regulation requires electronic signatures with two-factor authentication. This was not in the original requirements.

**Your role:** Enterprise Architect.

**Question:** How should Requirements Management handle this?

- A. Reject as out of scope
- B. Assess impact through Requirements Impact Assessment, update the requirements repository, and feed the change into the relevant ADM phases
- C. Implement immediately
- D. Log for next architecture cycle

**Answer: B**

---

### Q55 — Healthcare AI Startup: Architecture Maturity

**Scenario:** An AI startup developing diagnostic algorithms wants to establish EA to help with FDA approval and hospital partnerships. The startup has 20 employees and no existing architecture practice.

**Your role:** EA Consultant.

**Question:** What maturity level assessment is most appropriate in the Preliminary Phase?

- A. Full Architecture Maturity Model assessment
- B. Lightweight maturity assessment focused on architecture capability needs proportionate to startup size and regulatory requirements
- C. No maturity assessment needed
- D. External audit

**Answer: B**

---

### Q56 — Medical Device Manufacturer: Architecture Contract

**Scenario:** The medical device manufacturer contracts with an external software developer to build the manufacturing execution system. Quality and compliance are critical.

**Your role:** Enterprise Architect.

**Question:** What should the Architecture Contract with the developer include?

- A. Only the budget and timeline
- B. Architecture compliance requirements, quality standards, acceptance criteria, compliance review schedule, and governance process for deviations
- C. Only technical specifications
- D. Only the project plan

**Answer: B**

---

### Q57 — Hospital Network: Phase H Transition

**Scenario:** The hospital network's first hospital goes live with the new EHR. The architecture team needs to ensure continued value realization and manage ongoing changes.

**Your role:** Enterprise Architect.

**Question:** What is the primary focus of Phase H for this hospital?

- A. Develop a new architecture
- B. Establish value realization process, deploy monitoring, and manage change requests to ensure architecture achieves business value
- C. Conduct post-implementation review and close the project
- D. Start a new ADM cycle

**Answer: B**

---

### Q58 — Pharmaceutical Company: Compliance Classification

**Scenario:** During compliance review, the team finds the clinical trial platform uses a database that has all features specified plus additional auditing features. No specified features are missing.

**Your role:** Enterprise Architect.

**Question:** How should compliance be classified?

- A. Conformant — all specified features are implemented
- B. Non-conformant — extra features were added without approval
- C. Irrelevant
- D. Partial

**Answer: A**

---

### Q59 — Healthcare AI Startup: Architecture Repository

**Scenario:** The healthcare AI startup needs to organize its architecture artifacts. The CTO wants to understand what goes into the Architecture Repository.

**Your role:** EA Consultant.

**Question:** Which six classes of information does the Architecture Repository contain?

- A. Architecture Metamodel, Architecture Capability, Architecture Landscape, Standards Information Base, Reference Library, Governance Log
- B. Architecture Models, Standards, Guidelines, Principles, Contracts, Reviews
- C. Business, Data, Application, Technology, Security, Governance
- D. Strategic, Segment, Capability, Foundation, Industry, Organization-Specific

**Answer: A**

---

### Q60 — Biotechnology Company: Phase G Oversight

**Scenario:** The biotechnology company's gene therapy collaboration platform is being implemented by multiple partners. The architecture team needs to ensure all partners comply with the agreed architecture.

**Your role:** Enterprise Architect.

**Question:** What is the primary role of Phase G in this multi-partner program?

- A. Design the technology architecture
- B. Provide architectural oversight of implementation, conduct compliance reviews, and manage architecture change requests
- C. Define requirements
- D. Plan migration

**Answer: B**

---

## SECTION 5: Government & Public Sector Scenarios (Q61–75)

### Q61 — Government Agency: AI-First Mandate

**Scenario:** A government agency has been mandated by the Prime Minister to implement AI-first approaches to improve citizen services. The agency has no EA practice. Staff are concerned about job displacement. Citizens are concerned about privacy and bias. IT infrastructure is outdated. Budget is limited.

**Your role:** Chief Enterprise Architect.

**Question:** What is the correct first step?

- A. Procure AI technology immediately
- B. Execute the Preliminary Phase to establish EA capability, assess current maturity, and develop a roadmap for architecture-driven transformation
- C. Train all staff on AI
- D. Conduct a pilot AI project

**Answer: B**

---

### Q62 — Government Agency: Stakeholder Analysis

**Scenario:** Same government agency. Stakeholders include politicians (want quick wins), civil servants (fear job loss), citizens (concerned about privacy), IT staff (lack AI skills), and privacy regulators (demand compliance).

**Your role:** Chief Enterprise Architect.

**Question:** How should these conflicting concerns be managed?

- A. Focus only on politicians' requirements since they control the budget
- B. Conduct stakeholder analysis, map concerns, develop architecture views for each group, and create a communications plan
- C. Prioritize IT staff concerns since they implement the solution
- D. Ignore citizen concerns since they are end-users

**Answer: B**

---

### Q63 — Defense Department: Security Architecture

**Scenario:** A defense department needs to modernize its logistics systems to work with allied nations. Systems must handle classified information while enabling coalition data sharing. Different nations have different security classifications and data handling rules.

**Your role:** Enterprise Architect.

**Question:** Which approach best addresses security requirements?

- A. Each nation maintains separate systems
- B. Develop a security architecture with multi-level security, data classification schemas, and federation agreements between nations
- C. Use commercial cloud services
- D. Build a single shared system with uniform security

**Answer: B**

---

### Q64 — Defense Department: Enterprise Continuum

**Scenario:** Same defense department. They want to reuse architecture assets from allied nations and NATO standard architectures.

**Your role:** Enterprise Architect.

**Question:** Which TOGAF component supports classification of these assets?

- A. Architecture Repository
- B. Enterprise Continuum — classifying assets from generic (NATO standards) to organization-specific
- C. ADM
- D. Architecture Content Framework

**Answer: B**

---

### Q65 — City Government: Smart City Architecture

**Scenario:** A city government wants to implement smart city initiatives: intelligent traffic management, waste management sensors, public safety analytics, and citizen services portal. Multiple city departments must collaborate. Budgets are siloed.

**Your role:** Enterprise Architect.

**Question:** What is the biggest architecture challenge?

- A. Technology selection
- B. Cross-departmental governance and funding — architecture must address organizational silos and create shared services
- C. Vendor management
- D. Citizen engagement

**Answer: B**

---

### Q66 — City Government: Phase A Scoping

**Scenario:** Same city government. The smart city program is potentially unlimited in scope. The mayor wants to show progress within 12 months.

**Your role:** Enterprise Architect.

**Question:** How should the architecture scope be defined?

- A. Include all smart city initiatives from the start
- B. Use scope dimensions (breadth, depth, time period, domains) to define a manageable first iteration focused on high-value, achievable initiatives
- C. Let each department define its own scope
- D. Start with technology only

**Answer: B**

---

### Q67 — Federal Agency: COTS vs Custom

**Scenario:** A federal agency needs a new benefits administration system. Commercial products exist but would require significant process changes. Custom development would be expensive and slow. Congress wants to see results before the next election.

**Your role:** Enterprise Architect.

**Question:** Which Phase E activity is most relevant?

- A. Gap Analysis
- B. Determine make vs buy vs reuse approach, identify work packages, and define Transition Architectures
- C. Architecture Principles
- D. Risk Assessment

**Answer: B**

---

### Q68 — Federal Agency: Architecture Contract

**Scenario:** Same federal agency. A systems integrator will build the benefits system. The contract must ensure the integrator follows the agency's architecture.

**Your role:** Enterprise Architect.

**Question:** What type of Architecture Contract is needed?

- A. Architecture Contract with Development Partners — specifying deliverables, quality criteria, compliance requirements, and governance process
- B. Architecture Contract with Business Users
- C. Memorandum of Understanding
- D. Service Level Agreement only

**Answer: A**

---

### Q69 — State Government: Shared Services

**Scenario:** A state government wants to consolidate IT services across 20 departments into a shared services center. Each department currently operates its own IT. Department heads resist losing control.

**Your role:** Enterprise Architect.

**Question:** What Phase B artifact is most useful for this consolidation?

- A. Technology Standards catalog
- B. Business Service/Function catalog and Business Interaction matrix to identify shared business services
- C. Network diagram
- D. Data Entity catalog

**Answer: B**

---

### Q70 — State Government: Migration Approach

**Scenario:** Same state government. The shared services migration is politically sensitive. Department heads have threatened to withhold cooperation.

**Your role:** Enterprise Architect.

**Question:** Which technique should be used in Phase A?

- A. Capability-Based Planning
- B. Business Transformation Readiness Assessment to understand organizational readiness and identify risks
- C. Gap Analysis
- D. Interoperability Analysis

**Answer: B**

---

### Q71 — Regulatory Agency: Compliance System

**Scenario:** A financial regulatory agency is building a new market surveillance system. The system must handle terabytes of trading data daily. Algorithmic accuracy is critical — false positives waste resources, false negatives miss violations.

**Your role:** Enterprise Architect.

**Question:** Which architecture domain should be prioritized in Phase C?

- A. Business Architecture
- B. Data Architecture — data quality, lineage, and retention are critical for regulatory evidence
- C. Technology Architecture
- D. Application Architecture only

**Answer: B**

---

### Q72 — Regulatory Agency: Architecture Governance

**Scenario:** Same regulatory agency. The agency is independent but must coordinate with other regulators internationally. Different regulators use different architectures.

**Your role:** Enterprise Architect.

**Question:** How should architecture governance be structured?

- A. Independent governance for each regulator
- B. Establish an Architecture Board and governance framework for the agency, with interface standards for international data exchange
- C. No governance needed for a regulatory agency
- D. Outsource governance to an external body

**Answer: B**

---

### Q73 — City Government: Stakeholder Communication

**Scenario:** The smart city program has diverse stakeholders: elected officials, city departments, citizens, vendors, and utility companies. Each needs different information at different times.

**Your role:** Enterprise Architect.

**Question:** What Phase A deliverable addresses this?

- A. Architecture Vision
- B. Communications Plan — defining information needs per stakeholder group, delivery vehicles, and frequency
- C. Statement of Architecture Work
- D. Capability Assessment

**Answer: B**

---

### Q74 — Defense Department: Risk Management

**Scenario:** The defense logistics modernization program has significant risks: technology complexity, coalition partner dependencies, security threats, and budget uncertainty.

**Your role:** Enterprise Architect.

**Question:** What is the correct approach to risk management?

- A. Identify risks once in Phase A and monitor them
- B. Risk management should be continuous across all ADM phases, with risk identification, classification, mitigation, and residual risk assessment at each phase
- C. Manage risks only in Phase F
- D. Delegate risk management to project managers

**Answer: B**

---

### Q75 — Federal Agency: Post-Implementation Review

**Scenario:** The benefits administration system is live. The project team is disbanding. The architecture team needs to capture lessons learned for future projects.

**Your role:** Enterprise Architect.

**Question:** Which ADM phase and activity applies?

- A. Phase H — manage ongoing changes
- B. Phase G — post-implementation review and close the implementation, documenting lessons learned
- C. Phase F — migration planning
- D. A new Phase A

**Answer: B**

---

## SECTION 6: Technology & Manufacturing Scenarios (Q76–90)

### Q76 — Cloud Service Provider: Infrastructure Architecture

**Scenario:** A cloud service provider is expanding to new regions. Each region must meet local data sovereignty laws while maintaining consistent service quality. The architecture team needs to define standard data center designs that can be adapted locally.

**Your role:** Enterprise Architect.

**Question:** What is the best approach to balancing consistency with local adaptation?

- A. Use Architecture Partitioning with a common foundation architecture and region-specific extensions managed through governance
- B. Design a single global data center design
- C. Let each region design independently
- D. Use only common systems without any customization

**Answer: A**

---

### Q77 — Cloud Provider: Architecture Repository

**Scenario:** Same cloud provider. The EA team is growing and needs to organize architecture assets for reuse across regions. They want to store reference architectures, standards, and governance records.

**Your role:** Enterprise Architect.

**Question:** Which six classes should be established in the Architecture Repository?

- A. Architecture Metamodel, Architecture Capability, Architecture Landscape, Standards Information Base, Reference Library, Governance Log
- B. Strategic, Tactical, Operational, Technical, Business, Data
- C. Current, Transition, Target, Baseline, Gap, Roadmap
- D. Foundation, Industry, Common Systems, Organization-Specific, Solutions, Deployed

**Answer: A**

---

### Q78 — Industrial Manufacturer: IoT Architecture

**Scenario:** A manufacturer of industrial equipment wants to add IoT capabilities to its products. Machines will send telemetry data for predictive maintenance. Customers are concerned about data privacy and intellectual property protection. The manufacturer has no software-as-a-service experience.

**Your role:** Enterprise Architect.

**Question:** What is the most important Phase A activity?

- A. Technology platform selection
- B. Architecture Vision development including stakeholder concerns about data privacy, security, and new business model implications
- C. Network architecture design
- D. Cloud provider selection

**Answer: B**

---

### Q79 — Industrial Manufacturer: Architecture Domains

**Scenario:** Same manufacturer. The IoT architecture spans embedded software, cloud platforms, mobile apps, and analytics. The architecture team is unsure how to organize the work.

**Your role:** Enterprise Architect.

**Question:** Which architecture domains should be covered?

- A. Only Technology Architecture since IoT is technical
- B. Business, Data, Application, and Technology — the IoT initiative affects business models, data flows, applications, and technology infrastructure
- C. Only Data and Technology
- D. Only Business and Technology

**Answer: B**

---

### Q80 — Semiconductor Company: Supply Chain Architecture

**Scenario:** A semiconductor company needs to redesign its supply chain to handle geopolitical risks. The current supply chain is concentrated in one region. The board wants diversification. The architecture must support multiple suppliers, different regulatory regimes, and logistics complexity.

**Your role:** Enterprise Architect.

**Question:** Which Phase B artifacts are most critical?

- A. Technology Portfolio catalog
- B. Business Capability Map, Value Stream maps, and Location catalog to understand current and target supply chain capabilities
- C. Data Entity catalog
- D. Application Communication diagram

**Answer: B**

---

### Q81 — Semiconductor Company: Architecture Principles

**Scenario:** Same semiconductor company. The board wants architecture principles that support resilience, compliance, and cost efficiency.

**Your role:** Enterprise Architect.

**Question:** Which architecture principles are most relevant?

- A. Data is an Asset, Data is Shared, Technology Independence
- B. Business Continuity, Compliance with Law, Interoperability, Common Use Applications, Data is Secure
- C. Maximize IT Value, Ease of Use, Responsive Change Management
- D. Information Management is Everybody's Business, IT Responsibility

**Answer: B**

---

### Q82 — Robotics Company: Reference Models

**Scenario:** A robotics company is integrating its robot control software with factory automation systems from multiple vendors. Each vendor uses different communication protocols and data formats.

**Your role:** Enterprise Architect.

**Question:** Which TOGAF reference model would help standardize the integration?

- A. III-RM — for enabling boundaryless information flow between systems
- B. TRM — for technology platform standardization
- C. Both — TRM for the technology platform architecture, III-RM for inter-system communication
- D. Neither — use vendor-specific solutions

**Answer: C**

---

### Q83 — Robotics Company: Iteration Strategy

**Scenario:** The robotics company is developing its first architecture. The team is new to TOGAF. The project is complex. They are unsure whether to attempt all domains at once.

**Your role:** Enterprise Architect.

**Question:** What iteration strategy is most appropriate?

- A. Complete all phases from Preliminary through H for all domains
- B. Use the ADM iteration cycles: start with Architecture Context, then iterate Architecture Definition through B, C, D for one domain at a time
- C. Only execute Phase D
- D. Skip iteration — use waterfall approach

**Answer: B**

---

### Q84 — Cloud Provider: Target Architecture

**Scenario:** The cloud provider's expansion architecture is complete. Implementation teams in different regions are starting to build. The architecture team needs to ensure regional implementations conform.

**Your role:** Enterprise Architect.

**Question:** Which phase ensures implementation conformance?

- A. Phase F — Migration Planning
- B. Phase G — Implementation Governance, with compliance reviews and Architecture Contracts
- C. Phase H — Architecture Change Management
- D. Requirements Management

**Answer: B**

---

### Q85 — Industrial Manufacturer: Technology Selection

**Scenario:** The IoT manufacturer needs to select cloud platform, IoT protocols, and analytics tools. Multiple viable options exist with different trade-offs in cost, scalability, and vendor lock-in.

**Your role:** Enterprise Architect.

**Question:** What is the correct approach to technology selection in Phase D?

- A. Choose the cheapest option
- B. Choose the most popular option
- C. Define technology principles and standards, evaluate options against architecture requirements, and document trade-offs for Architecture Board decision
- D. Let each product team choose independently

**Answer: C**

---

### Q86 — Semiconductor Company: Data Architecture

**Scenario:** The semiconductor company's supply chain redesign requires sharing sensitive design data with manufacturing partners. IP protection is critical. Different partners have different security capabilities.

**Your role:** Enterprise Architect.

**Question:** Which Phase C Data Architecture artifact is most relevant?

- A. Conceptual Data diagram
- B. Data Security diagram showing data classification, access controls, and data sharing boundaries with partners
- C. Data Lifecycle diagram
- D. Data Entity catalog

**Answer: B**

---

### Q87 — Robotics Company: Architecture Roadmap

**Scenario:** The robotics company has completed Phases A through D. The architecture definition is comprehensive. The program manager wants to know how to sequence implementation.

**Your role:** Enterprise Architect.

**Question:** What is the output of Phase E that addresses this?

- A. Architecture Vision
- B. Architecture Roadmap — showing work packages with sequencing, milestones, and Transition Architectures
- C. Architecture Contract
- D. Compliance Assessment

**Answer: B**

---

### Q88 — Cloud Provider: Continuity Planning

**Scenario:** The cloud provider's expansion has been approved. The CFO wants to understand when each new region will become profitable. The COO wants to know resource requirements.

**Your role:** Enterprise Architect.

**Question:** Which Phase F deliverable addresses these concerns?

- A. Architecture Vision
- B. Implementation and Migration Plan (v1.0) — with resource estimates, cost/benefit analysis, and prioritized work packages
- C. Compliance Assessment
- D. Architecture Principles

**Answer: B**

---

### Q89 — Industrial Manufacturer: Phase H Strategy

**Scenario:** The IoT platform is operational. The CTO wants to ensure the architecture evolves with new technologies without requiring a full redesign each time.

**Your role:** Enterprise Architect.

**Question:** What should be established in Phase H?

- A. A new Architecture Vision
- B. Change management processes, value realization monitoring, and governance for classifying changes as simplification, incremental, or re-architecting
- C. A new Preliminary Phase
- D. Implementation plan for next release

**Answer: B**

---

### Q90 — Semiconductor Company: Risk Management

**Scenario:** The semiconductor supply chain architecture involves multiple countries, suppliers, logistics providers, and regulatory regimes. Risks include geopolitical disruption, supplier bankruptcy, and regulatory changes.

**Your role:** Enterprise Architect.

**Question:** How should risk management be integrated into the ADM?

- A. As a standalone activity outside the ADM
- B. Throughout all ADM phases — risk identification in each phase, classification by effect and frequency, mitigation planning, and residual risk acceptance
- C. Only in Phase F during migration planning
- D. Only in Phase A during initial assessment

**Answer: B**

---

## SECTION 7: Cross-Industry & Governance Scenarios (Q91–100)

### Q91 — Supermarket Chain: Digital Transformation

**Scenario:** A regional supermarket chain with 200 stores is facing competition from online retailers. They need to implement online ordering, home delivery, and loyalty programs. Each store currently operates semi-independently with different POS systems. The company has no EA practice.

**Your role:** Enterprise Architect (newly hired).

**Question:** What is the most important first step?

- A. Implement an e-commerce platform immediately
- B. Execute the Preliminary Phase to establish architecture principles, governance framework, and EA capability
- C. Create a detailed project plan
- D. Hire a system integrator

**Answer: B**

---

### Q92 — Supermarket Chain: Architecture Principles

**Scenario:** Same supermarket chain. The newly formed Architecture Board is defining architecture principles. The CMO wants principles that enable rapid digital innovation. The CFO wants cost control. The COO wants operational stability.

**Your role:** Enterprise Architect.

**Question:** What are essential characteristics of good architecture principles?

- A. They are specific, measurable, and technology-focused
- B. They are understandable, robust, complete, consistent, and stable, with clear rationale and implications
- C. They are flexible and changed frequently
- D. They address only IT concerns

**Answer: B**

---

### Q93 — Cybersecurity Company: Zero Trust Architecture

**Scenario:** A cybersecurity company is designing a zero-trust architecture for a large enterprise customer. The customer has legacy systems that cannot support modern authentication. The project involves network segmentation, identity management, and continuous monitoring. Stakeholders include the CISO (wants maximum security), CIO (worried about user productivity), and CFO (concerned about cost).

**Your role:** Lead Architect.

**Question:** Which approach best addresses all stakeholder concerns?

- A. Implement maximum security regardless of impact
- B. Prioritize user productivity over security
- C. Develop architecture viewpoints for each stakeholder group showing how the zero-trust architecture addresses their specific concerns, make trade-offs visible, and iterate until consensus
- D. Focus only on the CISO's requirements

**Answer: C**

---

### Q94 — Cybersecurity Company: Compliance Level

**Scenario:** Same cybersecurity project. During Phase G compliance review, the network team has implemented all specified security controls except one — they are using hardware-based MFA instead of the specified software-based MFA. Hardware MFA meets the same security objective.

**Your role:** Lead Architect.

**Question:** How should compliance be described?

- A. Conformant — the security objective is met
- B. Non-conformant — the implementation does not follow the specification; should request dispensation
- C. Consistent — equivalent functionality
- D. Irrelevant — MFA method is a minor detail

**Answer: B**

---

### Q95 — Energy Company: Net-Zero Architecture

**Scenario:** A multinational energy company is transitioning to net-zero emissions through acquisitions of renewable energy startups. Each startup has different technology stacks, cultures, and data standards. The company has a mature EA practice.

**Your role:** Chief Enterprise Architect.

**Question:** Which TOGAF concept helps classify and reuse architecture assets from acquisitions?

- A. ADM
- B. Enterprise Continuum — classifying acquired architectures from organization-specific to common systems for reuse
- C. Architecture Content Framework
- D. Architecture Governance Framework

**Answer: B**

---

### Q96 — Energy Company: Business Scenario

**Scenario:** Same energy company. The newly acquired solar analytics startup has developed innovative modeling software. The CTO of the parent company wants to understand how this software fits the overall enterprise architecture.

**Your role:** Chief Enterprise Architect.

**Question:** What technique helps understand the business context?

- A. Gap Analysis
- B. Business Scenarios — capturing business goals, processes, actors, and information needs of the combined enterprise
- C. Interoperability Analysis
- D. Risk Assessment

**Answer: B**

---

### Q97 — Multinational Conglomerate: Global vs Local

**Scenario:** A multinational conglomerate with businesses in food, chemicals, and logistics operates in 80 countries. Each business unit and region has different regulatory requirements. The corporate center wants global efficiency. Business units need local flexibility.

**Your role:** Chief Enterprise Architect.

**Question:** How should the Architecture Landscape be structured?

- A. Single global landscape
- B. Partitioned by business segment and region, with a common foundation architecture for shared services and local extensions for specific requirements
- C. Independent landscapes for each business
- D. Technology landscape only

**Answer: B**

---

### Q98 — Multinational Conglomerate: Governance

**Scenario:** Same conglomerate. The corporate Architecture Board must govern architectures across diverse businesses. Food, chemicals, and logistics have very different regulatory and operational requirements.

**Your role:** Chief Enterprise Architect.

**Question:** What governance approach is most appropriate?

- A. Single centralized Architecture Board for all decisions
- B. Federated governance — corporate-level Board sets enterprise-wide principles and standards; business-level boards handle domain-specific decisions
- C. No corporate governance
- D. Each business unit has its own independent board

**Answer: B**

---

### Q99 — Consulting Firm: Architecture Skills

**Scenario:** A consulting firm is building an EA practice. They need to hire architects, define career paths, and assess capability gaps. The managing partner asks what skills are needed.

**Your role:** EA Practice Lead.

**Question:** Which TOGAF framework defines architecture skills, roles, and responsibilities?

- A. Architecture Content Framework
- B. Architecture Capability Framework — including the Architecture Skills Framework
- C. Enterprise Continuum
- D. ADM

**Answer: B**

---

### Q100 — Consulting Firm: Capability Maturity

**Scenario:** Same consulting firm. After one year of operation, the managing partner wants to assess how mature the EA practice has become and identify areas for improvement.

**Your role:** EA Practice Lead.

**Question:** Which TOGAF model should be used?

- A. TRM
- B. III-RM
- C. Architecture Capability Maturity Model (ACMM) to assess the architecture process, governance, stakeholder involvement, and other dimensions
- D. Gap Analysis

**Answer: C**

---

## Quick Reference: Scenario Patterns

| Scenario Type | Key TOGAF Concepts Tested |
|---------------|--------------------------|
| **New EA practice** | Preliminary Phase, tailoring, architecture principles, maturity assessment |
| **Multi-stakeholder conflict** | Stakeholder management, views/viewpoints, communications plan |
| **Security/compliance** | Security in all phases, SIB, compliance reviews, governance |
| **Legacy modernization** | Transition Architectures, Phase E/F, migration planning |
| **M&A / integration** | Enterprise Continuum, partitioning, Phase G contracts |
| **Global vs local** | Partitioning, governance framework, dispensations |
| **Regulatory change** | Phase H, Requirements Management, change classification |
| **Implementation conformance** | Phase G, compliance assessment, Architecture Contracts |
| **Risk management** | Continuous across all phases, Business Transformation Readiness |
| **Agile alignment** | Phase G compliance reviews at sprint boundaries |

---

*Compiled from: OG0-092/OGEA-102 exam dumps (ITExams, ExamTopics), GitHub repos (xde013/togaf, Gana-Dube/togaf-exam-hub, sutharsuresh/togaf-part-2), and original scenarios based on real exam patterns.*
