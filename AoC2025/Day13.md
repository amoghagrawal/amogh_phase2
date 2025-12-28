# Day 13: YARA Rules - YARA mean one!

> When McSkidy went missing, there was chaos and uncertainty at The Best Festival Company (TBFC). However, even in her disappearance, McSkidy was trying to help the TBFC blue team. Taking a page out of the crisis communication process, McSkidy sent what looks like a bunch of images to the blue team from an anonymous location. These images looked like they were related to Easter preparations, but they contained a message sent by McSkidy. 

## Solution

- We have the files in the  `/home/ubuntu/Downloads/easter`
- The challenge requires us to use Yara which is a pattern matching tool for files and memory to detect malicious files
- By running `nano easter.yara` and writing the condition
```
{
    strings:
            $s1 = "TBFC"
    condition:
            all of them
}
```
- By running `-r` to scan the directories using `yara -r easter.yara .` we get 5 jpeg images containing the string
- By following the regex from the regular expression we get `/TBFC:[A-Za-z0-9]+/` as the second answer
- We can check the regex on regex101 to confirm as well
- By running `-s` in the previous command we can see the strings found in the command
- By running `yara -r -s easter.yara .` we get the 5 parts of the flag to get the final flag as `Find me in HopSec Island`

## Objectives

### How many images contain the string TBFC?
> 5

### What regex would you use to match a string that begins with TBFC: followed by one or more alphanumeric ASCII characters?
> /TBFC:[A-Za-z0-9]+/

### What is the message sent by McSkidy?
> Find me in HopSec Island

## Concepts learnt:

- Understand the basic concept of YARA
- Learn how to write YARA rules