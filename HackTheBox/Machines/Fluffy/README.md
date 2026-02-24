# Hack The Box - Fluffy

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Windows
- Status: Active
- Date: 2025-08-08

## What I learned
- Writable SMB shares are not just data exposure, they are delivery paths into user workflows. 
- One captured NetNTLMv2 response can become a full credential pivot when password hygiene is weak. 
- ADCS is an escalation surface. Even when the CA is hard to query, templates and group membership still matter. 

## Non spoiler observations
- Enumeration identified this host as a domain controller, with LDAP and Kerberos exposed and SMB signing required. 
- A known domain user had read and write access to an IT share, which gave me a place to plant a file. 
- A user interaction flow triggered authentication to my infrastructure, which let me capture a NetNTLMv2 challenge response. 
- Cracking that response provided a second set of domain credentials and expanded what I could query in AD. 
- I moved into ADCS enumeration and then used AD group membership changes to progress. 

## Skills practiced
- Domain controller triage from port and service signals, LDAP, Kerberos, and certificate services. 
- SMB share analysis, validating access levels and identifying realistic delivery points. 
- Credential capture and pivoting, turning a captured auth exchange into a new authenticated identity. 
- ADCS discovery workflow, locating CAs and enabled templates, exporting BloodHound compatible data. 
- AD object control checks, validating whether a low privilege user can modify group membership. 

## Defensive takeaways
- Fix: remove write access on broad SMB shares, apply least privilege, and separate software distribution from user writable paths. 
- Fix: enforce strong passwords and rotation, prioritize accounts that touch shared resources and service groups. 
- Fix: harden name resolution and auth capture paths, and disable protocols and behaviors that allow credential interception on untrusted networks. 
- Fix: review ADCS template security and who can enroll, and tightly control membership of privileged groups like service account operator groups. 
- Detect: alert on new or modified archives and executables in shared drives, and monitor unusual outbound authentication attempts. 
- Detect: alert on group membership changes, especially additions into service related groups and admin adjacent groups. 

## What I would do next time
- Start with SMB share mapping as soon as I see a domain controller and any writable share. 
- Look for user driven file processing paths, then validate what authentication leaks they can cause. 
- When ADCS exists, enumerate templates early and track what group changes unlock next. 

## Notes
I am not publishing flags, hashes, exploit strings, payloads, or step by step solution details while this target is active. 
