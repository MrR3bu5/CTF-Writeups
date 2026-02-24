# <Platform> - <TargetName>

## Metadata
- Platform: <HackTheBox | TryHackMe | VulnHub | PortSwigger | Other>
- Target: <Name>
- Category: <Machine | Fortress | Challenge | Room | Lab>
- OS: <Linux | Windows | Other>
- Difficulty: <Easy | Medium | Hard | Insane>
- Status: <Retired | Active | N/A>
- Date completed: <YYYY-MM-DD>

## Scope and rules
- Allowed actions: <What you allowed yourself to do>
- Excluded from this writeup: flags, passwords, tokens, private keys, direct copy and paste exploit strings, active target spoilers. [web:17]

## Goal
- Objective: <Get user flag, root, complete fortress, solve challenge>
- Success criteria: <What you count as done>

## High level attack path
- Entry point: <Service or bug class>
- Privilege escalation: <Bug class or misconfig>
- Key pivot: <One turning point>

## Recon
### What I enumerated
- Network: <Ports and services at a high level>
- Web: <Hosts, apps, tech stack at a high level>
- Auth: <Any auth boundaries you identified>
- AD: <Only if relevant>

### What mattered
- Finding 1: <One sentence>, proof: <artifact filename>
- Finding 2: <One sentence>, proof: <artifact filename>

### What I ignored and why
- Item 1: <One sentence>
- Item 2: <One sentence>

## Initial access
### Hypothesis
- Why this path: <1 to 2 sentences>

### Steps taken
1. Step 1: <Action and result>
2. Step 2: <Action and result>
3. Step 3: <Action and result>

### Proof
- Evidence: <artifact filename>
- Resulting access: <User, service, or foothold>

## Privilege escalation
### Enumeration
- Checks run: <High level list>
- Signal: <What stood out>

### Escalation method
- Root cause: <Misconfig | vuln | weak perms | injection | deserialization | credential reuse>
- Why it worked: <1 to 2 sentences>

### Proof
- Evidence: <artifact filename>
- Final access: <root, SYSTEM, admin>

## Post exploitation
- Data accessed: <High level>
- Lateral movement: <If any, high level>
- Cleanup: <What you removed or avoided changing>

## Defensive takeaways
- Fix: <One concrete fix you would ship>
- Detect: <One log source plus detection idea>
- Prevent: <One hardening control>
- Validation: <How to confirm the fix worked>

## Timeline
- T0: Start
- T1: Foothold
- T2: Privilege escalation
- T3: Done

## Artifacts
- artifacts/: screenshots, trimmed outputs, diagrams
- files/: scripts, configs, notes, sanitized

## References
- Official docs: <links>
- Vendor advisory or CVE: <links>
- Tool docs: <links>
