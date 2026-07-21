# TOGAF Phase E & F: Total Cost of Ownership (TCO) & Financial Model

This document establishes the financial feasibility model, transaction-level operational expenditures (OPEX), and cloud infrastructure capital expenditures (CAPEX) for NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform**.

---

## 1. Granular Unit Cost per Loan Cycle (OPEX)

Unlike traditional branch lending where costs are aggregated under fixed overheads, the digital lending platform operates on a variable, transaction-driven cost structure. Every integration call to the India Stack and SaaS providers incurs a direct charge.

### 1.1 Transaction-Level Cost Breakdown
The table below tracks a single loan from onboarding to final collections.

| Life Cycle Phase | Integration Activity | Provider / Utility | Charge Type | Cost (INR) |
| :--- | :--- | :--- | :--- | :--- |
| **Onboarding** | PAN Verification | Income Tax Department API via NSDL | Per fetch | ₹1.00 |
| **Onboarding** | Aadhaar e-KYC | UIDAI via KUA / AUA API | Per fetch | ₹3.00 |
| **Onboarding** | Biometric Liveness | SaaS SDK (e.g., HyperVerge / Signzy) | Per transaction | ₹5.00 |
| **Underwriting** | Credit Bureau Query | TransUnion CIBIL / Experian | Per pull | ₹12.00 |
| **Underwriting** | Bank Statement Parsing | Account Aggregator via Decentro / Perfios | Per consent fetch | ₹6.00 |
| **Execution** | Contract Execution | NeSL / NSDL e-Sign Gateway | Per document | ₹18.00 |
| **Execution** | Auto-Debit Registration | NPCI e-Mandate / Sponsor Bank | Per setup | ₹5.00 |
| **Disbursal** | Disbursal Settlement | IMPS / UPI transfer via Sponsor Bank | Per transfer | ₹1.50 |
| **Collection** | Monthly Repayment Pull | NPCI UPI AutoPay / eNACH | Per debit attempt | ₹1.00 |
| **Servicing** | Alerts & Communication | SMS Gateway / WhatsApp Business API | Total per cycle | ₹3.00 |
| **Total Origination** | — | **Single Loan Onboarding & Execution** | **Flat OPEX** | **₹54.50** |

*Note: For a 6-month loan, monthly auto-pay pull costs ₹6.00 (6 x ₹1.00), bringing the lifetime variable transactional cost of the loan to **₹59.50**.*

---

## 2. Infrastructure Overhead at Scale (Projected)

To run the microservices, databases, and gateways, cloud hosting overhead is computed at an expected volume of **50,000 active loans processed per month**.

### 2.1 AWS Hosting Cost Model (Monthly)
The cloud infrastructure is hosted in the AWS Mumbai region to satisfy RBI localization mandates.

| Component | AWS Service | Sizing Details | Monthly Cost (USD) | Monthly Cost (INR @ ₹83) |
| :--- | :--- | :--- | :--- | :--- |
| **Compute** | Amazon EKS | 3 Nodes (m6i.xlarge) + Master | $550.00 | ₹45,650.00 |
| **Database** | Amazon RDS (Multi-AZ) | db.r6g.xlarge (PostgreSQL / MySQL) | $780.00 | ₹64,740.00 |
| **Cache & Queue** | Amazon ElastiCache + MSK | Redis cluster + Managed Kafka | $420.00 | ₹34,860.00 |
| **Security & Gateway**| AWS WAF + API Gateway | WAF Rules + 3M requests | $310.00 | ₹25,730.00 |
| **Secrets & Keys** | AWS KMS + Secrets Manager | envelope encryption + secret storage| $150.00 | ₹12,450.00 |
| **Logs & Metrics** | Amazon CloudWatch | 500 GB ingestion + dashboard | $280.00 | ₹23,240.00 |
| **Total Hosting** | — | **AWS Infrastructure Subtotal** | **$2,490.00** | **₹206,670.00** |

### 2.2 Infrastructure Cost per Loan Unit
At the baseline volume of 50,000 loans/month:
$$\text{Infrastructure Cost per Loan} = \frac{\text{Monthly Hosting Cost}}{\text{Monthly Loan Volume}} = \frac{\text{₹}206,670}{50,000} \approx \mathbf{\text{₹}4.13 \text{ per loan}}$$

At higher scaling limits (e.g., 200,000 loans/month), automated Kubernetes scaling optimizes node density, reducing this overhead to less than **₹1.50 per loan**.

---

## 3. Financial Performance Comparison (Branch vs. Digital)

A detailed comparison between the traditional branch-based lending model and the target digital mobile platform highlights the financial advantages of automation.

### 3.1 Unit Cost Comparison

| Expense Category | Traditional Branch Model | Target Digital Platform | Cost Saving | Rationale / Detail |
| :--- | :--- | :--- | :--- | :--- |
| **Customer Acquisition** | ₹1,200.00 | ₹150.00 | 87.5% | Branch staff commissions and physical marketing vs. digital programmatic ads. |
| **Identity Verification** | ₹350.00 | ₹9.00 | 97.4% | Physical travel and manual document verification vs. Aadhaar e-KYC & liveness API. |
| **Credit Underwriting** | ₹450.00 | ₹18.00 | 96.0% | Risk officer salaries & worksheet calculations vs. automated CIBIL/AA scoring engine. |
| **Legal Documentation** | ₹150.00 | ₹18.00 | 88.0% | Paper agreement stamps, scanning, archiving vs. NeSL e-Sign and PDF generation. |
| **Disbursal & Collection**| ₹200.00 | ₹12.50 | 93.7% | Manual teller execution and collection agency fees vs. instant API and UPI AutoPay. |
| **Fixed Cost Overhead** | ₹150.00 | ₹4.13 | 97.2% | Branch rent, utilities, hardware depreciation vs. cloud-native hosting overhead. |
| **Total Origination Cost**| **₹2,500.00** | **₹211.63** | **91.5%** | **Massive structural cost reduction enabling small-ticket viability.** |

---

## 4. Cost-Benefit & ROI Projection (50,000 Loans/Month Scale)

To justify the initial platform capital expenditure (CAPEX), the following table models the financial returns over a 3-year period.

### 4.1 Initial Development CAPEX
* **Software Development & Integration**: ₹1,80,00,000 ($216k USD) (WP-01 to WP-03 development costs).
* **Security & Regulatory Audits**: ₹20,00,000 ($24k USD) (WP-04 certification audits).
* **Total CAPEX**: **₹2,00,000,000 ($240k USD)**.

### 4.2 Financial Projection Model (Annualized)

| Metric | Year 1 | Year 2 | Year 3 |
| :--- | :--- | :--- | :--- |
| **Active Loan Volume** | 3,00,000 | 6,00,000 | 12,00,000 |
| **Digital Execution Costs (OPEX)** | ₹6,34,89,000 | ₹12,69,78,000 | ₹25,39,56,000 |
| **Equivalent Branch Costs (OPEX)** | ₹75,00,00,000 | ₹1,50,00,00,000 | ₹3,00,00,00,000 |
| **Gross Operational Savings** | ₹68,65,11,000 | ₹1,37,30,22,000 | ₹2,74,60,44,000 |
| **Amortized CAPEX Allocation** | ₹2,00,00,000 | — | — |
| **Net Financial Savings** | **₹66,65,11,000** | **₹1,37,30,22,000** | **₹2,74,60,44,000** |
| **Platform Payback Period** | **3.5 Months** | — | — |

### 4.3 Strategic Financial Impact
1. **Net Interest Margin (NIM) Optimization**: By lowering transaction costs by over 91%, the bank can profitably offer loans at lower interest rates, capturing market share without eroding NIM.
2. **Moratorium and Default Tolerance**: The massive savings in transaction costs allow the bank to absorb higher default tolerances (up to 5% instead of the typical 2%) on small-ticket micro-loans while maintaining profitability.
3. **Return on Assets (ROA)**: Since the assets (loans) are originated and serviced without adding physical brick-and-mortar assets (branches, IT hardware), the bank's asset turnover increases, boosting overall ROA.

---

## 5. References & Linked Artifacts

* **Gap Analysis & Solutions**: [gap_analysis_and_solutions.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md)
* **Transition Architectures**: [transition_architectures.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md)
* **Migration Roadmap**: [migration_roadmap.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/migration_roadmap.md)
* **Compliance Guidelines**: [compliance_guidelines.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/compliance_guidelines.md)
