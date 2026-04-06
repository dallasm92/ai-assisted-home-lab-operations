# AI-Assisted Home Lab Operations

Practical implementation of secure AI-assisted infrastructure operations across a multi-host home lab.

Last reviewed: April 6, 2026

## Objective
Demonstrate production-style operational discipline with AI assistance while maintaining strict security boundaries.

## What This Repo Best Demonstrates
- repeatable validation before and after changes
- monitoring, backup, and alert workflow design
- secure AI-assisted operations with explicit guardrails

If a reviewer wants broader architecture context first:
- see `home-lab-overview`

If a reviewer wants more traditional support troubleshooting first:
- see `it-support-labs`
- see `ad-lab-windows-server-2022`

## Lab Scope (Sanitized)
- `macmint`: workstation
- `asus-server`: server + container host
- `pi-core`: DNS and utility node

## Implemented Capabilities
- SSH-based cross-host operations with hardened defaults
- Automated maintenance and health checks
- Backup + off-host sync + health monitoring workflow
- Service monitoring and endpoint validation workflow
- Standardized failure alerting for critical automation units

## What Hiring Managers Can Review
- `docs/implementation-summary.md`
- `docs/operations-journal-2026-02-13.md`
- `docs/security-notes.md`
- `docs/current-operations-snapshot.md`
- `docs/monitoring-evidence-sanitized.md`
- `docs/codex-in-homelab.md`
- `docs/service-consolidation-runbook.md`
- `docs/remote-admin-from-linux.md`
- `docs/windows-ad-lab-pattern.md`
- `docs/dashboard-and-host-observability-pattern.md`
- `docs/backup-restore-and-resilience-pattern.md`
- `docs/immutable-ops-and-incident-automation.md`
- `docs/phased-service-cutover-pattern.md`
- `docs/conditional-workstation-node-pattern.md`
- `docs/container-host-reboot-recovery-pattern.md`

## Security Boundaries
- Public docs omit real internal addressing and credentials
- No private keys, tokens, or secrets are committed
- Operational examples use sanitized identifiers only

See `SECURITY.md` for repository-level policy.
