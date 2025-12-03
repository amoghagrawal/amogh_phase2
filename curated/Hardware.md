# 1. I Like Logic More

> idk man, i feel like microsd cards are a thing of the past.
> chal file: https://drive.google.com/file/d/1lkgUiHkKmAOdb93pWmi4zYtQSFFw1jm9/view?usp=drive_link

## Solution:

- The challenge provides us a .sal file which upon opening in Logic 2 shows 4 channels
- The description mentions it has something to do with MicroSD cards and upon googling, I see that microsd cards communicate using SPI or Seriel Peripheral Interface
- Using a SPI analyzer, we have options to set MOSI, MISO, Clock and Enable
- We set the highest frequency channel to the clock that is Channel 3
- We now set Channel 1 to MISO (Master In, Slave Out) and Channel 0 to MOSI (Master Out, Slave In)
- Exporting the output table as a csv to decode
- I input the entire MISO column into cyberchef and convert it from hex but I got nothing
- I then put MOSI into cyberchef to get the final flag

## Flag:

```
HTB{unp2073c73d_532141_p2070c015_0n_53cu23_d3v1c35}
```

## Concepts learnt:

- SPI is a synchronous two way communication method which allows both reading and writing
- MOSI is the data sent to SD card and MISO is the data recieved back

## Incorrect Tangents

- Initially while inputting the channels into SPI, I was using Channel 2 as the clock and I wasnt getting anything meaningful
- I also played with which channel among 0 and 1 were MOSI or MISO

## Resources:

- https://rainbowpigeon.me/posts/csaw-2021/


***

# 3. Formwear

> this is most definitely going to ring some bells for those who attended the "router hijacking" workshop L0L
> chal file: https://drive.google.com/file/d/122PHIkxLtJ9RP7wiSq7X1v-jAZYGNcXB/view?usp=drive_link

## Solution:

- The challenge provides us a .zip extracting which we find 3 files - fwu_ver, hw_ver and rootfs referring to hardware ver X1 and firmware ver 3.0.5
- The description mentions router hijacking as the challenge type
- A rootfs file is generally the top level of a Linux file hierarchy
- On using binwalk on the rootfs file we see that it is a `SquashFS` file system
- The file can be analyzed using `unsquashfs`
- First we extract the rootfs file using `unsquashfs rootfs`
- Inside the extracted directory I start opening the folders and looking for hints
- By looking at the directories, we can confirm its a linux file system
- In `home/.41fr3d0` there is a file named `s.txt` having the text `almost there`
- Almost all the directories except lib, bin and dev were all empty
- I decided to search for the flag using grep using `grep -r “{“`
- Inside the `etc` folder, I found the final flag using grep in config_default.xml
```
config_default.xml:<Value Name="SUSER_PASSWORD" Value="HTB{N0w_Y0u_C4n_L0g1n}"/>
```

## Flag:

```
HTB{N0w_Y0u_C4n_L0g1n}
```

## Concepts learnt:

- Router/IOT firmware is packaged into a SquashFS filesystem and got an idea of a typical router structure

## Resources:

- https://kavigihan.medium.com/iot-hacking-reversing-a-router-firmware-df6e06cc0dc9


***