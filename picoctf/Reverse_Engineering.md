# 1. GDB baby step 1

> Figure out what is in the eax register at the end of the main function. Disessemble [this](https://artifacts.picoctf.net/c/512/debugger0_a)

## Solution:

- The challenge provides us with an assembly file and mentions to find what is in the eax function which is part of the main function
- The hint tells us to use gdb which I install on wsl and use it for analyzing the file
- Using the resource I found online, I tried running the program using gdb but it didnt give any output, looking at breakpoints, stepping theough the code using stepi but no progress
- I tried looking at the strings but it was also not helpful
- Then tried the disassemble command to get ``0x0000000000001138 <+15>:    mov    $0x86342,%eax``
- Now we know from the question that we were supposed to get a hex output which we have to convert to decimal
- I converted both 0x0000000000001138 and 0x86342 to decimal to get 4408 and 549698
- Running these numbers as flags and got 549698 as the correct value

```
gdb debugger0_a
(gdb) disassemble main
```

## Flag:

```
picoctf{549698}
```

## Concepts learnt:

- Upon disassembling the file, the first column is the memory address while second column was the offset from the start and 3rd column is what the function does and here it was move the first value into the second

## Notes:

- Running strings on the file resulted in nothing useful
- Tried using IDA for it but I was unable to inspect the main function simply and used the hint's recommendation to use gdb here to get the flag

## Resources:

- [https://ctf101.org/reverse-engineering/what-is-gdb/](https://ctf101.org/reverse-engineering/what-is-gdb/)
- [https://users.umiacs.umd.edu/~tudor/courses/ENEE757/Fall15/misc/gdb_tutorial.html](https://users.umiacs.umd.edu/~tudor/courses/ENEE757/Fall15/misc/gdb_tutorial.html)
- Hex to Decimal: [https://www.rapidtables.com/convert/number/hex-to-decimal.html](https://www.rapidtables.com/convert/number/hex-to-decimal.html)

***


# 2. Challenge name

> Put in the challenge's description here

## Solution:

- Include as many steps as you can with your thought process
- You **must** include images such as screenshots wherever relevant.

```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{}
```

## Concepts learnt:

- Include the new topics you've come across and explain them in brief
- 

## Notes:

- Include any alternate tangents you went on while solving the challenge, including mistakes & other solutions you found.
- 

## Resources:

- Include the resources you've referred to with links. [example hyperlink](https://google.com)


***


# 3. vault-door-3

> This vault uses for-loops and byte arrays. The source code for this vault is here [VaultDoor3.java](https://jupiter.challenges.picoctf.org/static/943ea40e3f54fca6d2145fa7aadc5e09/VaultDoor3.java)

## Solution:

- The challenge prtovided us with a java file to decode'
- Opening it in IDA was no luck since it opened as a binary and strings was not useful as well
- The hint mentioned making a table for each value and its corresponding buffer index
- Opening the file and running it required a passcode which we needed to figure out
- The code mentioned for the passcode to be 32 characters long which was exactly the length of a string being returned at the bottom of the code `jU5t_a_sna_3lpm18g947_u_4_m9r54f`
- A function which was checking the password would not work for strings less than 32 and give an error
- The above mentioned string also looked like a jumbled flag and we had to restronct it properly using the for loop present
- The function start at i=0 and ended at i=31
- For the first 8 characters from i=0 to i=7 we directly used the same index value from the give string i.e. **jU5t_a_s**
- For the next 8 characters till i=15, we used "23-i" which gave us **1mpl3_an**
- For characrters less than 32 starting from 16, we had "46-i" i=16,.....30 which were the even indices
- And the last condition was for odd indices from 17 to 31 to get the final flag

## Flag:

```
picoCTF{jU5t_a_s1mpl3_an4gr4m_4_u_79958f}
```

## Notes:

- At first I tried putting the given string as the password but still access was denied
- Using commands like strings on the file also lead to no output