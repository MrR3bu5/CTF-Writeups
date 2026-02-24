# Hack The Box - Cobblestone

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-11

## What I learned
- Host discovery is only step one. Virtual hosts and subdomains can change the entire attack surface. 
- Client facing apps often expose multiple trust boundaries. The gap between public pages and internal services is where risk shows up. 
- A clean chain usually mixes small issues. Discovery plus input handling plus weak secret handling is enough. 

## Non spoiler observations
- The target exposed SSH and an HTTP service that redirected to a hostname. 
- Subdomain and content discovery expanded the visible application footprint beyond the main site. 
- Web app behavior suggested multiple user driven features that deserved input validation testing. 
- I found indicators of missing defensive controls like CSRF protection and overly permissive app behavior. 

## Skills practiced
- Service triage and recon planning.
- Virtual host and subdomain enumeration.
- Web application testing workflow, focusing on input handling and session boundaries.
- Source awareness, mapping observed app behavior to likely components and risks.
- Local enumeration mindset after foothold, focusing on secrets and internal only services. 

## Defensive takeaways
- Fix: enforce server side input validation and output encoding across all user controlled fields. 
- Fix: remove hardcoded secrets from web accessible paths, rotate credentials, and scope DB accounts to least privilege. 
- Fix: lock down internal services so they do not become reachable through lateral access or accidental exposure. 
- Detect: alert on suspicious request patterns to dynamic pages that accept user input, and on unexpected file creation or web root writes. 
- Detect: monitor for anomalous database access from the web tier, including unusual queries and filesystem write behavior. 

## What I would do next time
- Confirm every hostname and vhost early.
- Enumerate all user input surfaces and rank them by impact.
- Track session and role boundaries before deeper testing.
- Look for secret sprawl, config files, and internal only services as soon as I get any foothold.

## Notes
I am not publishing flags, credentials, exploit strings, vulnerable endpoints, payloads, or step by step solution details while this target is active, per HTB guidelines.
