# Day 11: XSS - Merry XSSMas

> Since McSkidy’s disappearance, TBFC’s defences have weakened, and now the Email Protection Platform is down. With filters offline, the staff must triage every suspicious message manually.
The SOC Team suspects Malhare’s Eggsploit Bunnies have sent phishing messages to TBFC’s users to steal credentials and disrupt SOC-mas.

## Solution

- There are two XSS: Reflective and Stored; reflected is done immediately via a malicious link while stored happens because of malicious code on the backend server
- By running the script in the searchbox on the website in the attack box we get the first flag `THM{Evil_Bunny}`
- We send a POST command as a message and get the second flag `THM{Evil_Stored_Egg}`

## Objectives

### Which type of XSS attack requires payloads to be persisted on the backend?
> stored

### What's the reflected XSS flag?
> THM{Evil_Bunny}

### What's the stored XSS flag?
> THM{Evil_Stored_Egg}

## Concepts learnt:

- Understand how XSS works
- Learn to prevent XSS attacks