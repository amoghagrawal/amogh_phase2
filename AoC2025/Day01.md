# Day 1: Linux CLI - Shells Bells

> The unthinkable has happened - McSkidy has been kidnapped. Without her, Wareville’s defenses are faltering, and Christmas itself hangs by a thread. But panic won’t save the season. A long road lies ahead to uncover what truly happened. The TBFC (The Best Festival Company) team already brainstorms what to do next, and their first lead points to the tbfc-web01, a Linux server processing Christmas wishlists. Somewhere within its data may lie the truth: traces of McSkidy’s final actions, or perhaps the clues to King Malhare’s twisted vision for EASTMAS.

## Solution

- The challenge is based on basic linux shell commands
- The first task was to navigate to the Guides directory using `cd Guides` and look at the files there
- I found a `.guide.txt` using `ls -a`
- Opening the guide using `cat` gives us the flag for the first flag
- Next we had to look for "eggsploits" and "eggsplits" which we can do using `find` in `/home/socmas` as mentioned
- We find `eggstrike.sh` in `/home/socmas/2025` which contains the second flag
- The third flag is in the bash history so we switch to the root user using `sudo su` first
- Using the `history` command we get the third and final flag

## Objectives

### Which CLI command would you use to list a directory?
> ls

### What flag did you see inside of McSkidy’s guide?
> THM{learning-linux-cli}

### Which command helped you filter the logs for failed logins?
> grep

### What flag did you see inside the Eggstrike script?
> THM{sir-carrotbane-attacks}

### Which command would you run to switch to the root user?
> sudo su

### Finally, what flag did Sir Carrotbane leave in the root bash history?
> THM{until-we-meet-again}