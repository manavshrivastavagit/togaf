# TOGAF Phase H: Architecture Change Management & Governance

This document establishes the governance framework, change classifications, Architecture Review Board (ARB) operational procedures, and templates for requesting architecture modifications on NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform**.

---

## 1. Architecture Change Classification Matrix

Any modification to the platform architecture must be classified according to the scale of impact. The classification determines the required level of review, approval, and documentation.

| Change Classification | Definition | Examples | Governance & Approval Path |
| :--- | :--- | :--- | :--- |
| **Minor Change** | Localized modifications with no impact on external service integrations, system boundaries, or data contracts. | * Upgrading Redis cache patch version.<br>* Adjusting risk engine scoring coefficients.<br>* Adding a database index to improve lookup speed. | * **Approved by**: Development Team Lead.<br>* **Documentation**: Logged in Git commit messages; updated local inline comments. |
| **Major Change** | Modifications that alter interfaces between internal microservices, modify central databases, or change integrations. | * Changing the e-Sign gateway provider (e.g., NSDL to NeSL).<br>* Modifying shared JSON payload schemas in Kafka.<br>* Changing user authentication mechanisms in Keycloak. | * **Approved by**: Enterprise Architect and CISO.<br>* **Documentation**: Requires formal Request for Change (RFC) submission; updates to [architecture_requirements_specification.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/architecture_requirements_specification.md). |
| **Strategic Change** | Structural shifts affecting business capabilities, core platforms, regulatory compliance, or cloud infrastructure. | * Replacing Finflux LMS with an in-house double-entry ledger.<br>* Migrating cloud provider (e.g., AWS to Microsoft Azure).<br>* Restructuring direct fund flows to introduce a co-lending partner. | * **Approved by**: Full Architecture Review Board (ARB) and CTO.<br>* **Documentation**: RFC submission, formal board presentation, and complete update to all TOGAF blueprints and [preliminary_and_phase_a_vision.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/preliminary_and_phase_a_vision.md). |

---

## 2. Request for Change (RFC) Template

All **Major** and **Strategic** changes must be initiated using this standard template.

```markdown
# Request for Architecture Change (RFC) - RFC-[YYYY]-[NUMBER]

## 1. General Information
* **RFC ID**: RFC-2026-001 (Format: RFC-[YYYY]-[Sequential No.])
* **Title**: [Brief title of the change]
* **Requester Name / Team**: [e.g., Lead Engineer - Ledger Team]
* **Submission Date**: [YYYY-MM-DD]
* **Change Classification**: [Major / Strategic]
* **Target Release Date**: [YYYY-MM-DD]

## 2. Description and Rationale
* **Detailed Description of Change**: 
  [Explain what is being changed. Include target services, database schemas, or infrastructure assets.]
* **Reason for Change**: 
  [Explain the business, technical, or regulatory driver. For example, API deprecation, performance bottlenecks, or new compliance laws.]
* **Impact of Not Implementing**: 
  [Describe the risk or cost of maintaining the status quo.]

## 3. Architecture Domain Impact Analysis
* **Business Architecture**: [Describe impact on business processes, customer journey, or operations.]
* **Data Architecture**: [Describe changes to schemas, PII storage, consent, and encryption keys.]
* **Application Architecture**: [Describe impact on microservices, API Gateway routing, and message brokers.]
* **Technology Architecture**: [Describe impact on Kubernetes deployments, hosting costs, and HSMs.]

## 4. Risk Assessment & Safety Gateways
* **Risk Score**: [Calculate: Probability (1-5) x Impact (1-5)]
* **Key Risks Identified**: 
  1. [Risk description - e.g., temporary API latency spike during migration.]
* **Mitigation Strategy**: 
  1. [Mitigation - e.g., perform migration during low-traffic window (2:00 AM - 4:00 AM).]
* **Rollback Plan**: 
  [Detailed step-by-step instructions to revert to the previous state in case of failure.]

## 5. Test & Validation Plan
* **Integration Testing**: [Define test cases to validate the change in staging environment.]
* **Regression Testing**: [Verify that existing microservices are not broken by the release.]
* **Compliance Validation**: [Specify which checklist item in compliance_guidelines.md must be verified.]

## 6. Review & Approvals (Sign-offs)
* [ ] **Enterprise Architect**: Approve / Reject / Date: _________
* [ ] **Chief Information Security Officer (CISO)**: Approve / Reject / Date: _________
* [ ] **Compliance Officer (RBI/DPDP)**: Approve / Reject / Date: _________
* [ ] **DevOps/Ops Lead**: Approve / Reject / Date: _________
```

---

## 3. Architecture Review Board (ARB) Procedures

The ARB maintains the structural integrity of the NextGen Bank digital lending platform.

### 3.1 Board Composition (Quorum)
To conduct an official ARB session and approve changes, the following roles must be present (minimum quorum: 4 members):
* **Chairperson**: Enterprise Architect (EA)
* **Technical Representatives**: Lead Developers from each of the 3 stream-aligned teams (Onboarding, Risk, Ledger)
* **Security representative**: Chief Information Security Officer (CISO) or designated Security Lead
* **Business representative**: Head of Digital Lending Unit (DLU) or product proxy

### 3.2 Review Lifecycle
```
[1. Draft RFC] ──► [2. Submit to Repo] ──► [3. ARB Meeting Review]
                                                │
       ┌────────────────────────────────────────┴────────────────────┐
       ▼                                                             ▼
[Approved] ──► [Deploy & Document]                            [Deferred / Rejected] ──► [Revise]
```

1. **Submission**: The requester drafts the RFC in markdown and commits it to the central `/architecture/rfcs/` folder via a pull request.
2. **Scheduled Review**:
   * **Major Changes**: Reviewed during the weekly ARB meeting (held every Thursday at 3:00 PM).
   * **Strategic Changes**: Requires an ad-hoc ARB session scheduled with at least 5 business days' notice to allow pre-reading.
3. **Evaluation Guidelines**: The board evaluates the RFC against:
   * Architectural Principles (STP-first, API-first, Privacy by design).
   * Security vulnerabilities and performance latency overhead.
   * Unit cost impact (to ensure compliance with the [tco_financial_model.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/tco_financial_model.md)).
4. **Outcome Logging**: The decision (Approved, Rejected, or Deferred for modifications) is recorded in the RFC file metadata. The pull request is merged to maintain an audit trail.

---

## 4. Post-Implementation Review (PIR)

For all Strategic Changes, a Post-Implementation Review (PIR) must be conducted **15 days after deployment**:
1. **Performance Audit**: Compare actual API latency, CPU load, and transaction failure rates against target metrics defined in the RFC.
2. **Financial Verification**: Audit transaction costs to ensure no unforeseen SaaS API overhead was introduced.
3. **Lessons Learned**: Log any operational incidents or unexpected behavior during the deployment window to improve the next migration cycle.

---

## 5. References & Linked Artifacts

* **Gap Analysis & Solutions**: [gap_analysis_and_solutions.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md)
* **Transition Architectures**: [transition_architectures.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md)
* **Compliance Guidelines**: [compliance_guidelines.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/compliance_guidelines.md)
* **SLAs and KPIs**: [slas_and_kpis.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/slas_and_kpis.md)
