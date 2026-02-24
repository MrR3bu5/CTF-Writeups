# Hack The Box - Expressway

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-09-21

## What I learned
- VPN and remote access services are a real entry point, even when there is no web app to attack.
- Weak shared secrets turn strong protocols into an offline guessing problem.
- Local privilege escalation on Linux is often about version awareness and careful validation of sudo boundaries.

## Non spoiler observations
- The initial attack surface was not a website. It looked like a remote access service workflow.
- Early enumeration produced an identity hint that helped focus authentication testing.
- I validated that the environment allowed offline style secret guessing, which led to a usable access path.
- After getting a user level foothold, I shifted to local enumeration and found a privilege boundary related to sudo.

## Skills practiced
- Network service triage on non HTTP targets.
- VPN and IKE reconnaissance mindset, focusing on what can be learned without credentials.
- Offline secret risk evaluation and controlled validation.
- Post access Linux enumeration, focusing on sudo version and configuration boundaries.
- Privilege escalation planning, starting with safe checks and only then moving to exploitation.

## Defensive takeaways
- Fix: avoid aggressive mode style exposures and reduce information leakage in remote access handshakes.
- Fix: require strong pre shared keys, rotate them, and enforce lockout and monitoring for repeated auth failures.
- Fix: keep sudo patched and monitor for known local escalation risks tied to specific versions.
- Detect: alert on repeated handshake attempts and enumeration patterns against remote access services.
- Detect: log sudo usage and alert on unusual invocations and unexpected environment or root context transitions.

## What I would do next time
- If HTTP is absent, pivot immediately into VPN, auth, and management protocols.
- Treat handshake metadata as actionable intelligence, then validate carefully.
- Once in, check sudo and local privilege boundaries early.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
