# Security Notes

## Core Principles Applied
- Least privilege on network exposure (LAN-scoped rules by default)
- Key-based authentication over password-based remote execution where possible
- Explicit validation after each change
- No internet-exposed admin interfaces by default

## Controls Implemented
- UFW enabled on server nodes with explicit allowlists
- Sensitive automation paths moved to root-owned scripts where appropriate
- Failure-alerting attached to automated jobs (`systemd` OnFailure units)
- Service health and port checks after configuration changes

## Operational Boundaries
- Changes focused on low-risk and reversible operations during live setup
- Destructive actions avoided without explicit authorization
- Hostnames/IPs and sensitive details redacted in public-facing documentation

## Recommended Next Steps
- Add MFA and hardened auth on externally reachable platforms
- Add off-host backup target and periodic restore tests
- Add centralized alert destination (email/webhook/chat)
- Add monthly firewall and open-port review checklist
