# Day 5: IDOR - Santa’s Little IDOR

> The elves of Wareville are on high alert since McSkidy went missing. Recently, the support team has been receiving many calls from parents who can't activate vouchers on the TryPresentMe website. They also mentioned they are receiving many targeted phishing emails containing information that is not public. The support team is wary and has enlisted the help of the TBFC staff. When looking into this peculiar case, they discovered a suspiciously named account named Sir Carrotbane, which has many vouchers assigned to it. For now, they have deleted the account and retrieved the vouchers. But something is going on. Can you help the TBFC staff investigate the TryPresentMe website and fix the vulnerabilities?

## Solution

- To get the user id of the parent which had 10 children we had to manually increment the user_id by 1 and check for the desired result in the output json
- By setting the user_id to `15` in the GET request we get 10 children - `http://MACHINEIP/api/parents/view_accountinfo user_id=15`

## Objectives

### What does IDOR stand for?
> Insecure Direct Object Reference

### What type of privilege escalation are most IDOR cases?
> Horizontal

### Exploiting the IDOR found in the `view_accounts` parameter, what is the `user_id` of the parent that has 10 children?
> 15

## Concepts learnt:

- Exploit IDOR to perform horizontal privilege escalation
- IDOR is a flaw when an app exposes internal database IDs in URLs or forms letting people abuse them or change them to access other people's data wihout authorization