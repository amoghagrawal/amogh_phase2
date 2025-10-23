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


# 3. m00nwalk

> Decode this message from the moon.

## Solution:

- Listening to the audio file the beeps resembled a SSTV signal and the hint confirmed the same
- The challenge provides us with an audio file which resembles a SSTV signal used to decode and encode messages sent to space
- Using YONIQ to decode the image with the VB-Cable virtual audio device we get the image directly
- Using Hint 2 to find the CMU mascot to be **Scottie** we use that in RX to get [moonwalk.jpg](moonwalk.jpg)
- The image gives us `CTF{beep_boop_im_in_space}` amd following the standard flag practice we get the full flag which is `picoCTF{beep_boop_im_in_space}`

## Flag:

```
picoCTF{beep_boop_im_in_space}
```

## Concepts learnt:

- The challenge was about audio decoding where the analog signals where made into digital ones using slow scan televsion technology or SSTV

## Notes:

- I had solved a similar question prior in another CTF challenge with the same approach
- My first approach was to open the .wav file in Sonic Visualizer and look at the spectogram for any clues but there was nothing
- I tried decoding the beeps as morse code but got nowhere
- Using Hint 1, I got the beeps as SSTV
- To get the image I tried CW Skimmer and played the audio on speaker but it couldnt record it to decode the audio then I installed MMSSTV/YONIQ following a youtube tutorial

## Resources:

- Watched this short video on how to operate MMSSTV: [How To - SSTV by GM6DX](https://youtu.be/bbHFw6SF_PA)
- Took help from Chatgpt to figure out how to use a virtual audio cable along with MMSSTV to get the image