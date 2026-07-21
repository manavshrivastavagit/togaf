# Phase D: Technology Architecture - Deployment Topology

This document details the physical deployment topology, AWS VPC subnetting layout, networking, security boundary definition, and hybrid-cloud integration links to the sponsor bank's Core Banking System (CBS).

---

## 1. Network Subnet Layout

To isolate workloads according to security tiers, the infrastructure is deployed inside an AWS VPC across three Availability Zones (ap-south-1a, ap-south-1b, ap-south-1c).

```
+----------------------------------------------------------------------------------+
|                                AWS VPC (10.100.0.0/16)                           |
|                                                                                  |
|  +----------------------------------------------------------------------------+  |
|  | Public Subnets (DMZ) - 10.100.1.0/24, 10.100.2.0/24, 10.100.3.0/24        |  |
|  |  [Route53] -> [WAF v2] -> [Application Load Balancer (ALB)] -> [NAT GWs]   |  |
|  +-------------------------------------+--------------------------------------+  |
|                                        |                                         |
|                                        v (Inbound Route)                         |
|  +----------------------------------------------------------------------------+  |
|  | Private App Subnets - 10.100.10.0/20, 10.100.32.0/20, 10.100.48.0/20       |  |
|  |  [AWS EKS Cluster]                                                         |  |
|  |    - Go Onboarding, Node Consent, FastAPI Underwriting, Spring Ledger, etc. |  |
|  +-------------------------------------+--------------------------------------+  |
|                                        |                                         |
|                                        v (DB Connections Only)                   |
|  +----------------------------------------------------------------------------+  |
|  | Private DB Subnets - 10.100.80.0/24, 10.100.81.0/24, 10.100.82.0/24        |  |
|  |  [RDS Aurora Postgres]  [DocumentDB Cluster]  [ElastiCache Redis]          |  |
|  +----------------------------------------------------------------------------+  |
|                                                                                  |
+----------------------------------------------------------------------------------+
                                         |
                        (Transit Gateway / Direct Connect)
                                         v
                         +-------------------------------+
                         |  Sponsor Bank Core Banking    |
                         |  System (CBS) Network         |
                         +-------------------------------+
```

### Subnet Allocation Table
| Subnet Tier | CIDR Range | Placement | NAT Gateway / Internet Gateway Routing |
| :--- | :--- | :--- | :--- |
| **Public DMZ (AZ1)** | `10.100.1.0/24` | ap-south-1a | Internet Gateway (IGW) route active. Host ALBs, Nat Gateways. |
| **Public DMZ (AZ2)** | `10.100.2.0/24` | ap-south-1b | Internet Gateway (IGW) route active. Host ALBs, Nat Gateways. |
| **Public DMZ (AZ3)** | `10.100.3.0/24` | ap-south-1c | Internet Gateway (IGW) route active. Host ALBs, Nat Gateways. |
| **Private App (AZ1)** | `10.100.10.0/20` | ap-south-1a | Routes outgoing traffic to NAT Gateway in Public AZ1. EKS Node Group. |
| **Private App (AZ2)** | `10.100.32.0/20` | ap-south-1b | Routes outgoing traffic to NAT Gateway in Public AZ2. EKS Node Group. |
| **Private App (AZ3)** | `10.100.48.0/20` | ap-south-1c | Routes outgoing traffic to NAT Gateway in Public AZ3. EKS Node Group. |
| **Private DB (AZ1)** | `10.100.80.0/24` | ap-south-1a | No Internet access. Host RDS databases and Redis instances. |
| **Private DB (AZ2)** | `10.100.81.0/24` | ap-south-1b | No Internet access. Host RDS databases and Redis instances. |
| **Private DB (AZ3)** | `10.100.82.0/24` | ap-south-1c | No Internet access. Host RDS databases and Redis instances. |

---

## 2. Ingress & Edge Protection Specs

1. **Route53 DNS:** Resolves external domains (e.g. `api.lender.com`) and routes to the ALB via Geo-Proximity records to minimize latency.
2. **AWS WAF v2:** Attached directly to the Application Load Balancer. Rules applied include:
   * SQL Injection Prevention.
   * Cross-Site Scripting (XSS) Mitigation.
   * Geo-blocking (blocking all traffic originating outside India, except certified corporate VPN IP ranges).
   * Rate-limiting: Max 120 requests per minute per IP address.
3. **Application Load Balancer (ALB):** Terminates SSL using a certificate managed by AWS Certificate Manager (ACM). ALB is configured to forward requests to the **Kong API Gateway** running inside the EKS cluster Private App subnet.

---

## 3. EKS Cluster Architecture

* **Type:** Managed EKS (Kubernetes 1.28)
* **Worker Nodes Node-Groups:**
  * **System Node Group:** `m5.large` instances (running CoreDNS, Metrics Server, Kong, Istio Ingress).
  * **Application Node Group:** `c5.xlarge` compute-optimized instances (scaled via Cluster Autoscaler).
  * **Database/Cache Support:** Managed databases used instead of running databases inside K8s, ensuring physical disk state isolation.

---

## 4. Sponsor Bank Hybrid-Cloud Connectivity (CBS Link)

Ledger reconciliation and disbursements require a low-latency, secure physical link to the Sponsor Bank's host system (CBS).

```
   [AWS VPC Private App Subnet] 
                │
         [Transit Gateway]
                │
       [AWS Direct Connect] ◄─── (Primary Link: 1Gbps Dedicated Fiber)
                │
   [Virtual Private Gateway] ◄─── (Backup: IPSec VPN tunnel over internet)
                │
        [Sponsor Bank CBS]
```

### Connectivity Protocol & Specs
* **Primary Connection:** AWS Direct Connect (DX) link at 1 Gbps with physical diversity across two DX locations.
* **Redundancy Fallback:** Site-to-Site IPSec VPN tunnel terminating at AWS Virtual Private Gateway (VGW) over standard ISP lines using BGP dynamic routing.
* **Transit Gateway (TGW):** Routes traffic from multiple AWS accounts (Staging, Production, Management) to the Direct Connect gateway connection.
* **Encapsulation & Port Access:** Data is encrypted inside the DX tunnel using IPsec (MACsec standard at Layer 2), and only specific port allocations (e.g., port `15002` for bank's direct gRPC ledger interface) are allowed through the bank router ACLs.
