## Hi there 👋

I'm a software engineer building **production-oriented Java/Spring Boot services**, with depth in
**transactional correctness, distributed systems, cloud-native delivery, and AI-native engineering** —
on top of a long background in large-scale telecom service delivery (incident/problem management, SLAs).

My work spans REST API design, relational and document persistence, event-driven integration,
containerized delivery, and infrastructure-as-code, brought together across a set of related portfolio
repositories — each built to make **real engineering decisions with explicit trade-offs**, not just to demo a framework.

---

## Core Stack

- **Languages:** Java 17 / 21
- **Framework:** Spring Boot 3.x (Web, Data JPA, Data MongoDB, Security/OAuth2, Actuator, AOP, Cache, OpenAPI)
- **Databases:** PostgreSQL, MongoDB
- **Messaging:** Apache Kafka
- **Resilience:** Resilience4j (circuit breakers, fallbacks)
- **Testing:** JUnit 5, Testcontainers, Mockito, JaCoCo
- **Frontend:** React 19, Vite, TypeScript, Tailwind CSS
- **Ops / Delivery:** Docker, Docker Compose, Kubernetes, Helm, Terraform, Jenkins, GitHub Actions
- **Cloud:** AWS (EC2, S3, RDS, ECS/EKS, IAM, CloudWatch)
- **Observability:** Prometheus, Grafana, Spring Boot Actuator

---

## Selected Engineering Decisions

A few real decisions from the repositories below — each stated with its trade-off (happy to go deeper):

- **Concurrency & correctness** — optimistic locking (JPA `@Version`) for inventory reservation, *proven
  with a Testcontainers concurrency test against real Postgres*: parallel orders can't oversell, the loser
  retries instead of blocking. Invariants enforced in both the domain layer and a DB `CHECK` constraint.
- **Caching** — in-process Caffeine with per-cache TTLs and evict-on-write, chosen for zero-infra
  simplicity; designed to move to a shared cache (Redis) once the service scales horizontally.
- **Resilience** — synchronous inter-service calls wrapped in Resilience4j circuit breakers with
  fallbacks; event publishing kept *best-effort async* so a broker outage degrades to "no event" rather
  than a failed request (transactional outbox as the next step).
- **Security** — stateless OAuth2 resource server validating JWTs locally against cached JWKS (no
  per-request IdP call); sensitive media served through auth-gated endpoints with EXIF/GPS stripping.
- **Contracts & schema** — contract-first OpenAPI generating server interfaces; Flyway-managed, auditable
  schema evolution.
- **Cloud & CI/CD** — Helm-packaged services with Actuator readiness/liveness probes; Terraform
  (VPC / EKS / RDS in private subnets); an in-cluster, daemonless Jenkins pipeline (Kaniko).

---

## AI-Native Engineering

- **Building *with* AI** — governance for coding agents: permission boundaries, human-approval gates and
  spec-driven supervision, documented as reusable patterns →
  **[ai-native-delivery-patterns](https://github.com/ferrelm/ai-native-delivery-patterns)**.
- **Building AI features** — LLM (OpenAI) integration in a recommendations service: candidate retrieval,
  prompt construction, and response shaping behind a clean service boundary.
- **Writing about it** — *[The Great Inversion: How AI Broke the Software Development Model We Spent 50 Years Building](https://ferrelm.github.io/the-great-inversion/)*,
  an essay on how AI is reshaping software engineering.

---

## Portfolio Repositories

> Some repositories below are private while I scrub them for public release — they'll be linked as they go public.

### Backend Fundamentals — transactional correctness & concurrency
🟢 Public **[order-inventory-api](https://github.com/ferrelm/order-inventory-api)**
Spring Boot + PostgreSQL + JPA + Flyway. Stock reservation under concurrency via optimistic locking
(`@Version`), with a latch-synchronized Testcontainers test proving only one of two parallel orders wins.
Defense-in-depth invariants (domain + DB `CHECK`), Bean Validation, contract-first API.

### Microservice Integration — events & resilience
🟢 Public **[shopping-cart-service](https://github.com/ferrelm/shopping-cart-service)**
Spring Boot + MongoDB microservice: best-effort async Kafka event publishing, synchronous pricing via
OpenFeign wrapped in a Resilience4j circuit breaker with fallback, AOP-based cross-cutting logging,
OpenAPI, Helm/Kubernetes manifests, and Testcontainers + Postman/Newman testing.

### Security-Aware Service Delivery
🟢 Public **[book-orders-service](https://github.com/ferrelm/book-orders-service)**
Stateless OAuth2 resource server (JWT validated against cached JWKS), contract-first OpenAPI, Checkstyle +
JaCoCo quality gates, Helm + Terraform, and a Jenkins CI/CD pipeline with a manual promotion gate.

### Multi-Service Platform Design
🔒 Private **discover-portugal**
A multi-service platform (catalog, booking, payments, notifications, AI) demonstrating **domain
decomposition**, **hybrid persistence** (PostgreSQL for the structured core, MongoDB for flexible detail
documents), **Kafka event choreography** (a slow mailer never blocks a booking), Feign + circuit breakers
for read-time calls, and an **OpenAI-backed recommendations service**.

### Full-Stack Product Delivery
🔒 Private **club-analytics**
Full-stack analytics around Strava data. Java 21 + Spring Boot backend with 50+ Flyway migrations, JWT
auth, contract-first OpenAPI, **proactive OAuth token refresh with incremental sync**, Caffeine caching,
and private object storage (S3-compatible) with EXIF/GPS stripping. React 19 + Recharts frontend;
Testcontainers + Vitest; Makefile workflows and rich CI.

### Cloud & Platform Engineering
🔒 Private **cloud-backend-learning**
A progression from Spring Boot basics through AWS deployment, Kubernetes/Helm, an in-cluster Kaniko
Jenkins pipeline, Terraform (VPC/EKS/RDS), and observability (Prometheus/Grafana).

---

## What I'm Working On

- Deepening cloud-native and platform engineering (AWS, Kubernetes, Terraform, observability)
- Building production-realistic full-stack demos end-to-end
- Improving deployment and release discipline across the portfolio

---

## Contact

Feel free to explore the repos or reach out via GitHub.
