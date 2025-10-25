# 1. Challenge name

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