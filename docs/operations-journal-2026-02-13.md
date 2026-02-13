# Operations Journal - February 13, 2026

## Change Goal
Create secure AI-assisted operations for a three-node home lab with automation, validation, and documentation.

## Timeline (Condensed)

### Access and Trust
- Verified host inventory and SSH target definitions.
- Confirmed key-based authentication paths and host alias usage.
- Normalized remote execution workflow for repeatability.

### Update and Maintenance Reliability
- Implemented multi-host package maintenance flow.
- Fixed script behavior for Linux Mint scripting compatibility (`apt-get` vs wrapper behavior).
- Added clearer step-by-step pass/fail output and final error summary.

### Security and Hardening
- Applied UFW LAN-only inbound policy on server hosts.
- Confirmed Pi-hole DNS service continuity after firewall updates.
- Performed post-hardening connectivity checks for required service ports.

### CasaOS Operations
- Audited CasaOS core services and container stack health.
- Ran controlled image refresh + stack restart sequence.
- Verified container health after settle period.
- Added weekly automated CasaOS maintenance timer.

### Alerting
- Added failure-alert handlers for automated update/maintenance jobs.
- Corrected unit configuration placement (`OnFailure` in `[Unit]`).
- Validated alert trigger path and log output.

### Service Access and DNS
- Installed and configured additional support services (Duplicati, NPM).
- Resolved startup/path issues by correcting app data mount locations.
- Aligned proxy hostnames with Pi-hole local domain behavior.
- Added minimal Docker-bridge firewall exceptions required for proxy upstream traffic.

### Backup Automation
- Added encrypted nightly Duplicati backup workflow.
- Resolved first-run passphrase target mismatch by isolating backup target path.
- Verified successful seed backup completion and timer schedule.

## Post-Change State
- Automated maintenance and backup schedules active.
- Alerting active for failure conditions.
- Core services healthy and reachable via standardized local DNS/proxy paths.
- Documentation completed for repeatability and portfolio evidence.

## Lessons Learned
- Always account for distro-specific package manager wrappers in automation.
- Containerized reverse proxies may require explicit firewall allowances from bridge CIDRs.
- Local DNS behavior should match chosen internal domain strategy from day one.
- First backup seed runs need longer windows and explicit verification.
