# Hack The Box - Soulmate

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-09-26

## What I learned
- Subdomain discovery can expose a second application that is the real entry point.
- A web facing management service can fail closed in the UI and still be vulnerable behind the scenes.
- Post exploit enumeration can reveal local only services that bypass sudo entirely.
- If a local service supports command execution, it becomes your privilege escalation path.

## Non spoiler observations
- Enumeration showed SSH and an nginx web service that redirected to a hostname.
- Directory discovery on the main site was minimal, which pushed the focus toward subdomains and alternate services.
- A vulnerable service allowed creation of a new account, which enabled authenticated access.
- That access led to a web shell style foothold and local enumeration.
- Local enumeration revealed credentials for a real system user, which provided stable SSH access.
- Privilege escalation came from a local only SSH style service on a high port that dropped into an Erlang shell.
- From that shell, OS command execution ran as root.

## Skills practiced
- Virtual host and subdomain enumeration.
- Service version mapping and exploit validation.
- Web foothold setup, then rapid local enumeration with automated tooling.
- Credential hunting in application configs and scripts.
- Privilege escalation through local service discovery and trusted localhost access paths.

## Defensive takeaways
- Fix: restrict administrative services to internal networks, and patch or disable vulnerable versions.
- Fix: enforce strong separation between web app context and host execution context.
- Fix: treat localhost bound services as privileged surfaces, require authentication and restrict who can reach them.
- Fix: remove plaintext credentials from scripts and configuration, and rotate any exposed passwords.
- Detect: alert on new user creation in admin services, unexpected web shells, and outbound reverse connections.
- Detect: monitor for connections to unusual local ports and for command execution from service accounts.

## What I would do next time
- If the main app looks thin, prioritize subdomain fuzzing early.
- After you get any foothold, enumerate listening ports and local services before chasing kernel exploits.
- When you find a localhost only control interface, test it as a privilege escalation path fast.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
