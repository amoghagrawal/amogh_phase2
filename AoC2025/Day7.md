# Day 7: Network Discovery - Scan-ta Clause

> Christmas preparations are delayed - HopSec has breached our QA environment and locked us out! Without it, the TBFC projects can't be tested, and our entire SOC-mas pipeline is frozen. To make things worse, the server is slowly transforming into a twisted EAST-mas node. <br>
> Can you uncover HopSec's trail, find a way back into tbfc-devqa01, and restore the server before the bunny's takeover is complete? For this task, you'll need to check every place to hide, every opened port that bunnies left unprotected. Good luck!

## Solution

- The challenge requires using NMap to get the key
Using the command `ftp 10.49.170.124 21212` we get the first part of the key which is `3aster_`
- Using the next few commands, we get the second part which is `15_th3_`
```
nc -v  10.49.170.124 25251
HELP
GET KEY
```
- We get the third part from `dig @10.49.170.124 TXT key3.tbfc.local +short` which is `m3w_xm45`
- Opening the website, on the banner we see the msg `Pwned by HopSec` which is the first answer
- Entering the full key onto the admin panel, we get access to the website terminal and we can run the command `ss -tunlp` to find the MySQL database running on `3306` port which is also the default
- By running `select * from flags;` we get the final flag from the database

## Objectives

### What evil message do you see on top of the website?
> Pwned by HopSec

### What is the first key part found on the FTP server?
> 3aster_

### What is the second key part found in the TBFC app?
> 15_th3_

### What is the third key part found in the DNS records?
> n3w_xm45

### Which port was the MySQL database running on?
> 3306

### Finally, what's the flag you found in the database?
> THM{4ll_s3rvice5_d1sc0vered}

## Concepts learnt:

- Learn the basics of network service discovery with Nmap
- Learn core network protocols and concepts along the way