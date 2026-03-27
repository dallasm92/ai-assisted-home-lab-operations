# Conditional Workstation Node Pattern

## Scope
- Source theme: integrating a Windows workstation into a mixed-platform lab without making it an infrastructure dependency
- Purpose: document a public-safe pattern for using a primary workstation as an operator endpoint while keeping core services independent of that workstation’s uptime.

## Design Goal
- Keep a primary Windows workstation available for:
  - browser-based admin access
  - file movement
  - ad hoc validation
  - occasional remote administration
- Avoid making the workstation a hard dependency for normal server-side operations.

## Operating Model
- Treat the workstation as a conditional node:
  - available when intentionally in use
  - optional when offline
- Use it as an operator endpoint, not as the system that other core services depend on.

## Common Failure Pattern
- The workstation can still reach internal services by IP.
- Internal hostnames stop resolving.
- The lab servers are healthy, but the workstation appears “cut off” from the environment.

## Troubleshooting Pattern
- Confirm raw IP reachability first.
- Test service ports directly before assuming a server outage.
- Check which Windows adapter is actually carrying live traffic.
- If Hyper-V external switching is in use, verify DNS on the active `vEthernet` path rather than assuming the physical NIC settings are authoritative.
- Only after adapter and DNS checks should browser-specific behavior be investigated.

## Hyper-V Networking Lesson
- Host networking can shift behind a virtual switch abstraction.
- That means:
  - the visible physical adapter may not be the interface that matters for DNS
  - resolver settings must be verified on the effective host path
  - mixed Windows and virtualization features can create confusing but explainable name-resolution failures

## Why This Pattern Matters
- It separates:
  - server availability problems
  - workstation resolver problems
  - browser-level issues
- This prevents optional client nodes from being misread as infrastructure failures.

## Public-Safe Notes
- Replace private hostnames, interface names, and internal DNS records with generic examples.
- Keep the note centered on method and design choice rather than the exact live topology.
