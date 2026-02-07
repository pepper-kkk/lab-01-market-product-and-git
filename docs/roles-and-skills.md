## Components and roles

- Mobile/Web Client
  - Mobile engineer (iOS/Android) / Front-end engineer (Web)
  - UI/UX designer
  - QA engineer
  - Product manager
- MTProto Gateway (connection layer / edge)
  - Back-end engineer
  - DevOps / SRE
  - Security engineer
  - QA engineer
- Auth Service
  - Back-end engineer
  - Security engineer
  - QA engineer
  - DevOps / SRE
- Message Service (core messaging)
  - Back-end engineer
  - QA engineer
  - DevOps / SRE
  - Data engineer (optional: analytics/streaming)
- Media Service (uploads/downloads, metadata)
  - Back-end engineer
  - DevOps / SRE
  - QA engineer
  - Security engineer (optional)
- Push Service (notifications)
  - Back-end engineer
  - DevOps / SRE
  - QA engineer
- Kafka Event Bus / event streaming
  - Back-end engineer
  - DevOps / SRE
  - Data engineer
- Data layer (State Cache, Sharded DB, Distributed DFS)
  - Database engineer / Back-end engineer
  - DevOps / SRE
  - Security engineer
  - QA engineer

## Roles and responsibilities

1. **Back-end engineer**
   - Designs and implements server-side services and APIs.
   - Works with databases, caching, message queues, and performance optimization.
   - Adds observability (logs/metrics/traces) and handles production issues with the team.

2. **Mobile engineer (iOS/Android)**
   - Builds and maintains mobile client features (UI, offline behavior, media handling).
   - Integrates with backend APIs/protocols, handles authentication and session state.
   - Optimizes performance (battery, network, memory) and ensures stability across devices.

3. **DevOps / SRE**
   - Maintains infrastructure and deployments (CI/CD, environments, configs, secrets).
   - Ensures reliability: monitoring/alerting, incident response, capacity planning, scaling.
   - Improves operational practices (automation, IaC, disaster recovery, backups).

4. **QA engineer**
   - Creates test plans and test cases, validates features end-to-end.
   - Automates tests where possible (API/UI), manages regressions and quality gates.
   - Reports bugs with clear steps, verifies fixes, helps improve release confidence.

5. **Security engineer**
   - Reviews architecture for threats (auth/session security, abuse prevention, data access).
   - Helps with secure coding practices, vulnerability management, and security testing.
   - Supports incident handling related to security and improves controls over time.

## Common skills across roles

- Git basics (branches, PRs, code review)
- Understanding of client–server architecture and APIs (REST-like patterns, protocols, payloads)
- Debugging and troubleshooting (logs, reproducing issues, root-cause analysis)
- Testing mindset (unit/integration/e2e concepts, regression awareness)
- CI/CD basics (pipelines, environments, releases)
- Observability basics (metrics, logs, tracing; monitoring and alerting)
- Security hygiene (auth/session basics, secrets, least privilege, common web/app risks)
- Clear communication and collaboration (tickets/issues, code review comments, documenting decisions)
