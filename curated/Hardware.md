# 1. I Like Logic More

> idk man, i feel like microsd cards are a thing of the past. <br>
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


# 2. Red Devil

> this is the worst football team ever(i dont even watch football lmeow) <br>
> chal file: https://drive.google.com/file/d/1bsUDpXxN6M-P-x85OFNYuSGdeifb--sI/view?usp=drive_link

## Solution:

- The challenge file is a .cf32 file is a raw data file using in Software-Defined Radio (SDR)
- Opening the file in Inspectrum, we can see a spectogram of the data file
- The file is Manchester encoding as the description also suggests a football related chal
- Adding a amplitude plot and then a threshold plot we can see square waves of different widths
- Initially the cursors were not properly aligned and got `����NHTB{RF_H4ck1n6_1s����`
- Changing the samples to 900 and extracting the symbols to stdout we get the [output bits](https://drive.proton.me/urls/KZ2J2MBK1W#7YF0wGrAW2li)
- In a Manchester decode, a pair of (0,1) becomes 0 and (1,0) becomes 1
- Using a python script we get the final decoded sequence which is like `1010101.......0010111110`

```py
file = open("C:/users/amogh/downloads/thresholdvalues.txt", "r")
data = file.read()

for i in range(0, len(data)-1, 2):
    if data[i] == '0' and data[i+1] == '1':
        print(0, end="")
    elif data[i] == '1' and data[i+1] == '0':
        print(1, end="")
```

- Converting the output from binary we get the final output `ªªªªNHTB{RF_H4ck1n6_1s_c00l!!!>` because the last 7 bits are `0111110` and when 1 is added to the end to make it `01111101` we get the final flag - `NHTB{RF_H4ck1n6_1s_c00l!!!}`

## Flag:

```
NHTB{RF_H4ck1n6_1s_c00l!!!}
```

## Concepts learnt:

- A `.cf32` file is a complex float 32 bit file
- Inspectrum is a tool for analyzing captured signals and viewing spectrograms

## Altnerative Solutions

- The chal could also be solved using RTL 433 using the command `rtl_433 signal.cf32 -A`
- Opening the file in Universal Radio Hacker (URH), the file was Amplitude Shift Key with samples 900
- For 1 bit, they graph had a frequency but for 0 it was swithced off and then using Manchester II to decode it to get the final flag

## Incorrect Tangents

- I also tried opening the file as raw data in Audacity but it was not helpful

## Resources:

- https://github.com/miek/inspectrum
- https://www.rtl-sdr.com/inspectrum-a-new-tool-for-analyzing-captured-signals/


***


# 3. Formwear

> this is most definitely going to ring some bells for those who attended the "router hijacking" workshop L0L <br>
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


# 4. Speed Thrills But Kills

> i recently got involved in a hit and run case in pune, that kids porsche was going wayy too fast, if only i knew what the VIN of the car was :( <br>
> chal file: https://drive.google.com/file/d/13Q0Sd938buuzDHJ8p8Pea7OLOqRmVoR3/view?usp=drive_link

## Solution:

- Since its a `.sal` file the first step was to open it in Logic 2
- The chal desc mentioned a car accident I decided to check LIN and CAN analyzers in Logic
- The salae file had 2 digital channels and 2 analog channels which were mirrored
- By setting the CAN Input to `Channel 0` and the initialy bitrate to `500000` I got nothing useful
- I then set the bitrate to `125000` and got no output at all
- By switching INVERTED to OFF and at `125000` bitrate, valid packets appeared
- I got [output hex data](https://drive.proton.me/urls/GW8KVNMYDC#lUWruIl1j1i1) which I decoded from hex in cyberchef to get the final flag

## Flag:

```
HTB{v1n_c42_h4ck1n9_15_1337!*0^}
```

## Concepts learnt:

- CAN bus is central communication device in vehicles
- The blackbox or EDR stores data from CAN when an accident/event occurs
- LIN bus is used for low speed communication of non safety components like mirrors, climate control etc

## Incorrect Tangents

- I had first tried CAN and LIN anlyzers at different BIT rates but both of them didnt work
- I also tried ASYNC analyzers at different baud rates to find something useful but that also didnt work
- Initially I had set the Inverted as ON in the CAN analyzer setting which prevented in the correct output data


***


# 5. Gates of Mayhem

> iqtest but its on steriods and you have weird aah inputs aswell. <br>
> chal file: https://drive.google.com/file/d/1JE2XLNjjtQtZ54O7JIZ8ZTNy_7GMm9-C/view?usp=drive_link <br>
> input sequence: https://drive.google.com/file/d/1TioFPmf4ik_M9ZpKasOjjlCKEWSC6YIF/view?usp=drive_link

## Solution:

- The challenge provided us with a Kicad diagram of a series of transistors and a input sequence of 1s and 0s
- Transistors in series act as AND gates (&) and transistors in parallel behave as OR gate (|)
- A single transistor acts as a NOT gate
- Redrawing the schematic using basic gates as in attatched image: <br>
<img src="" height=500px> <br>
- The final equation is `((IN1 & IN2) ⊕ ((IN3 & IN4) & (IN5 | IN6)))`
- Writing a python code to decode the final equation with the input sequence to get the final binary sequence

```py
import csv
file = open("C:/Users/amogh/Downloads/input_sequence.csv", "r")
reader = csv.reader(file)
next(reader)

output = []
for  i in reader:
    IN1 = int(i[0])
    IN2 = int(i[1])
    IN3 = int(i[2])
    IN4 = int(i[3])
    IN5 = int(i[4])
    IN6 = int(i[5])
    final = ((IN1 & IN2) ^ ((IN3 & IN4) & (IN5 | IN6)))
    output.append(final)

print(output)
file.close()
```

- Converting the final binary sequence to ASCII in cyberchef we get the flag as `citadel{1_l0v3_t0_3xpl01t_l0g1c}`

## Flag:

```
citadel{1_l0v3_t0_3xpl01t_l0g1c}
```

## Incorrect Tangents

- Initially I tried to recreate the schematic on Kicad and export it and use LTspice to calculate the flag but that didnt work
- When manually translating the transistors to gates, I didnt calculate the output properly and got the equation as `((IN1 & IN2) | ((IN3 & IN4) & (IN5 | IN6)))`

## Resources:

- https://www.101computing.net/creating-logic-gates-using-transistors/