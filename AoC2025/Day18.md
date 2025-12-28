# Day 18: Obfuscation - The Egg Shell File

> WareVille has not felt right since the wormhole appeared. Everyone in TBFC is on high alert: Systems are going haywire, dashboards are spiking, and SOC alerts have been firing nonstop. Amid the chaos, McSkidy keeps her focus on a particular alert that caught her interest: an email posing as northpole-hr. It’s littered with carrot emojis, but the weird thing is this: there is no North Pole human resources department. TBFC’s HR is at theSouth Pole.

## Solution

- We open the SantaStealer.ps1 script in vs code
- The comments mention the first step is to decode the C2B64 variable from Base64 which is `aHR@cHM6Ly9jMiSub3J@aHBvbGUudGhtL2V4Zmls` to get the URL `https://c2.northpole.thm/exfil`
- On running the script, we get the first flag which is `THM{C2_De0bfuscation_29838}`
- For the second question, we need to XOR the API key `CANDY-CANE-API-KEY` with the key as 0x37 and then convert it to hex
- Adding it to the code and rerunning the script we get the second flag: `THM{API_Obfusc4tion_ftw_0283}`

## Objectives

### What is the first flag you get after deobfuscating the C2 URL and running the script?
> THM{C2_De0bfuscation_29838}

### What is the second flag you get after obfuscating the API key and running the script again?
> THM{API_Obfusc4tion_ftw_0283}

## Concepts learnt:

- Learn about obfuscation, why and where it is used.
- Use CyberChef to recover plaintext safely.