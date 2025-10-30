# 1. buffer overflow 0

> can you overflow the correct buffer? The program is available [here](https://artifacts.picoctf.net/c/174/vuln). You can view source [here](https://artifacts.picoctf.net/c/174/vuln.c).

## Solution:

- On launching the instance it was asking for an input and since the challenge was named buffer overflow I figured we had to override the character limit to get the flag
- On typing a 20 character string I got the flag for the challenge

## Flag:

```
picoCTF{ov3rfl0ws_ar3nt_that_bad_c5ca6248}
```

## Concepts learnt:

- Buffer overflow occurs when the program tries to write more data into a fixed memory variable. This causes the memory to overflow and potentialy corrupt the program


***


# 2. format string 0

> Can you use your knowledge of format strings to make the customers happy? <br>
> Download the binary [here](https://artifacts.picoctf.net/c_mimas/69/format-string-0). <br>
> Download the source [here](https://artifacts.picoctf.net/c_mimas/69/format-string-0.c).

## Solution:

- The challenge was about format identifiers which generally begin with %
- On launching the instance the first question wanted an option to fill the customer up but the 1st and 3rd option were not enough and were normal string inputs
- The 2nd option worked because of `%114d` which made the input string of 114 characters by adding space between Gr and _Cheese
- For the 2nd question, the option `Cla%sic_Che%s%steak` worked and we got the flag
- The option first passes to scanf where it is stored as a normal string but when it passes to printf, the string isnt processed properly because of string vulnerability giving us the flag

## Flag:

```
picoCTF{7h3_cu570m3r_15_n3v3r_SEGFAULT_dc0f36c4}
```

## Concepts learnt:

- Format identifiers are placeholders to specify the type or format of data during input or output


***


# 3. clutter-overflow

> Clutter, clutter everywhere and not a byte to use. <br>
> nc mars.picoctf.net 31890

## Solution:

- The challenge provided a .c file to explore
- It had a size variable and a goal variable with size as `256` and goal as `0xdeadbeef`
- I noticed `lc` written on the bed in the header and thought this challenge was again inputting a long long string and overflowing the buffer
- I manually tried inputting a long string but that didnt work and it showed code not equal to 0 but still not equal to deadbeef
- I then saw the usage of `gets` which confirmed that the input had to be overflowed since gets was vulnerable to buffer overflow
- The input taken by the challenge was put in a stack called `clutter` of size 256 and if it exceeded that limit it would overflow to `code`
- We wanted to overflow `0xdeadbeef` to the code variable
- By writing a small python code we can achieve the same
```py
(python2 -c "print('A'*264) + '\xef\xbe\xad\xde'") | nc mars.picoctf.net 31890
```
- We are writing A 264 times to the server because of the size of 256 and a buffer of 8 bytes because of the padding
- The hex part is also to be written in little endian format

## Flag:

```
picoCTF{c0ntr0ll3d_clutt3r_1n_my_buff3r}
```

## Concepts learnt:

- Format identifiers are placeholders to specify the type or format of data during input or output

## Notes

- I was trying to run the python script in python3 and it was not working
- I also tried different methods to send the output to the server including manually copy and pasting but it also didnt work
- Took a bit of help from ChatGPT to understand the problem and figure out the solution when python3 was not working properly for this