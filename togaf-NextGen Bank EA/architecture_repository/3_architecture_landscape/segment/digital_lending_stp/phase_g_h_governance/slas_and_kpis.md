# TOGAF Phase G & H: Operational SLAs & Key Performance Indicators (KPIs)

This document establishes the system performance targets, business metrics, and concrete Prometheus/Grafana configurations required to monitor and maintain the health of NextGen Bank's **Straight-Through Processing (STP) Micro-Loan Mobile Platform**.

---

## 1. Service Level Agreement (SLA) & KPI Targets

To ensure a premium customer experience and secure risk management, the platform operates under strict SLAs categorized into technical performance and business operations.

### 1.1 Technical Performance SLAs

| Metric Category | Specific KPI | SLA Target | Measurement Window | Escalation Pathway |
| :--- | :--- | :--- | :--- | :--- |
| **API Latency** | P95 Response Latency (Internal Microservices). | **< 200ms** | 5-minute rolling average. | Alert to Team Lead (On-Call Engineer). |
| **Gateway Latency** | P99 Response Latency (Kong API Gateway Edge). | **< 500ms** | 5-minute rolling average. | Alert to Platform Team (Priority 1). |
| **System Uptime** | API Gateway and Core Microservices Availability. | **99.95%** | Monthly aggregate. | Immediate CTO notification if breach occurs. |
| **Database Load** | CPU Utilization of PostgreSQL RDS. | **< 70%** | 10-minute average. | Autoscale database read replicas. |
| **Queue Processing** | Kafka Message Lag. | **< 100 messages** | Per partition, real-time. | Trigger autoscale of consumer pods. |

### 1.2 Integration SLAs (External Partners)

| Integration Partner | Target Latency (P95) | Max Allowed Error Rate | Timeout Threshold | Fallback Action |
| :--- | :--- | :--- | :--- | :--- |
| **UIDAI (e-KYC)** | < 1,500ms | < 2% | 3,000ms | Retry once; fallback to manual document upload (TA-1 only) or automated delay notification screen. |
| **Decentro (AA)** | < 2,500ms (fetch data) | < 3% | 5,000ms | Display "Processing Bank Statement..." and poll asynchronously in background. |
| **CIBIL (Bureau)** | < 3,000ms | < 1% | 6,000ms | Fallback to secondary Bureau (Experian) API call. |
| **NeSL (e-Sign)** | < 2,000ms | < 2% | 4,000ms | Send contract link via SMS for execution in browser session. |
| **Sponsor Bank** | < 1,200ms (disbursal API)| < 0.5% | 2,500ms | Mark disbursal as "Pending"; queue for auto-retry via secondary sponsor bank gateway. |

### 1.3 Business Operations KPIs

| Metric Name | Formula / Definition | Target Value | Monitoring Priority |
| :--- | :--- | :--- | :--- |
| **STP Ratio** | $\frac{\text{Loans completed with 0 manual steps}}{\text{Total loans disbursed}}$ | **100%** (Target State) | High (Platform health indicator). |
| **End-to-End TAT** | Time from OTP login to funds hitting client bank account. | **< 5 Minutes** | High (Customer experience indicator). |
| **Funnel Drop-off Rate**| Percentage of users exiting onboarding at each step. | **< 25%** | Medium (UX optimization indicator). |
| **First Payment Default**| $\frac{\text{Loans defaulting on the 1st installment}}{\text{Total loans disbursed in cohort}}$ | **< 1.5%** | Critical (Risk model accuracy). |
| **Mandate Success Rate**| $\frac{\text{Successful AutoPay debits}}{\text{Total debit requests on billing date}}$ | **> 92%** | High (Servicing efficiency). |

---

## 2. Operational Dashboards: Prometheus & Grafana Mappings

Operational metrics are collected using Prometheus client libraries embedded in the microservices and visualized on Grafana dashboards.

### 2.1 Prometheus Metrics Schema

```
┌───────────────────────┐      Prometheus Scraping      ┌────────────────────────┐
│   Spring Boot / Go    │──────────────────────────────►│   Prometheus Server    │
│  Microservices APIs   │     (Pulls /metrics path)     └────────────────────────┘
└───────────────────────┘                                           │
                                                                    ▼ Visualizes
                                                        ┌────────────────────────┐
                                                        │   Grafana Dashboard    │
                                                        └────────────────────────┘
```

The following core metrics are registered on the platform:

1. **HTTP Request Duration**:
   * **Name**: `http_request_duration_seconds`
   * **Labels**: `method`, `handler`, `status`
   * **Description**: Tracks latency of API endpoints.
2. **Loan Disbursal Performance**:
   * **Name**: `lms_loan_disbursals_total`
   * **Labels**: `status` (success, failed, pending), `bank` (sponsor_a, sponsor_b)
   * **Description**: Tracks loan volume and disbursal channel health.
3. **Underwriting Execution Latency**:
   * **Name**: `underwriting_decision_duration_seconds`
   * **Labels**: `decision` (approve, reject, review)
   * **Description**: Tracks the turnaround execution speed of the Python credit scoring models.
4. **Consent Request Count**:
   * **Name**: `consent_requests_total`
   * **Labels**: `status` (created, approved, expired, revoked)
   * **Description**: Tracks consent lifecycle.

### 2.2 Prometheus Alerting Rules (`alerts.rules.yml`)
The Prometheus Alertmanager is configured with the following threshold rules:

```yaml
groups:
  - name: API_Alerts
    rules:
      - alert: HighAPILatency
        expr: histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le)) > 0.200
        for: 2m
        labels:
          severity: warning
        annotations:
          summary: "P95 API latency exceeds 200ms"
          description: "Current P95 latency is {{ $value }}s on service."

      - alert: DisbursalFailures
        expr: sum(rate(lms_loan_disbursals_total{status="failed"}[5m])) > 2
        for: 1m
        labels:
          severity: critical
        annotations:
          summary: "Loan disbursal failures detected"
          description: "Disbursal failure rate has exceeded 2 failed attempts in the last minute."

      - alert: ConsentDropOff
        expr: (sum(rate(consent_requests_total{status="expired"}[10m])) / sum(rate(consent_requests_total{status="created"}[10m]))) * 100 > 30
        for: 5m
        labels:
          severity: warning
        annotations:
          summary: "High consent drop-off rate detected"
          description: "Consent expiration is {{ $value }}%, indicating friction in the Account Aggregator flow."
```

### 2.3 Grafana Dashboard Panels Configuration

#### Panel 1: End-to-End Processing Latency (Heatmap)
* **Title**: API Gateway Latency Distribution (P95/P99)
* **PromQL Query**:
  ```promql
  histogram_quantile(0.95, sum(rate(http_request_duration_seconds_bucket[5m])) by (le, handler))
  ```
* **Visualization Type**: Time Series (Line graph showing trend over 24 hours, with green-yellow-red threshold lines at 200ms and 500ms).

#### Panel 2: Real-time Disbursal Funnel (Gauge)
* **Title**: Disbursal Success Rate (%)
* **PromQL Query**:
  ```promql
  sum(rate(lms_loan_disbursals_total{status="success"}[5m])) / sum(rate(lms_loan_disbursals_total[5m])) * 100
  ```
* **Visualization Type**: Gauge (Target: green range 99.5% - 100%; warning: yellow 98% - 99.5%; critical: red < 98%).

#### Panel 3: Account Aggregator Status Monitor (Bar Chart)
* **Title**: Consent Transactions State
* **PromQL Query**:
  ```promql
  sum(increase(consent_requests_total[1h])) by (status)
  ```
* **Visualization Type**: Bar Chart (Visualizes status states: `created`, `approved`, `expired`, `revoked` side-by-side).

---

## 3. References & Linked Artifacts

* **Gap Analysis & Solutions**: [gap_analysis_and_solutions.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/gap_analysis_and_solutions.md)
* **Transition Architectures**: [transition_architectures.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_e_f_migration/transition_architectures.md)
* **Compliance Guidelines**: [compliance_guidelines.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/compliance_guidelines.md)
* **Change Management Governance**: [change_management_governance.md](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/3_architecture_landscape/segment/digital_lending_stp/phase_g_h_governance/change_management_governance.md)
