# Hack The Box - Fortress - Jet

## Metadata
- Platform: HackTheBox
- Target: Jet
- Category: Fortress
- OS: Linux
- Status: Retired or allowed for public writeup
- Date completed: 2025-10-12

## Scope and rules
I removed flags, credentials, private keys, and copy and paste exploit strings.
I focus on the attack chain, what I observed, and what I would fix. 

## Goal
Gain administrative control of the exposed applications and prove privileged access through evidence, without publishing sensitive values. 

## High level attack path
1. Network enumeration revealed DNS and multiple web services. 
2. Reverse DNS exposed an internal hostname, which expanded the web attack surface via virtual host routing. 
3. Client side JavaScript contained an obfuscated route to an admin interface. 
4. The admin login was vulnerable to SQL injection, enabling database enumeration and credential recovery. 
5. Authenticated access exposed additional functionality that enabled command execution and a shell. 

## Recon
### What I enumerated
- TCP services: SSH, DNS, HTTP, and several custom high ports. 
- DNS: reverse lookup for host discovery. 
- Web: initial landing page, then a discovered virtual host with additional content. 

### What mattered
- DNS answered authoritatively and returned an internal hostname via PTR lookup. 
- A local JavaScript file contained encoded logic that revealed a hidden admin directory. 

### What I ignored and why
- I did not brute force SSH because the web surface provided clear leads and multiple app level trust boundaries. 

## Initial access
### Hypothesis
If the app hides admin routes in client side code, server side access control is likely weak. That made web testing the fastest path. 

### Steps taken
1. Enumerated open ports and identified DNS and HTTP services. 
2. Performed reverse DNS lookup and added the discovered hostname for browsing. 
3. Retrieved and analyzed the JavaScript loaded by the site, then decoded the encoded logic to recover the hidden admin path. 
4. Opened the admin login and tested input handling, then confirmed SQL injection in the authentication flow using controlled probes. 

### Proof
- Evidence: nmap output, reverse DNS output, decoded JS, and captured proxy request for the login workflow. Store these as screenshots in `artifacts/`. 

## Privilege escalation
### Enumeration
- After confirming injection, I enumerated database names, tables, and the user table used by the admin login. 

### Escalation method
- Root cause: unparameterized SQL queries in the login flow. 
- Impact: database extraction enabled offline password cracking and reuse of recovered credentials. I do not publish the values. 

### Proof
- Evidence: redacted database dump output, and authenticated dashboard access screenshot. 

## Post exploitation
With authenticated dashboard access, additional admin functionality became available.
One feature accepted user controlled input and executed system commands, which I used to obtain a shell. I removed the exact payload. 

## Defensive takeaways
- Fix: use parameterized queries for all database interactions, especially authentication. 
- Fix: remove sensitive routes from client side code, enforce server side authorization checks for all admin paths. 
- Fix: store passwords using adaptive hashing with salts, enforce strong credential policy. 
- Detect: alert on SQLi indicators at the WAF or app layer, for example boolean patterns, union patterns, and time delays on the login endpoint. 
- Detect: log and alert on command execution attempts and unexpected child process spawning from the web server user. 

## Timeline
- T0: Port scan and service ID. 
- T1: Reverse DNS and vhost discovery. 
- T2: JS analysis to locate admin route. 
- T3: SQL injection confirmed and database enumerated. 
- T4: Authenticated dashboard access. 
- T5: Command execution to shell. 

## Artifacts
- `artifacts/`: screenshots of nmap, dig, admin panel, and redacted tool output.
- `files/`: any helper scripts.
