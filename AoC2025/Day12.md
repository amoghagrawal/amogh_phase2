# Day 12: Phishing - Phishmas Greetings

> Since McSkidy’s disappearance, TBFC’s defences have weakened, and now the Email Protection Platform is down. With filters offline, the staff must triage every suspicious message manually.
The SOC Team suspects Malhare’s Eggsploit Bunnies have sent phishing messages to TBFC’s users to steal credentials and disrupt SOC-mas.

## Solution

- We need to classify the email correctly as spam or phishing to get the flag
- The first email is Phishing and the signals are Spoofing, Sense of Urgency and Fake Invoice
- The second email is Phishing and the signals are Impersonation, Spoofing and Malicious Attachment
- The signals in the third were Impersonation, Social Engineering Text and Sense of Urgency
- The fourth were Impersonation, External Sender Domain and Social Engineering Text
- The fifth email is just spam
- The sixth email is phishing and the signals are Impersonation, Typosquatting/Punycodes and Social Engineering Text

## Objectives

### Classify the 1st email, what's the flag?
> THM{yougotnumber1-keep-it-going}

### Classify the 2nd email. What's the flag?
> THM{nmumber2-was-not-tha-thard!}

### Classify the 3rd email. What's the flag?
> THM{Impersonation-is-areal-thing-keepIt}

### Classify the 4th email. What's the flag?
> THM{Get-back-SOC-mas!!}

### Classify the 5th email. What's the flag?
> THM{It-was-just-a-sp4m!!}

### Classify the 6th email. What's the flag?
> THM{number6-is-the-last-one!-DX!}

## Concepts learnt:

- Spotting phishing emails
- Learn trending phishing techniques
- Understand the differences between spam and phishing