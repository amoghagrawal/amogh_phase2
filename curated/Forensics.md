# 1. Hide and Seek

> Sakamoto’s at it again with a game of hide and seek, but this time, it’s not with Shin or his daughter. An old friend hid some secret data in this [image](https://drive.google.com/file/d/1MoiPo-rCALJurIR1MceM_0-uiLldYVwA/view?usp=drive_link). Can you find it before the others do?


## Solution:

- The hint mentioned the use of `stegseek`
- Directly using the hint to run the command
```
stegseek sakamoto.jpg /mnt/c/users/amogh/downloads/rockyou.txt/rockyou.txt flag.txt
```
- The tool outputs
```
[i] Found passphrase: "iloveyou1"
[i] Original filename: "flag.txt".
[i] Extracting to "flag.txt".
```
- Stegseek found the hidden file named `flag.txt` and the passphrase required for it which was `iloveyou1`

## Flag:

```
nite{h1d3_4nd_s33k_but_w1th_st3g_sdfu9s8}
```

## Concepts learnt:

- Stegseek is used to find and extract hidden data from files

## Resources:

- https://github.com/RickdeJager/stegseek


***


# 2. Nutrela Chunks

> One of my favorite foods is soya chunks. But as I was enjoying some Nutrela today, I noticed a few chunks weren’t quite right. Seems like something’s off with their structure. Could you help me fix these broken chunks so I can enjoy my meal again?
> Image Link: https://drive.google.com/file/d/1sq24uSK6Upavdan4Xv58nixtqRTC44Bp/view?usp=drive_link

## Solution:

- The challenge had a corrupted png file
- Opening it in HxD and comparing to the structure of a normal png file, we find that the chunk headers - PNG, IHDR, IDAT, IEND were all misaligned
- We could confirm the same by running exiftool to get `Error : File format error`
- First we fix the header which was 20 bytes forward
- Again exiftool gave the error which was `Warning : Truncated PNG image`
- The warning was fixed by moving the END backwards by 20 bytes

## Flag:

```
nite{nOw_yOu_know_abOut_PNG_chunk5}
```

## Resources:

- https://www.researchgate.net/figure/shows-a-PNG-image-with-chunks-and-image-data-identified-The-IDAT-chunk-is-followed_fig6_220207950


***


# 3. RAR of the Abyss

> Two philosophers peer into the networked abyss and swap a secret. Use the secret to decrypt the Abyss’ RAwR and pull your flag from the void.
> Chal file: https://drive.google.com/file/d/1y3uXswPgTy4JZLo2UJX_YgcUKNaERCn8/view?usp=drive_link

## Solution:

- Using strings on the .pcap file gives us some password - `b3y0ndG00dand3vil`
```
Camus: whats the password ?
Nietzsche: b3y0ndG00dand3vil
```
- Opening the file in Wireshark and search for `rar` as the conversation and challenge description mentions
- It points us to `17	0.003489	10.0.0.20	10.0.0.10	TCP	340	53003 → 80 [PSH, ACK] Seq=1 Ack=1 Win=8192 Len=286`
- On following the TCP stream we get some raw data - `526172211a07010094.......52a94a7f`
- Saving the raw data as a [.rar file](https://drive.proton.me/urls/X9RWQT233G#f2OvlioktzbG) and extracting it using the password gives us flag.txt inside with the flag

## Flag:

```
nite{thus_sp0k3_th3_n3tw0rk_f0r3ns1cs_4n4lyst}
```

## Concepts learnt:

- Using wireshark to follow files and extracting them


***


# 4. NineTails

> Looks like I got a little too clever and hid the flag as a password in Firefox, tucked away like one of NineTails’ many tails. Recover the "logins" and the "key4" and let it guide you to the flag.
> Chal file: https://drive.google.com/file/d/1TGAwjuKp37JuQ_9JyJRAt3qkMTe5YT_U/view?usp=drive_link

## Solution:

- Open the file in FTK Imager as an image file
- Inside the file we see a user named `GIC2024` and we open that
- We then navigate to `AppData/Roaming/Mozilla/Firefox/Profils/j4gjesg4.default-release` as the hint mentioned
- We export the files from the [profile folder](https://drive.proton.me/urls/GC780MK2T0#hf1YDnZ5avVP) to use firefox decrypt on them
- On running [firefox_decrypt](https://github.com/unode/firefox_decrypt) we get
```
python3 firefox_decrypt.py /mnt/c/users/amogh/downloads/j4gjesg4.default-release
```

```
Website:   https://www.rehack.xyz
Username: 'warlocksmurf'
Password: 'GCTF{m0zarella'

Website:   https://ctftime.org
Username: 'ilovecheese'
Password: 'CHEEEEEEEEEEEEEEEEEEEEEEEEEESE'

Website:   https://www.reddit.com
Username: 'bluelobster'
Password: '_f1ref0x_'

Website:   https://www.facebook.com
Username: 'flag'
Password: 'SIKE'

Website:   https://warlocksmurf.github.io
Username: 'Man I Love Forensics'
Password: 'p4ssw0rd}'
```
- Extracting the flag from the passwords we get `GCTF{m0zarella_f1ref0x_p4ssw0rd}` which is the flag

## Flag:

```
GCTF{m0zarella_f1ref0x_p4ssw0rd}
```

## Concepts learnt:

- Browsers store user information in AppData/Roaming and cache in AppData/Local
- Firefox Decrypt is a tool to extract passwords from profiles of Mozilla if the master password is known

## Incorrect Tangents

- I initially tried opening the file with Autopsy and finding the information from there but that didnt work for me
- I also tried extracting the .ad1 file and opening it using 7zip but it didnt lead me to the information
- Using FTK I had first extracted the `j4gjesg4.default-release` folder from `Local` which only contained the cache memory and firefox decrypt didnt work on it
- It mentioned missing the key.db and logins.json file

## Resources:

- https://github.com/unode/firefox_decrypt
- https://medium.com/geekculture/how-to-hack-firefox-passwords-with-python-a394abf18016


***


# 5. Re:Draw

> Her screen went black and a strange command window flickered to life, lines of text flashed across before everything went silent. Moments later, the system crashed. By sheer luck, we recovered a memory dump. 
> Note: There are three stages to this challenge and you will find three flags.
> What we know: just before the crash, a black command window flickered across the screen, something in its output might still be visible if you dig through memory. She was drawing when it happened, and remnants of a painting program linger, which could reveal more if inspected in the right way. Finally, a mysterious archive hides deeper in memory, likely holding the last piece of her work.
> Chal file: https://drive.google.com/file/d/10bSczFPLichF-_qRXw0BYMaFvpTSwQd1/view?usp=drive_link

## Solution:

- The challenge provided us with a zip upon extracting which we get a .raw file which is a memory image dump
- The description mentioned using Volatility 2 and its plugins to get to the flags
- The challenge had 3 flags related to 3 different applications
1. A cmd window flickered just before the crash
2. MsPaint was being used before system crashed
3. An archive holding her last pieces of work
- First I ran `imageinfo` to get to know about the profile used in the memory dump
```
python2 vol.py -f /mnt/c/users/amogh/downloads/MemoryDump_Lab1.raw imageinfo
Suggested Profile(s) : Win7SP1x64, Win7SP0x64, Win2008R2SP0x64, Win2008R2SP1x64_24000, Win2008R2SP1x64_23418, Win2008R2SP1x64, Win7SP1x64_24000, Win7SP1x64_23418
```
- All the commands that I used started with `python2 vol.py -f /mnt/c/users/amogh/downloads/MemoryDump_Lab1.raw --profile=Win7SP1x64`
- I ran the plugin `clipboard` and got `St4G3$1`
- Then I ran `consoles` to get `ZmxhZ3t0aDFzXzFzX3RoM18xc3Rfc3Q0ZzMhIX0=` which when converted from Base64 gave us the first flag contained in the command prompt history - `flag{th1s_1s_th3_1st_st4g3!!}`
- On running `cmdline` we see the output which mentions a rar file called `Important.rar` which might point to the third flag
```
WinRAR.exe pid:   
1512 Command line : "C:\Program Files\WinRAR\WinRAR.exe" "C:\Users\Alissa Simpson\Documents\Important.rar"
```
- On running `filescan | grep -i "Important"` we get
```
0x000000003fa3ebc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
0x000000003fac3bc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
0x000000003fb48bc0      1      0 R--r-- \Device\HarddiskVolume2\Users\Alissa Simpson\Documents\Important.rar
```
- We can extract the file using `dumpfiles -Q 0x000000003fa3ebc0 -D extracted` to get the [.dat file](https://drive.proton.me/urls/EXGFM0P4JC#3UQWzwYp6TJL) in a folder I manually create called `extracted`
- Since it was originally a .rar file, we simply change the file extension and get [`file.None.0xfffffa8001034450.rar`](https://drive.proton.me/urls/PQ8XYR2BA8#JfvGa2Z8ESlq)
- If we try extracting the rar file it asks for a password
- Upon reading the .dat file we notice the line `Password is NTLM hash(in uppercase) of Alissa's account passwd.`
- Using hashdump we get the NTLM hash for Alissa
```
python2 vol.py hashdump -f /mnt/c/users/amogh/downloads/MemoryDump_Lab1.raw --profile=Win7SP1x64
```
```
Administrator:500:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
Guest:501:aad3b435b51404eeaad3b435b51404ee:31d6cfe0d16ae931b73c59d7e0c089c0:::
SmartNet:1001:aad3b435b51404eeaad3b435b51404ee:4943abb39473a6f32c11301f4987e7e0:::
HomeGroupUser$:1002:aad3b435b51404eeaad3b435b51404ee:f0fc3d257814e08fea06e63c5762ebd5:::
Alissa Simpson:1003:aad3b435b51404eeaad3b435b51404ee:f4ff64c8baac57d22f22edc681055ba6:::
```
- We notice that the first part is same for everyone so the hash for Alissa is `f4ff64c8baac57d22f22edc681055ba6` and converting it to uppercase gets us the password for the RAR file - F4FF64C8BAAC57D22F22EDC681055BA6
- Inside the rar we have [flag3.png](https://drive.proton.me/urls/F47Q5AKF44#N5JL0N7iwM8E) giving us the third flag which was - `flag{w3ll_3rd_stage_was_easy}`
- The second flag is related to the MsPaint so we use `psscan` to see a list of all the active processes and notice `0x000000003e8bab30 mspaint.exe        2424    604 0x000000003a581000 2019-12-11 14:35:14 UTC+0000`
- Using `memdump -p 2424 --dump-dir extracted` we get 2424.dmp file which we can rename to a .data
- On searching, I found that Gimp has the option to open raw image files so thats what I did
- A .data file doesnt have any headers so GIMP has no way to know the dimensions and we have to specify them manually
- On setting the offset to a high non zero value and the width to 1230 and height to 2000 and flipping the image vertically we get the [second flag](https://drive.proton.me/urls/83KWJ5SF70#3AIp4tPYgYlj) - `flag{Good_BoY_good_girl}`

## Flag:

```
flag{th1s_1s_th3_1st_st4g3!!}
flag{Good_BoY_good_girl}
flag{w3ll_3rd_stage_was_easy}
```

## Concepts learnt:

- A .raw file is the memory image dump of the system's RAM
- Volatility is used to conduct forensics on such files and it is known for its wide variety of plugins

## Incorrect Tangents

- After getting the hash for Alissa I initally went to run john to get the password but then I remembered rar password was just the uppercase of the NTLM hash that we got
- Used procdump with the PID of 2424 for MsPaint `procdump -p 2424 --dump-dir extracted` we get `executable.2424.exe` 
- I tried running strings on the exe to get something but the .exe didnt help
- After getting the .data file for MsPaint process I had tried opening it in Fiji and Darktable but both didnt help

## Resources:

- https://medium.com/@4aryash/forensics-using-volatility-2d9d3ef3f665
- https://www.reddit.com/r/GIMP/comments/carkpp/cant_open_a_raw_file/
- https://www.reddit.com/r/GIMP/comments/18p8o00/how_to_open_rawdata/
