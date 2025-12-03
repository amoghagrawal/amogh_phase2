# Day 2: Phishing - Merry Clickmas

> In light of several recent cyber security threats against The Best Festival Company (TBFC), the local red team has scheduled several penetration tests. The red teamers proceeded to carry out a regular penetration test against their TBFC. Part of this exercise is to ensure that the employees are diligent when clicking links and that the company is well protected against the latest phishing attacks. This type of authorised phishing is a proven way to learn whether the cyber security awareness training has fruited.
> In this task, you will be part of the TBFC local red team with the elves Recon McRed, Exploit McRed, and Pivot McRed. You will help them plan and execute their phishing campaign. It is time to see if more cyber security awareness training is required.

## Solution

- Host the fake login page from the attack machine by running the script `./server.py`
- Using Social-Engineer-Toolkit (SET) to create and send the phishing email
- We start the tool using `setoolkit` and chose `Social Engineering Attacks`
- Then we want it to be `Masds Mailer Attack` and then since we only want to send an email to a single person we chose `E-Mail Attack Single Email Address`
- Setting the from, to and the method to deliver the email as `Use your own server or open relay` we write the body of the email to contain the fake login page `http://CONNECTION_IP:8000`
- We get the credentials on the fake login page after a few minutes as `admin` and `unranked-wisdom-anthem` which is the first answer
- Using the password and the username as `factory` we can login to `http://MACHINE_IP` to access the mailbox which contains the total number of toys expected for delivery which is the second answer

## Objectives

### What is the password used to access the TBFC portal?
> unranked-wisdom-anthem

### What is the total number of toys expected for delivery?
> 1984000

## Concepts learnt:

- How to get senstitive information (social engineering) using phishing
- Explore and host a fake login page
