# Hack The Box - Code

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-02

## What I learned
- If a service runs user supplied code, the first risk to test is sandbox escape, not missing endpoints. 
- Local files and app databases often contain credential material. You need a fast process to find and assess it. 
- Backup tooling is a common privilege boundary. Config validation errors can turn safe helpers into data exposure. 

## Non spoiler observations
- The target exposed SSH and a web service hosting an online Python code editor. 
- The Python execution environment allowed access to more runtime capability than expected for an editor. This shifted my focus to containment and execution boundaries. 
- After initial access, I found an application data store that contained user records and credential material. I did not publish values. 
- The host had a privileged backup workflow that accepted a task definition file and enforced path restrictions. The restriction logic was weaker than intended. 

## Skills practiced
- Service triage and risk ranking, prioritizing “code execution service” containment testing. 
- Post-access local enumeration, focusing on app config, instance data, and lightweight databases. 
- Credential risk handling, identifying reuse opportunities without exposing any secrets publicly. 
- Linux privilege boundary review, focusing on sudo rules and helper scripts. 
- Input validation review for configuration driven tooling. 

## Defensive takeaways
- Fix: run any code editor or execution service in a locked down sandbox, remove OS level escape primitives, and restrict outbound network access. 
- Fix: treat app databases as sensitive, enforce file permissions, avoid storing reusable secrets, and use strong password hashing. 
- Fix: for privileged backup jobs, use an allowlist that cannot be bypassed by path normalization edge cases, and validate the final resolved path. 
- Detect: alert on abnormal process spawning from the web app user, and on unexpected outbound connections from the app service. 
- Detect: log and alert on unusual backup task submissions, especially tasks that target privileged directories or change destinations unexpectedly. 

## What I would do next time
- Test the runtime boundary first on any “online code runner” feature.
- After foothold, hunt for secrets in app instance folders and small databases early.
- Review sudo rules for helper scripts and check how they normalize and validate paths.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active, per HTB guidelines.
