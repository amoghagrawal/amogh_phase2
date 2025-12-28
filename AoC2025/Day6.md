# Day 6: MAlare Analysis — Egg-xecutable

> "Why is Elf McClause working at 3AM?" Screams a member of the SOC team in the background. They're right, something is amiss. <br>
> Elf McBlue is immediately suspicious. Their years of experience in the SOC have given them the wisdom not to download "out of the blue" executables. Without McSkidy's wisdom, Elf McBlue takes charge, loading up their malware investigation toolkik - the investigation begins.

## Solution

- For the initial static analysis, we launch PeStudio and get the SHA256 value of the .exe
- In the strings section at the bottom we find the THM flag which is the answer to the second question
- For dynamic analysis, we use Regshot, we set the output path as the desktop and do the first shot
- Now we execute the HopHelper.exe and all the icons on the desktop change
- We now run a second shot on Regshot and now we compare both to find the file path with the first directory of 3 characters as `HKU\S-1–5–21–1966530601–3185510712–10604624–1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper` which is the thrid answer
- We execute the .exe file again and open ProcMon
- Using ProcMon or process monitor, we apply filters:
1. Process Name is HopHelper.exe
2. Operation contains CCP
- In the path we that the exe is using `http` as the protocol

## Objectives

### Static analysis: What is the SHA256Sum of the HopHelper.exe?
> F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33

### Static analysis: Within the strings of HopHelper.exe, a flag with the format THM{XXXXX} exists. What is that flag value?
> THM{STRINGS_FOUND}

### Dynamic analysis: What registry value has the HopHelper.exe modified for persistence?
> HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper: “C:\Users\DFIRUser\Desktop\HopHelper\HopHelper.exe

### Dynamic analysis: Filter the output of ProcMon for "TCP" operations. What network protocol is HopHelper.exe using to communicate?
> http

## Concepts learnt:

- The principles of malware analysis
- Static vs. dynamic analysis
- How to use tools like PeStudio, ProcMon, Regshot
- ProcMon shows us what exactly the process does