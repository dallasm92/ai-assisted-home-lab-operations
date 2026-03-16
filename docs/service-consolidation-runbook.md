# Service Consolidation Runbook

## Scope
- Source theme: moving self-hosted services from a smaller utility host onto a primary application server while leaving DNS filtering in place
- Purpose: capture the public-safe runbook for service consolidation.

## Goal State
- Keep the DNS filtering role on the lightweight utility host.
- Move application and dashboard containers to the primary always-on server.
- Preserve familiar service URLs and operational behavior where practical.

## Migration Strategy
1. Inventory what is actually running on the source host.
2. Identify the persistent data path for each service.
3. Copy configuration and data before any cutover.
4. Recreate each service with compose-based definitions on the destination host.
5. Validate the destination instance before stopping the source instance.
6. Cut over one service at a time.

## Discovery Pattern
- Enumerate running containers.
- Find compose definitions or equivalent startup definitions.
- Capture:
  - image name
  - published ports
  - bind mounts or named volumes
  - environment variables
- Treat data path discovery as the critical step.

## Destination Pattern
- Use per-service directories on the destination host.
- Prefer compose-managed services with persistent bind mounts.
- Standardize restart behavior and basic logging checks.

## Cutover Discipline
- Never migrate all services at once.
- For each service:
  - start on destination
  - validate
  - stop old instance
  - validate again through the client path
- Keep DNS filtering out of the batch if it is your primary local resolver.

## Networking Pattern
- Either adopt new server-hosted URLs or preserve old friendly names through local DNS updates.
- Reverse proxying can be layered on later if you want cleaner internal URLs.

## Public-Safe Notes
- Do not publish:
  - real source and destination IPs
  - real account names
  - exact private data paths unless already intentionally public
