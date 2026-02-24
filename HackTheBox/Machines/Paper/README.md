# Hack The Box - Paper

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-03

## What I learned
- A default looking web page can still hide a real app, you just need the right hint to reach it.
- Low impact web bugs can expose high impact secrets, like hidden links and invite tokens.
- Chat bots that can read files are risky. One path traversal style feature can become credential disclosure.
- Local privilege escalation often comes from one unpatched system component, once you have a shell.

## Non spoiler observations
- Enumeration showed SSH and an Apache web server on a CentOS host.
- The main web surface led to a WordPress instance and a hidden path that exposed extra content.
- That content pointed to an internal chat application with an invite based registration flow.
- A bot inside the chat app exposed file listing and file read behavior that leaked credentials.
- Reused credentials provided SSH access as a real user.
- Privilege escalation relied on a vulnerable local policy component present on the system.

## Skills practiced
- Web enumeration on a host that presents default content.
- Pivoting from a web app into a second internal app using discovered links.
- Testing bot commands and mapping file access controls.
- Credential validation and reuse testing for SSH access.
- Local package enumeration to identify privilege escalation candidates.

## Defensive takeaways
- Fix: keep WordPress and plugins patched, and remove leftover test content and hidden endpoints.
- Fix: treat invite links as secrets, rotate them, and restrict where they are exposed.
- Fix: lock down bot capabilities, enforce strict allowlists for file access, and remove directory traversal patterns.
- Fix: enforce unique passwords per service account and user account.
- Fix: patch privilege sensitive components like polkit, and harden local account management services.
- Detect: alert on bot file access patterns, suspicious file reads outside normal directories, and unexpected account creation.

## What I would do next time
- If the site looks empty, hunt for hidden content and alternate paths first.
- When you find a chat app, test bots and integrations early.
- After SSH access, enumerate installed packages and privilege boundaries immediately.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
