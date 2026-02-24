# Hack The Box - Planning

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-09

## What I learned
- Subdomain discovery can reveal the real target fast, even when the main site looks like a template.
- Authenticated RCE in observability tools is a direct path to full compromise when patching lags.
- Secrets in environment variables are still secrets. If you get code execution, you can often read them.
- Internal only services can become reachable through SSH port forwarding, which changes your options.

## Non spoiler observations
- Enumeration showed SSH and an nginx site that redirected to a hostname.
- Fuzzing found a Grafana subdomain, which became the primary attack surface.
- Exploiting the Grafana instance gave code execution and immediate high privilege access in that context.
- From that access, I recovered additional credentials from environment variables and pivoted to a real user shell.
- Local enumeration revealed a job scheduling system and a local only web interface.
- Port forwarding let me interact with the internal service and create a job that copied sensitive data into a readable location.

## Skills practiced
- Virtual host and subdomain discovery.
- Application versioning and exploit selection.
- Credential discovery in process environments and config paths.
- SSH port forwarding to reach localhost bound services.
- Abuse of job schedulers and backup style tasks for controlled data access.

## Defensive takeaways
- Fix: patch and harden Grafana, and restrict admin access to internal networks only.
- Fix: do not store privileged secrets in environment variables, use a secret manager with strict access controls.
- Fix: lock down internal admin panels, require strong auth, and limit what scheduled jobs can execute.
- Fix: audit cron and scheduler job definitions for dangerous commands and data exfil paths.
- Detect: alert on new scheduled jobs, changes to scheduler databases, and unexpected access to localhost bound services via SSH tunnels.

## What I would do next time
- If the front page looks generic, hunt for subdomains and alternate apps early.
- After app RCE, check env, config, and mounted volumes for pivot credentials fast.
- Enumerate internal services with local port checks, then decide if port forwarding is worth it.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
