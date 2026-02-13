# AI-Assisted Home Lab Operations

Practical documentation of how I securely configured AI-assisted operations across a multi-machine home lab and automated recurring maintenance tasks.

Date of implementation: February 13, 2026

## Objective
Build a secure, repeatable workflow where an AI coding agent can:
- access lab machines over SSH safely
- audit service health
- apply low-risk maintenance and updates
- automate recurring update/backup operations
- produce operational documentation suitable for IT portfolio review

## Lab Scope
- `macmint` (Linux Mint workstation)
- `asus-server` (Ubuntu Server + CasaOS + Docker services)
- `pi-core` (Raspberry Pi running Pi-hole)

Note: Sensitive details are intentionally redacted or generalized.

## What Was Implemented
- SSH key-based access across hosts with host aliases
- LAN-scoped firewall hardening (UFW) on server endpoints
- Daily/weekly maintenance automation with `systemd` timers
- Failure alerting hooks for automated jobs
- CasaOS service audit and controlled container refresh
- Proxy + DNS path standardization (`.lan`) for service access
- Encrypted nightly config backups (Duplicati)
- Morning/nightly health-summary workflow

## Outcomes
- Cross-host update workflow became one command + scheduled automation
- Core CasaOS services validated healthy post-maintenance
- Backup and alert paths tested successfully
- Service access simplified through stable internal hostnames

## Before/After Metrics (Interview-Friendly)

| Area | Before | After | Impact |
|---|---|---|---|
| Hosts maintained per cycle | 0 automated | 3 hosts managed in one workflow (`macmint`, `asus-server`, `pi-core`) | Multi-node maintenance became repeatable |
| Daily patching effort | Manual execution each day | Scheduled automation at 01:00 on always-on hosts + one manual run script for full lab | Reduced repetitive daily admin work |
| Automated maintenance timers | 0 | 4 active timers (`lab-auto-update`, `casaos-maintenance`, `duplicati-nightly-backup`, plus summary workflow usage) | Predictable maintenance windows |
| Failure visibility | Reactive/manual log checking | `OnFailure` alert handlers wired for update, CasaOS maintenance, and backup jobs | Faster detection of failed automation runs |
| Service access consistency | Mixed direct ports and ad-hoc paths | Standardized internal routing via NPM + Pi-hole local DNS names (`*.lan`) | Faster troubleshooting and easier daily operations |
| Backup posture | No validated automated config backup run | Encrypted nightly Duplicati backup with retention policy | Measurable recovery readiness |

### Measured Results from Initial Validation
- Duplicati seed backup completed successfully:
  - Duration: 5m39s
  - Data uploaded: ~672.56 MB
  - Remote files created: 29
- CasaOS application stack health validated after update cycle:
  - 8 containers running
  - No unhealthy containers reported at validation time
- Firewall posture tightened:
  - Removed unused inbound `80/tcp` LAN allow when not required, then re-opened deliberately for reverse proxy workflow

## Repository Contents
- `docs/implementation-summary.md` - architecture and implementation notes
- `docs/operations-journal-2026-02-13.md` - detailed timeline of actions and results
- `docs/security-notes.md` - hardening decisions and boundaries

## Skills Demonstrated
- Linux administration
- SSH and key-based authentication
- Firewall policy design (least privilege on LAN)
- Docker/CasaOS operations
- DNS and reverse-proxy troubleshooting
- `systemd` service/timer automation
- Incident-style documentation and validation

## Next Improvements
- Add centralized notification channel (email/Discord/webhook)
- Add service-level backup verification/restore drills
- Add trend dashboard for resource usage over time
