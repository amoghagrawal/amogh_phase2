# Day 16: Forensics - Registry Furensics

> TBFC is under attack. Systems are exhibiting weird behavior, and the company is now feeling the absence of its lead defender, McSkidy. However, McSkidy made sure the legacy continues. <br>
> They have now decided to conduct a detailed forensic analysis on one of the most critical systems of TBFC, dispatch-srv01. The dispatch-srv01 coordinates the drone-based gifts delivery during SOCMAS. However, recently it was compromised by King Malhare’s bandits of bunnies.

## Solution

- For the first qustion to see the programs, we load the `SOFTWARE` file in the registry explorer
- We open files while pressing SHIFT
- In the available bookmarks in Uninstall (HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall) we see a file called `DroneManager Updater` on 21st October when the activity started
- For the second question we open `NTUSER.dat` in the UserAssist we find an entry for DroneMananger with the file path as `C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe`
- For the value added we again go to `SOFTWARE` and in `CurrentVersion/Run` we get the value as `"C:\Program Files\DroneManager\dronehelper.exe" --background`

## Objectives

### What application was installed on the dispatch-srv01 before the abnormal activity started?
> DroneManager Updater

### What is the full path where the user launched the application (found in question 1) from?
> C:\Users\dispatch.admin\Downloads\DroneManager_Setup.exe

### Which value was added by the application to maintain persistence on startup?
> "C:\Program Files\DroneManager\dronehelper.exe" --background

## Concepts learnt:

- Understand what the Windows Registry is and what it contains.
- Dive deep into Registry Hives and Root Keys.
- Analyze Registry Hives through the built-in Registry Editor tool.