# Reference Library: Design Patterns

This directory contains reusable microservices and integration design patterns tailored for high-volume, low-latency, and compliance-driven lending platforms.

---

## 🎨 Documented Design Patterns

1.  **[Transactional Outbox Pattern](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/patterns/outbox_pattern.md)**: Resolves dual-write problems between microservices databases and Kafka event streams.
2.  **[Saga Orchestration Pattern](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/patterns/saga_pattern.md)**: Manages distributed transactions and rollbacks (compensating actions) across multiple services.
3.  **[Resilience Circuit Breaker Pattern](file:///Users/manavshrivastava/Documents/github/untitled%20folder/togaf/architecture_repository/5_reference_library/patterns/circuit_breaker_pattern.md)**: Implements fault isolation to prevent partner API outages from bringing down core lending systems.

---

## 🛠️ Usage Guidelines
All developers and architects must leverage these patterns when implementing asynchronous messaging, multi-service workflows, or third-party API integrations. Conformance to these patterns is validated during Stage-Gate 2 (Pre-Deployment Audit) reviews.
