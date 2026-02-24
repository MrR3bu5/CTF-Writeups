# Hack The Box - Legacy

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Windows
- Status: Active
- Date: 2025-08-04

## What I learned
- Old Windows builds often fall fast once you confirm SMB exposure and OS version.
- SMB misconfigurations like disabled signing are a strong risk signal on legacy hosts.
- If you can get remote code execution over SMB, you usually land straight into full host compromise.

## Non spoiler observations
- Enumeration showed a legacy Windows target exposing RPC and SMB.
- Service fingerprinting pointed to Windows XP era SMB behavior.
- The primary path focused on an SMB remote code execution class issue, not web exploitation.
- After a session was established, locating user and admin artifacts was straightforward.

## Skills practiced
- SMB and RPC enumeration for OS identification.
- Rapid exploit selection based on version and service exposure.
- Session management and file system search for sensitive artifacts.
- Operational discipline on older targets, keeping actions minimal and stable.

## Defensive takeaways
- Fix: remove or isolate SMB on untrusted networks, especially on legacy Windows systems.
- Fix: enforce SMB signing and modern SMB versions, and disable SMB1 wherever possible.
- Fix: patch or retire unsupported operating systems, then verify with authenticated vulnerability scanning.
- Detect: alert on RPC and SMB scanning patterns and on anomalous SMB activity from non admin workstations.

## What I would do next time
- Confirm OS and SMB dialect early, then validate likely exploit paths.
- If you get a session, move quickly to proof of impact and stop.
- Capture evidence cleanly, then pivot to hardening guidance.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
