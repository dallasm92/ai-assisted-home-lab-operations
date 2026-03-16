# Windows AD Lab Pattern

## Scope
- Source themes:
  - Windows Server build for lab use
  - Active Directory workflow and documentation structure
- Purpose: capture a public-safe pattern for a Windows Server and Active Directory learning lab tied to entry-level IT operations.

## Design Goal
- Build a small domain environment that supports:
  - identity basics
  - DNS understanding
  - user and group administration
  - password resets and account unlocks
  - basic permissions and policy concepts

## Build Pattern
- Create a Windows Server VM or dedicated lab server.
- Promote it to a domain controller for a non-production lab domain.
- Use the lab for:
  - users and groups
  - organizational units
  - workstation joins
  - basic group policy
- Optionally integrate a Linux host with the domain for cross-platform identity practice.

## Core Help Desk Tasks Modeled
- Create users
- reset passwords
- unlock accounts
- manage group membership
- organize users and computers into OUs
- validate name resolution and domain joins

## Documentation Pattern
- Keep the writeup structured as:
  - build steps
  - screenshots or evidence
  - validation checks
  - troubleshooting notes
- Separate repeatable lab steps from environment-specific values.

## Public-Safe Notes
- Use generic domain examples.
- Avoid real usernames, emails, and exact VM internals in public screenshots.
- Treat account lists and group membership screenshots as review-required before publishing.
