# Remote Administration From Linux

## Scope
- Source theme: administering Windows systems from a Linux workstation over the local network
- Purpose: document the public-safe pattern for mixed-platform remote administration.

## Design Goal
- Use a Linux workstation as a credible daily administration point for mixed Windows and Linux lab environments.
- Access Windows systems through RDP without exposing them externally.

## Pattern
- Enable remote desktop on the Windows target.
- Verify the correct user account and password requirements.
- Confirm the LAN-facing Windows network profile supports the connection.
- Use a Linux RDP client for day-to-day access.

## Security Model
- Limit remote desktop use to the trusted local network or a future VPN path.
- Do not expose RDP directly to the public internet.
- Keep firewall rules aligned with private or trusted network scope only.

## Operational Value
- This supports a practical mixed-platform workflow:
  - Linux workstation for SSH, docs, Git, and scripting
  - Windows hosts for Windows-native admin tasks and labs
- It also reinforces network-profile awareness and Windows firewall validation.

## Public-Safe Notes
- Remove real hostnames, usernames, and LAN IPs from any screenshots or command examples.
