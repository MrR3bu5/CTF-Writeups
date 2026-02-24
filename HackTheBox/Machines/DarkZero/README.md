# Hack The Box - DarkZero

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Windows
- Status: Active
- Date: 2025-10-04

## What I learned
- AD targets reward discipline. Time sync, signing requirements, and protocol choices can block common tooling fast.
- SMB read access to domain shares is not harmless. It is an early foothold for policy and configuration discovery.
- SQL Server in a domain environment can act like a bridge to execution when it is misconfigured or overly trusted.

## Non spoiler observations
- The exposed services strongly suggested a domain controller style attack surface with Kerberos, LDAP, and SMB.
- SMB signing was enforced, which narrowed down relay style options and pushed me toward authenticated paths.
- LDAP signing requirements affected how enumeration tools behaved, which forced me to adapt transport and approach.
- A SQL Server service was reachable and became the most direct pivot to code execution style outcomes.

## Skills practiced
- AD service triage and planning, choosing what to enumerate first and what to ignore.
- SMB share review for policy and deployment signals without assuming writable access.
- Handling common AD friction points like clock skew and directory signing requirements.
- SQL Server assessment mindset in domain contexts, focusing on boundaries and trust, not only version checks.
- Post access privilege boundary mapping on Windows Server targets.

## Defensive takeaways
- Fix: lock down SQL Server features that enable OS level command execution, and restrict who can use them.
- Fix: enforce least privilege for service accounts, and review delegation and rights assignments routinely.
- Fix: limit data exposure in domain shares, and monitor access to SYSVOL and NETLOGON for unusual clients.
- Detect: alert on abnormal authentication patterns across Kerberos, LDAP, and SMB, especially off hours and from new source IPs.
- Detect: monitor SQL Server for suspicious procedure usage and lateral movement indicators.

## What I would do next time
- Validate time sync early on AD targets.
- Confirm signing settings and pick tools and transports that match.
- Inventory reachable management planes, then focus on the highest trust boundary first.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
