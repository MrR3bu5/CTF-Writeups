# Hack The Box - Imagery

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-09-27

## What I learned
- File upload features can turn into account takeover when the app renders user content unsafely.
- A single leaked session cookie can be enough to pivot into admin only functionality.
- Path traversal bugs often chain into credential discovery when apps expose logs or config artifacts.

## Non spoiler observations
- The host exposed SSH and a Python web app on port 8000.
- The app supported image uploads, and its handling of user supplied content created an execution path in the browser.
- After I gained elevated access in the app, I found an admin endpoint that allowed reading unintended files.
- That file read primitive exposed stored credentials, which I used to move from app access to host access.
- Privilege escalation relied on a scheduled task style workflow available through a local admin tool.

## Skills practiced
- Web enumeration on non standard ports, fingerprinting frameworks and endpoints.
- Testing file upload boundaries, focusing on rendering, sanitization, and content type assumptions.
- Session handling and cookie based pivoting.
- Finding and exploiting path traversal to access secrets.
- Linux post exploit enumeration, then validating safe privilege escalation paths.

## Defensive takeaways
- Fix: sanitize and validate uploaded content, enforce server side type checks, and do not inline render untrusted SVG or HTML.
- Fix: use httpOnly and secure cookie settings, rotate sessions, and bind sessions to device signals where possible.
- Fix: prevent traversal by canonicalizing paths and using allowlists for log identifiers.
- Fix: never store plaintext credentials in web accessible or readable files, and restrict access to config and database files.
- Fix: audit local admin tools that can schedule commands, enforce least privilege and strong authentication.

## What I would do next time
- Prioritize upload and render flows early, then test for client side execution.
- If you gain a session token, validate role boundaries before running deeper scans.
- When you have file read, hunt for config, database files, and secrets that enable an OS foothold.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
