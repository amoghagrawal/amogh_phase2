# 1. Web Gauntlet

> Can you beat the filters? Log in as admin http://shape-facility.picoctf.net:63661/ http://shape-facility.picoctf.net:63661/filter.php

## Solution:

- We had to login as admin on the website by doing sql injection but not using the banned words prresent on the filter website
- Reading a sql injection resource I found out we can comment the rest of the code and using that concept I passed the filters
- For Round 1 since or was blocked I used `admin’ --`
- For Round 2 they blocked `--` so I used `; #` to end the command and then comment the rest of it. The command was `admin';#`
- In Round 3 also `admin';#` worked
- For Round 4 since admin was now blocked I first tried concactination of the words ad, min or the character seperately but it was not working
- Then I tried `ad'||'min';` which worked
- For Round 5 again the same command `ad'||'min';` worked

## Flag:

```
picoCTF{y0u_m4d3_1t_79a0ddc6}
```

## Concepts learnt:

- In such challenges we can stop the execution of the second half of the command by commenting them out using -- or ;#

## Notes:

- At first I tried solving the challenge using the banned/filter words only and on challenge 1 I tried the commands
```
' or '1'='1
hello' or '1' = '1
```

## Resources:

- https://www.invicti.com/blog/web-security/sql-injection-cheat-sheet/

***


# 2. SSTI1

> Get the website http://rescued-float.picoctf.net:56607/ to announce the flag

## Solution:

- The hint mentioned server side template injection so I first looked that up
- I tried `{{1+1}}` to see if its vulnerable and it was
- Next was to use the input to get the flag
- Using the resource I found I tried the command `{{request['application']['__globals__']['__builtins__']['__import__']('os')['popen']('id')['read']()}}` to get `uid=0(root) gid=0(root) groups=0(root)`
- On seeing the command we injected and the output, we see that its the **id** command in linux which is being executed
- On replacing `id` with `ls` we can see the list of files inside and we have a flag file
- Using cat to open the flag file and retrieve the flag

```
put codes & terminal outputs here using triple backticks

you may also use ```python for python codes for example
```

## Flag:

```
picoCTF{s4rv3r_s1d3_t3mp14t3_1nj3ct10n5_4r3_c001_bcf73b04}
```

## Concepts learnt:

- SSTI is used when the website needs to render some input from the user as a template like here it was the announce

## Notes:

- I first tried a random announcement to see what was the method to see whether it was using a GET method or not
- I also tried `<script>alert(1)</script>` but didnt get anything 

## Resources:

- https://onsecurity.io/article/server-side-template-injection-with-jinja2/


***


# 3. Cookies

> Find out the best cookie on http://mercury.picoctf.net:6418/

## Solution:

- The challenge mentioned cookies so I first opened the developer console and looked through the cookies to find one with NAME as name and VALUE as -1
- I tried putting -1 in the input to search but I got nothing
- Then I put `snickerdoodle` which was the sample text to search and saw the cookie change from -1 to 1
- Upon manually incrementing the cookies, I could see the name of the biscuit changing
- On setting a high value it would give an error
- I manually started increasing them one by one until I got to the flag
- The flag was hidden in the value 18

## Flag:

```
picoCTF{3v3ry1_l0v3s_c00k135_88acab36}
```