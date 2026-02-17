# How I Use Codex in My Home Lab (Sanitized)

Last updated: February 17, 2026

## Role of Codex in My Workflow
I use Codex as an operations co-pilot for structured, low-risk infrastructure work:
- run repeatable validation checks across hosts/services
- make controlled config/documentation updates
- enforce public-repo sanitization and security standards
- maintain timestamped operational logs and state snapshots

## Typical Task Types
- Cross-host health validation (`systemd`, service reachability, monitor summaries)
- Monitoring expansion (new device/service checks in Uptime Kuma)
- DNS/proxy consistency checks and remediation
- Repository hardening (private IP redaction, security policy files, CI guardrails)
- Portfolio documentation updates for interview-readiness

## Safety Guardrails Used
- No destructive commands without explicit intent
- Backup before high-impact config changes
- Validate after every change
- Keep public outputs sanitized (no private IPs, no secrets, no credentials)
- Record each operation run with timestamp + outcome + pending items

## Examples of Codex-Assisted Outcomes
- Standardized `.lan` service routing and HTTPS validation
- Expanded LAN monitoring coverage and dashboard links
- Added security scan workflows to lab repositories
- Applied branch protection rules on active public repos
- Updated interview documentation to reflect current environment and repos

## Why This Matters for IT Operations
Using Codex this way improves consistency and speed while preserving change control:
- faster triage and repeatable validation
- stronger documentation discipline
- better security hygiene for public technical portfolios
