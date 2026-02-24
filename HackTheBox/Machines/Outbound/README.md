# Hack The Box - Outbound

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-10

## What I learned
- Webmail is a high value target. A single RCE in a mail client stack can hand you a stable foothold fast.
- App config files often contain second order secrets, like database credentials and encryption keys.
- NOPASSWD rules are not safe by default. One misconfigured allowed command can become a clean root path.

## Non spoiler observations
- Enumeration showed SSH and an HTTP service that redirected to a mail subdomain running Roundcube.
- Initial access came from exploiting the mail application, which landed me in a low privilege web context.
- Local enumeration exposed Roundcube configuration, which included database access details and an encryption key.
- Database artifacts and email content enabled a pivot into a real user context on the host.
- Privilege escalation came from a sudo rule allowing a monitoring tool, which was exploitable through log handling behavior.

## Skills practiced
- Web surface mapping with redirects and virtual hosts.
- Vulnerability validation and controlled exploitation to obtain a foothold.
- Secret hunting in application configs, then validating impact through database queries.
- Session and data decoding to recover useful auth material.
- Sudo boundary review, then exploitation of a misconfigured allowed binary.

## Defensive takeaways
- Fix: keep webmail stacks patched, and isolate mail applications in hardened containers with minimal host access.
- Fix: store secrets outside web roots, restrict file permissions, and rotate database credentials and keys.
- Fix: avoid NOPASSWD for broad command patterns, and tightly scope allowed arguments.
- Fix: audit log directories for symlink and write protections, and ensure privileged tools cannot write to arbitrary paths.
- Detect: alert on suspicious Roundcube process behavior, unusual outbound connections, and new privileged users.

## What I would do next time
- Treat redirects to subdomains as separate apps, fingerprint them early.
- After foothold, look for app config and database access before brute forcing anything.
- When sudo is available, test allowed commands for file write and log based abuse paths.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
