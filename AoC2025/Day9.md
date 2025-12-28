# Day 9: Passwords - A Cracking Christmas

> With time between Easter and Christmas being destabilised, the once-quiet systems of The Best Festival Company began showing traces of encrypted data buried deep within their servers. Sir Carrotbane, stumbled upon a series of locked PDF and ZIP files labelled “North Pole Asset List.” Rumours spread that these could contain fragments of Santa’s master gift registry, critical information that could help Malhare control the festive balance between both worlds. <br>
> Sir Carrotbane sets out to crack the encryption, learning how weak passwords can expose even the most guarded secrets. Can the Elves adapt fast and prevent their secrets from being discovered?

## Solution

- In the desktop directory we find the flag.pdf file which we need to unlock
- By running `pdfcrack -f flag.pdf -w /usr/share/wordlists/rockyou.txt` we get the password as `naughtylist` and the flag inside as `THM{Cr4ck1ng_PDFs_1s_34$y}`
- For the zip file we use john, by running `zip2john flag.zip > ziphash.txt` first for a file which john can read
- We run the command `john --wordlist=/usr/share/wordlists/rockyou.txt ziphash.txt` and weget the pass as `winter4ever`
- We get the flag in the zip file as `THM{Cr4ck1n6_z1p$_1s_34$yyyy}`

## Objectives

### What is the flag inside the encrypted PDF?
> THM{Cr4ck1ng_PDFs_1s_34$y}

### What is the flag inside the encrypted zip file?
> THM{Cr4ck1n6_z1p$_1s_34$yyyy}

## Concepts learnt:

- How password-based encryption protects files such as PDFs and ZIP archives.
- Why weak passwords make encrypted files vulnerable.