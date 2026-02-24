# Hack The Box - Editor

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-05

## What I learned
- Multi service targets often hide a second app that matters more than the main site.
- Wiki and collaboration platforms are high risk when they allow scripting features or plugin execution paths.
- Secret reuse is still one of the fastest pivots from service access to user access.

## Non spoiler observations
- The host exposed SSH, a primary HTTP site, and a second HTTP service running a Java app stack.
- Discovery hints like redirects and robots rules suggested an additional application surface.
- After initial access, I found application configuration files containing credential material.
- Those credentials were reusable for a real user account on the host, which changed the privilege level and options.
- Privilege escalation centered on a trusted helper style binary and weak boundary controls around it.

## Skills practiced
- Multi port triage, separating main web content from the service that mattered.
- Web app enumeration strategy for platforms like wikis, focusing on features that imply code execution capability.
- Local enumeration for secrets, prioritizing application config and service directories.
- Credential handling and validation, checking for reuse in OS level authentication.
- Privilege boundary review, focusing on SUID and helper binaries and how they can be abused.

## Defensive takeaways
- Fix: keep wiki platforms patched and remove risky scripting features unless they are required and strongly controlled.
- Fix: do not store plaintext secrets in config files. Use a secret manager and restrict file permissions.
- Fix: prevent credential reuse between app services and OS accounts, enforce unique secrets and rotation.
- Fix: reduce SUID footprint and audit any privileged helper binaries for argument and path control issues.
- Detect: alert on unusual process execution from application service accounts, and on suspicious access to configuration files.

## What I would do next time
- Treat secondary services as first class targets, especially Java stacks and wiki platforms.
- After foothold, look for secret material early, then test reuse safely.
- Enumerate privileged helpers with a boundary mindset, not only a CVE mindset.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
