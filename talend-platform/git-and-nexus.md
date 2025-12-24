# Git & Nexus Integration

## Git Repository
Git is used for:
- Source code versioning
- Branch management (DEV / PROD)
- Collaboration across teams
- Traceability and rollback

Key operations:
- Pull / Commit / Push
- Merge from dev to master
- Environment isolation via branches

## Nexus – Artifact Repository
Nexus stores build outputs (artifacts), not source code.

- Stores compiled Job packages (JARs, ZIPs)
- Manages artifact versions
- Enables promotion across environments
- Supplies artifacts to TAC and Job Servers

Git manages **code**.
Nexus manages **runtime artifacts**.
