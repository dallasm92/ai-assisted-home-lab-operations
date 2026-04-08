# Container Host Reboot Recovery Pattern

## Scope
- Source theme: post-maintenance reboot recovery on a Linux container host
- Purpose: capture a public-safe recovery pattern for verifying that a container host is truly healthy after a reboot instead of stopping at basic network reachability.

## Operating Problem
- A host can finish rebooting and respond to ping or SSH while the application stack is still partially unavailable.
- Reverse-proxied services may briefly return:
  - connection failures
  - connection resets
  - `502` responses
- Container health checks can lag behind basic host recovery by several minutes.

## Recovery Sequence
1. Confirm the host is reachable on the network.
2. Confirm SSH login succeeds and the reboot-required flag is cleared.
3. Check for failed systemd units before assuming the issue is only in Docker.
4. Verify the container engine is fully active.
5. Check container status and health, not just whether the containers exist.
6. Test local application ports on the host before testing the reverse-proxy path.
7. Test the external service hostnames only after the local app ports respond.

## Why This Matters Operationally
- A restart after patching is one of the easiest moments to create a false green state.
- Basic host recovery can hide:
  - Docker not fully initialized yet
  - reverse proxy startup lag
  - unhealthy application containers
  - backend dependencies such as database or cache services still warming up
- If the operator stops at "SSH works again," the next signal often comes from users or uptime alerts instead of from the recovery workflow itself.

## Practical Validation Pattern
- Host-level checks:
  - ping
  - SSH login
  - uptime
  - `systemctl --failed`
  - reboot-required file state
- Container-host checks:
  - container runtime active
  - per-container status
  - per-container health state
  - startup logs for reverse proxy and key apps
- Service-path checks:
  - local loopback or host-port requests
  - reverse-proxy ports
  - final hostname-based HTTPS validation

## Recovery Tiers

### Tier 1: Host Recovery
- Confirm the host has finished booting cleanly.
- Check:
  - uptime
  - `systemctl --failed`
  - disk space and memory pressure
  - whether the host still thinks a reboot is pending

### Tier 2: Runtime Recovery
- Confirm the container runtime and the supervisor layer are stable.
- Check:
  - Docker or container-engine service state
  - container restart counts
  - health status for key containers
  - recent logs for reverse proxy, database, and application services

### Tier 3: Service Recovery
- Confirm the application path is working end to end.
- Check:
  - local app ports on the host
  - proxy listener state
  - final HTTPS responses on the public-safe service hostnames
  - monitoring system view after services are back

## Decision Points
- If SSH is available but Docker is not yet healthy:
  - wait for the runtime to stabilize before escalating
- If Docker is healthy but reverse-proxied services are failing:
  - inspect proxy logs and backend container health before rebooting again
- If local app ports work but hostname-based checks fail:
  - focus on the reverse-proxy layer or DNS path rather than the app container itself
- If one container stays unhealthy while the rest recover:
  - troubleshoot that service directly instead of treating the whole host as failed

## Key Lesson
- "Host is back" is not the same as "services are back."
- A clean reboot can still produce a short incident window where:
  - the reverse proxy is starting
  - application containers are still warming up
  - health checks temporarily mark services as unhealthy
- The correct operator response is staged validation rather than repeated full-host reboots.

## Decision Rule
- If the host is reachable, systemd is clean, and containers are progressing toward healthy states, prefer targeted service validation and selective container troubleshooting over another immediate reboot.

## Reusable Operator Pattern
- Treat reboot recovery as a short runbook, not as a single ping test.
- Capture the validation order in automation where possible so the same sequence is used every time:
  - reachability
  - host health
  - container runtime health
  - application-path validation
- That pattern creates better evidence for:
  - post-maintenance verification
  - incident review
  - portfolio documentation of operational discipline

## Public-Safe Notes
- Keep exact internal hostnames, IPs, and service mappings sanitized when publishing.
- Focus the writeup on recovery method and validation order rather than the private environment layout.
