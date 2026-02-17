# Monitoring Evidence (Sanitized)

## Coverage
- Core services monitored via HTTP checks
- Infrastructure endpoints monitored via ping checks
- Device-level visibility for active LAN clients

## Typical Validation Outputs
- Endpoint reachability checks return expected HTTP status classes
- Scheduled backup jobs report successful completion state
- Monitoring system reports active monitor totals and current up/down distribution

## Notes
- Consumer endpoints may transition to down state when idle/sleeping.
- Critical infra checks are separated from consumer endpoints to reduce alert fatigue.
