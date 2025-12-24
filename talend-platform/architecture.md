# Talend Architecture – High Level

Talend environments are typically composed of the following components:

- Talend Studio – development environment
- Git Repository – source code management
- Nexus – artifact repository
- Talend Administration Center (TAC) – orchestration and monitoring
- Execution Servers (Job Servers) – runtime execution
- Database – metadata, scheduling, logs

---

## High-Level Flow
1. Developers build Jobs in Talend Studio
2. Code is versioned and managed in Git
3. Jobs are built into artifacts (JARs)
4. Artifacts are stored in Nexus
5. TAC schedules and triggers executions
6. Job Servers execute processes and report status back to TAC

