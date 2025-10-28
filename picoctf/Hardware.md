# 1. IQ Test

> let your input x = 30478191278. <br>
> wrap your answer with nite{ } for the flag. <br>
> As an example, entering x = 34359738368 gives (y0, ..., y11), so the flag would be nite{010000000011}.

## Solution:

- The challenge had a combination of logic gates that we had to solve for x=30478191278
- We had 36 inputs and 12 outputs so first for logic gates we need a binary input
- Converting x from decimal to binary we get 11100011000101001000100101010101110 with each byte being input at one gate
- On [solving the gates](https://drive.proton.me/urls/5HB94EYRY4#ZyAz7cooDxWG) we get 100010011000

## Flag:

```
nite{100010011000}
```

## Concepts learnt:

- Learnt the concepts of AND, OR, NOR and XOR gates


***


# 2. I like Logic

> i like logic and i like files, apparently, they have something in common, what should my next step be.

## Solution:

- The challenge gave us a .sal file and I first extracted it to see if its possible and I got .bin files inside and it looked like logic gates again
- Upon searching the internet I found that .sal files can be opened on [Logic 2](https://www.saleae.com/pages/downloads)
- It added the contents of the file to Channel 3
- The resource mentioned to use a async seriel for analyzing it and I continued with the default bitrate of 9600 to get hex values
- On reading the values in terminal view and scrolling down we get to see the final flag

## Flag:

```
FCSC{b1dee4eeadf6c4e60aeb142b0b486344e64b12b40d1046de95c89ba5e23a9925}
```

## Concepts learnt:

- We can analyze and debug .sal files using Logic 2

## Notes:

- Firstly I had opened it in HxD to see what kind of file it is
- Also tried running foremost to find anything but they were dead ends

## Resources:

- Used the writeup of a [HTB challenge](https://medium.com/@rahulhoysala07/hack-the-box-hardware-challenge-debug-writeup-3889089897ef) for this 

***


# 3. Bare Metal Alchemist

> my friend recommended me this anime but i think i've heard a wrong name.

## Solution:

- On searching on Google, I found that .elf files are also a binary file so I tried running it but it wouldnt run
- On seeing the file info 
- The challenge name was "Bare Metal" and the anime it was referring to was "Full Metal Alchemists"
- Ran the file command to see its architecture and it was `firmware.elf: ELF 32-bit LSB executable, Atmel AVR 8-bit, version 1 (SYSV), statically linked, with debug_info, not stripped`
- On searching online I found that the file is for microcontrollers and mainly the Arduino UNO
- Tried running it via simavr or arduino uno but it was a dead ends
- I tried opening the file on https://filext.com/online-file-viewer.html to get the contents inside and it had
```
.bss
.comment
.data
.debug_abbrev
.debug_aranges
.debug_info
.debug_line
.debug_str
.note.gnu.avr.deviceinfo
.shstrtab
.strtab
.symtab
.text
NULL
```
- Searching about the files online I see that AVR stores constants and strings in .text so my next step is to inspect that
- Doing strings .text give nothing and I move to seeing its hexdump using xxd
```
00000060: 0c94 6800 0c94 6800 f1e3 e6e6 f1e3 def1  ..h...h.........
00000070: cd94 d6fa 94d6 fad6 cac8 96fa d694 c8d5  ................
00000080: c996 fa91 d7c1 d094 cbca fac3 94d7 c8d2  ................
```
- Searching online about the hexdump, I see that `0c94` is a realtive jump or RJMP and it is used to jump to different parts of the code
- The hexdump from `f1e3` to `c8d2` likely represented data
```
f1 e3 e6 e6 f1 e3 de f1 cd 94 d6 fa 94 d6 fa d6 ca c8 96 fa d6 94 c8 d5 c9 96 fa 91 d7 c1 d0 94 cb ca fa c3 94 d7 c8 d2 91 d7 c0 d8
```
- On cyberchef running XOR bruteforce on it we get the final flag on the key A5

```bash
readelf -h firmware.elf
readelf -h /usr/bin/cat
```

## Flag:

```
TFCCTF{Th1s_1s_som3_s1mpl3_4rdu1no_f1rmw4re}
```

## Notes:

- Initially seeing a binary file I tried opening it in Ghidra and analyzing it, running DWARF on it but they were dead ends
- Also ran strings on the .elf file but it was not helpful
- I had also tried Arduino IDE and running the file through that but it was not possible as Arduino only took .ino files mainly and it was only possible to export compiled binary files as .elf from the IDE and not read them
- I then tried simavr on WSL to run the .elf file but it also didnt run it properly
- Next I checked the file for corruption and compared it to the cat binary file present in /usr/bin/cat using readelf
- I tried modifying the bytes of the firmware file to match the other file and then run it but again it didnt run