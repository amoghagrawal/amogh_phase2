# Day 15: Web Attack Forensics - Drone Alone

> TBFC’s drone scheduler web UI is getting strange, long HTTP requests containing Base64 chunks. Splunk raises an alert: “Apache spawned an unusual process.” On some endpoints, these requests cause the web server to execute shell code, which is obfuscated and hidden within the Base64 payloads. For this room, your job as the Blue Teamer is to triage the incident, identify compromised hosts, extract and decode the payloads and determine the scope.

## Solution

- The initial phase of hacking or the "reconnaissance" exe file is generally whoami to to determine which user account they are running as
- We can set the search time frame as `All Time`
- We can run the command `index=windows_sysmon *cmd.exe* *whoami*` in splunk and in the results, we see an entry with the command whoami in the cmdline
- Seeing the OriginalFileName of that command we get the first answer: whoami.exe
- By running `index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")` we see a command on the powershell trying to run a script called powershell.exe with an evil msg in base64

## Objectives

### What is the reconnaissance executable file name?
> whoami.exe

### What executable did the attacker attempt to run through the command injection?
> powershell.exe

### What's the flag?
> THM{DOCKER_ESCAPE_SUCCESS}

## Concepts learnt:

- Detect and analyze malicious web activity through Apache access and error logs
- Investigate OS-level attacker actions using Sysmon data