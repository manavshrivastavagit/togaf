# Phase C: Application Architecture - Microservices Portfolio

This document details the microservices topology, individual service specifications, technology stacks, container configurations, and default resource allocations for the digital lending platform.

---

## 1. Microservice Catalog & Port Map

The system is split into 6 core domain microservices running inside an Istio Service Mesh on Kubernetes.

```
                  ┌──────────────────────┐
                  │   API Gateway (Kong)  │
                  └──────────┬───────────┘
                             │ (Routing)
      ┌──────────────────────┼───────────────────────┐
      ▼                      ▼                       ▼
┌──────────────┐      ┌──────────────┐       ┌──────────────┐
│Go Onboarding │      │ Node Consent │       │ FastAPI      │
│Service       │      │ Service      │       │ Underwriting │
│Port: 8080    │      │ Port: 8081   │       │ Port: 8000   │
└──────┬───────┘      └──────┬───────┘       └──────┬───────┘
       │                     │                      │
       └──────────────┬──────┴──────────────────────┘
                      ▼ (Internal Event Bus / Kafka)
┌──────────────┐      ┌──────────────┐       ┌──────────────┐
│Go Payments   │◄─────┤ Spring Boot  │◄──────┤ Node         │
│Service       │      │ Fineract     │       │ Notification │
│Port: 8082    │      │ Ledger Port: │       │ Port: 8083   │
└──────────────┘      │ 8085         │       └──────────────┘
                      └──────────────┘
```

| Service Name | Tech Stack | Exposed Port | Database Backend | Core Responsibility |
| :--- | :--- | :--- | :--- | :--- |
| **Go Onboarding** | Go 1.20 (Gin, GORM) | `8080` | PostgreSQL (Customer DB) | Customer registration, PAN/Aadhaar vault matching, KYC verification. |
| **Node Consent** | Node.js (Express, TypeScript) | `8081` | MongoDB (Consent JSON DB) | Account Aggregator handshakes, signed consent validations, webhook handlers. |
| **FastAPI Underwriting** | Python 3.10 (FastAPI, NumPy) | `8000` | PostgreSQL (Risk Metadata) | Bureau queries, bank statement parser, ML model scoring, risk calculations. |
| **Spring Boot Fineract Ledger** | Java 17 (Spring Boot, Fineract) | `8085` | PostgreSQL (Core Ledger) | Double-entry bookkeeping, interest accruals, loan accounts, balances. |
| **Go Payments** | Go 1.20 (Echo) | `8082` | PostgreSQL (Txn Outbox DB) | NPCI eNACH registration, UPI AutoPay triggers, bank payout gateway integrations. |
| **Node Notifications** | Node.js (NestJS, TypeScript) | `8083` | Redis Cache (Queues) | Dispatch of transactional updates (SMS, Email, WhatsApp) via Firebase. |

---

## 2. Service Specifications

### A. Go Onboarding Service
* **Tech Stack:** Go, Gin Framework, pgx driver.
* **Health Probes:** `/healthz/live` (port 8080), `/healthz/ready`.
* **State Management:** Talks to Aadhaar Vault HSM via local gRPC link.

### B. Node Consent Service
* **Tech Stack:** TypeScript, Express, Axios.
* **Security Context:** Digitally signs all requests using a key loaded from KMS.
* **AA Schema:** Enforces ReBIT-compliant schemas for all FIP payload validation.

### C. FastAPI Underwriting Service
* **Tech Stack:** Python, FastAPI, Pydantic, Scikit-learn.
* **Workers:** Uvicorn with 4 worker processes.
* **Dependencies:** Requires read-only access to MongoDB (via internal service routing) to parse retrieved consent financial data.

### D. Spring Boot Fineract Core Ledger
* **Tech Stack:** Spring Boot, JPA/Hibernate, Liquibase, Apache Fineract Core.
* **JVM Settings:** `-XX:MaxRAMPercentage=75.0 -XX:+UseG1GC`.
* **Reliability:** Transactions run with `@Transactional(isolation = Isolation.SERIALIZABLE)`.

### E. Go Payments Service
* **Tech Stack:** Go, Kafka-go writer, HTTP client with Circuit Breaker (Hystrix-Go).
* **Integrations:** Direct API gateway endpoints to Sponsor Banks (ICICI/HDFC) for IMPS/NEFT payouts.

### F. Node Notifications Service
* **Tech Stack:** NestJS, BullMQ (Redis-based queue), Firebase Admin SDK.
* **Resilience:** Auto-retry with exponential backoff on notification failures.

---

## 3. Kubernetes Deployment Blueprint

Below is the standard K8s deployment template applied across the portfolio, ensuring consistent resource boundaries, sidecars, and monitoring hooks.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: onboarding-service
  namespace: private-app
  labels:
    app: onboarding-service
    tier: application
spec:
  replicas: 3
  selector:
    matchLabels:
      app: onboarding-service
  template:
    metadata:
      labels:
        app: onboarding-service
      annotations:
        sidecar.istio.io/inject: "true" # Mesh integration
        prometheus.io/scrape: "true"
        prometheus.io/port: "8080"
        prometheus.io/path: "/metrics"
    spec:
      containers:
        - name: app
          image: 123456789012.dkr.ecr.ap-south-1.amazonaws.com/lending/onboarding-service:v1.2.4
          imagePullPolicy: IfNotPresent
          ports:
            - containerPort: 8080
              name: http
          envFrom:
            - configMapRef:
                name: onboarding-config
            - secretRef:
                name: onboarding-secrets
          resources:
            requests:
              memory: "512Mi"
              cpu: "250m"
            limits:
              memory: "1024Mi"
              cpu: "1000m"
          readinessProbe:
            httpGet:
              path: /healthz/ready
              port: 8080
            initialDelaySeconds: 10
            periodSeconds: 5
            timeoutSeconds: 2
            failureThreshold: 3
          livenessProbe:
            httpGet:
              path: /healthz/live
              port: 8080
            initialDelaySeconds: 15
            periodSeconds: 10
            timeoutSeconds: 2
            failureThreshold: 3
          securityContext:
            allowPrivilegeEscalation: false
            readOnlyRootFilesystem: true
            runAsNonRoot: true
            runAsUser: 10001
            capabilities:
              drop:
                - ALL
---
apiVersion: v1
kind: Service
metadata:
  name: onboarding-service
  namespace: private-app
spec:
  ports:
    - port: 8080
      targetPort: 8080
      protocol: TCP
      name: http
  selector:
    app: onboarding-service
```
