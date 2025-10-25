# 1. Trivial Flag Transfer Protocol

> Figure out how they moved the [flag](https://mercury.picoctf.net/static/ed308d382ae6bcc37a5ebc701a1cc4f4/tftp.pcapng).

## Solution:

- Seeing a pcap file I first opened it on the Wireshark and tried seeing through the data packets for some clues
- Saw `picture1.bmp`, `instructions.txt` and `program.deb` being read in one of the data packets
- Googled how to extract files within a pcap file and tried exporting packet bytes but it failed because I was on the latest version of Wireshark
- Reverting to Wireshark 4.4.2 but the export option was now disabled
- Upon googling, I got that TFTP packets are treated differently and you need to go to File and then **Export Objects**
- I got [6 files](https://drive.proton.me/urls/DFEXVJ8KMG#0c38aJ4mRMlA) from exporting, 3 were .bmp, 1 was a .txt, 1 was called plan and the other was a .deb
- Googled to know that .deb can be extracted using 7zip so thats what i did
- Inside the program.deb was a file called `steghide` which is also a tool used to hide info inside the images so I figured that it must have been used
- The text in both instructions.txt and plan looked like to be cipher
- I tried various ciphers including the most common ones on instructions.txt like Caeser, Vignere and ROT13 until getting some progress with ROT13
- The instructions mentioned "figure out a way to hide the flag" to our guess of using steghide was correct
- Now running the plan file through ROT13 gives us
> IUSEDTHEPROGRAMANDHIDITWITH-DUEDILIGENCE.CHECKOUTTHEPHOTOS
- Now to figure out the passphrase, I first tried steghide on the first picture with a blank password but it failed
- I tried combinations of words like TFTP, BMP, PICOCTF but none were the password
- I ultimately noticed the decoded text from the plan to see DUEDILIGENCE written seperately and decided to try it on picture1 but it was again not the password
- I tried everything on picture2 but no result and ultimately got the flag on picture3.bmp

```
steghide extract -sf picture3.bmp
```

## Flag:

```
picoCTF{h1dd3n_1n_pLa1n_51GHT_18375919}
```

## Concepts learnt:

- Wireshark is used to analyze the packets sent or recieved over the network. Here packets were being read from some source and we can view and export those packet data.
- TFTP is like less secure version of HTTP and used for simpler tasks. It stands for Trivial Flag Transfer Protocol

## Notes:

- After I had got the images from the .pcap file I tried running strings, binwalk and even seeing them through stegsolve for any hidden msgs inside the pictures

## Resources:

- Referred to this reddit thread to learn how to extract objects from the pcap file [https://www.reddit.com/r/wireshark/comments/6ndvpq/extract_tftp_file_from_pcapng/](https://www.reddit.com/r/wireshark/comments/6ndvpq/extract_tftp_file_from_pcapng/)


***


# 2. tunn3l v1s10n

> We found this [file](https://mercury.picoctf.net/static/06a5e4ab22ba52cd66a038d51a6cc07b/tunn3l_v1s10n). Recover the flag.

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