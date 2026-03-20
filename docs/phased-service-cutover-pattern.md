# Phased Service Cutover Pattern

## Scope
- Source theme: moving a small set of active containerized services from a utility node to a primary server without disturbing the DNS role
- Purpose: capture the public-safe execution pattern for a cautious, service-by-service cutover when the source host is small, the destination host is stronger, and the front-door proxy path matters

## Situation This Fits
- A lightweight node is still carrying dashboard or app containers that would be better hosted on the main server.
- The environment already has one service that must stay in place, such as DNS filtering.
- The migration has to preserve operator access and avoid breaking the front-door reverse-proxy path.

## Target Shape
- Keep core DNS or resolver duties on the utility node.
- Move secondary application and dashboard containers to the primary server.
- Preserve familiar URLs or route names where practical after validation.

## Why This Pattern Is Different From A Generic Lift-And-Shift
- The source host may not have clean Compose-based definitions for every service.
- Container state discovery matters as much as the eventual destination config.
- One migrated service may be the ingress layer for the others, so it must move last.

## Discovery First
- Before any move, capture:
  - running container names
  - image names
  - published ports
  - persistent bind mounts or named volumes
  - startup method or compose-file location
- Treat “where the real data lives” as the highest-risk unknown.

## Safe Migration Order
1. Migrate non-front-door application services first.
2. Migrate dashboards or operator-facing apps next.
3. Migrate the ingress or reverse-proxy layer last.

## Why This Order Works
- Early moves validate the destination Docker environment without risking the main entry point.
- Dashboard migration is lower risk than moving the component that owns ports 80 and 443.
- Keeping the ingress service for last limits the blast radius of a bad cutover.

## Cutover Discipline
- Recreate each service on the destination with explicit persistent storage.
- Validate the new instance before stopping the old one.
- Stop and remove the old container only after destination checks pass.
- Re-check through the client path after each cutover, not just at the container level.

## Recovery Rule
- If the destination instance fails validation, keep the source service running and do not proceed to the next service.
- The migration should always allow a one-service rollback instead of forcing a full-environment rollback.

## Destination Standardization
- Use compose-managed service definitions on the primary host.
- Prefer one directory per migrated service.
- Normalize restart behavior and logging expectations while rebuilding the stack.

## Networking And URL Handling
- Plan whether services will:
  - keep the same friendly names through DNS or proxy updates
  - or temporarily move to server-specific URLs during validation
- Avoid changing multiple naming layers at the same moment as the container cutover unless the migration is very small and well understood.

## Public-Safe Notes
- Do not publish:
  - real host IPs
  - private bind-mount paths
  - live proxy targets
  - copied environment files with secrets or tokens
