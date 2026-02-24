# Hack The Box - Devel

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Windows
- Status: Active
- Date: 2025-08-05

## What I learned
- When FTP and IIS share a writable path, it can collapse the boundary between file upload and code execution.
- Misconfigurations are often a faster win than bug hunting. Anonymous access plus a reachable web root is enough.
- Older Windows targets often hinge on local privilege escalation once you land a low privilege service context.

## Non spoiler observations
- The host exposed FTP and an IIS web service.
- FTP allowed anonymous access, which immediately raised the risk of web content tampering.
- Web content and FTP accessible directories overlapped in a way that suggested a direct path to execution.
- After initial access, the main work was moving from a low privilege service context to full control.

## Skills practiced
- Service triage and fast validation of risky combinations, FTP plus web server.
- Web root and file handling risk assessment, focusing on where uploads land.
- Post access Windows enumeration, identifying escalation paths from a service account context.
- Session handling and operational discipline, keeping access stable while escalating.

## Defensive takeaways
- Fix: disable anonymous FTP, or isolate it onto a non-executable, non-web-accessible storage path.
- Fix: enforce strict separation between upload locations and any directory the web server can execute from.
- Fix: remove legacy web server behaviors that increase risk, and keep Windows and IIS patched to current baselines.
- Detect: alert on new file creation in web directories, especially script extensions.
- Detect: monitor IIS worker processes for anomalous child process creation and outbound connections.

## What I would do next time
- Check for file upload to executable path as the first hypothesis when FTP and IIS coexist.
- Validate write permissions and execution boundaries before deeper enumeration.
- After foothold, pivot quickly into local privilege escalation checks.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
