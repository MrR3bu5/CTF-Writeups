# Hack The Box - Nibbles

## Metadata
- Platform: HackTheBox
- Category: Machine
- OS: Linux
- Status: Active
- Date: 2025-08-05

## What I learned
- Always validate hidden paths on simple web pages, the real app can live under a subdirectory.
- Exposed config files can hand you usernames and reduce password guessing to one high confidence attempt.
- Post exploitation on easy Linux boxes often comes down to one mismanaged script or scheduled task.

## Non spoiler observations
- Enumeration showed SSH and a basic Apache site, with the real target content under a blog path.
- Directory discovery revealed an admin area and readable XML files that exposed useful context.
- Valid credentials provided access to the admin panel, which enabled a file upload style foothold.
- After foothold, I located the user flag in the home directory.
- Root access came from abusing a locally accessible script or maintenance workflow found in user owned files.

## Skills practiced
- Web content discovery using directory brute forcing.
- Config and metadata mining from exposed files.
- Picking a known exploit path based on product and version signals.
- Remote session navigation, file search, and artifact collection.
- Local enumeration focused on user writable scripts and privilege boundaries.

## Defensive takeaways
- Fix: block access to sensitive XML and config files, enforce proper web root permissions.
- Fix: require strong admin credentials and remove default or guessable passwords.
- Fix: restrict file upload capabilities and validate file types and destinations.
- Fix: audit scripts that run with elevated rights, and remove write access for untrusted users.
- Detect: alert on new or modified files under web app plugin or upload directories.

## What I would do next time
- Start with quick content discovery, then focus on the admin surface.
- Check for exposed config and user files before heavy exploitation.
- After foothold, enumerate for writable scripts and misconfigured sudo paths fast.

## Notes
I am not publishing flags, credentials, exploit strings, payloads, vulnerable endpoints, or step by step solution details while this target is active.
