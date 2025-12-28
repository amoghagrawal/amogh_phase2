# Day 17: CyberChef - Hoperation Save McSkidy

> McSkidy is imprisoned in King Malhare's Quantum Warren. Sir BreachBlocker III was put in charge of securing the fortress and implemented several access controls to prevent any escape. <br>
> However, McSkidy managed to send vital clues to his team using harmless bunny pictures. One message revealed that five locks needed to be disabled to secure an escape route. The locks can be broken by examining their logic and leveraging the system's built-in chat for the guards. 

## Solution

### Task 3 (Outer Gate)

- The challenge is divided in 5 levels
- For the first level we see a base64 msg ` QWxsIGhhaWwgS2luZyBNYWxoYXJlIQ==` decoded to `All hail King Malhare!`
- We need to find the username and pass to enter the gates
- In the debugger in app.ks we see the logics for al levels
- The username is the base64 of the guards from the chatbox
- The chatbox mentions to send only base64 so we convert the XMagic ques to base64 and send that to get another base64
- The base64 says `Here is the password: SWFtc29mbHVmZnk=` which is another base64 and decoding that we get the password `Iamsofluffy`
- The username `CottonTail` is `Q290dG9uVGFpbA==` in base64

### Task 4 (Outer Wall)

- The username is `CarroltHelm` which gives `Q2Fycm90SGVsbQ==` in base64
- The magic question returns a base64 string which again gives a base64 string which is `U1hSdmJHUjViM1YwYjJOb1lXNW5aV2wwSVE9PQ==` decoded to `SXRvbGR5b3V0b2NoYW5nZWl0IQ==` which gives `Itoldyoutochangeit!`

### Task 5 (Guard House)

- The third level requires XOR along with base64
- The username is `LongEars` encoded to Base64 to `TG9uZ0VhcnM=`
- The networks tab mentions a recipe key as `cyberchef`
- In app.js, it mentions `From Base64 => XOR(key=recipeKey)`
- To get the base64 password, the challenge mentions to simply ask the guard with a simple `Password please.`
- By sending that, the guard returns a base64 string which is decoded to `IQwFFjAWBgsf` and running it through Base64 decoder and XOR in the mentioned order we get `BugsBunny` which is the password

### Task 6 (Inner Castle)

- The guard is named `Lenny` and we get the username as `TGVubnk=`
- The same `Password please.` in Base64 gets us the response from the guard
- The app.js mentions using CrackStation and the use of MD5 hash
- From the guard we get the hash `b4c0be7d7e97ab74c13091b76825cf39`
- Putting the hash on crackstation, we get the result as `passw0rd1`

### Task 7 (Prison Tower)

- For the final level, the recipe ID is R3 and the key is `cyberchef`
- The recipe in app.js mentions `ROT13 => From Base64 => XOR(key=recipeKey)`
- The username is `Carl` which in Base64 is `Q2FybA==`
- Again the `password please.` string in Base64 works to give us the reply from the guard which gives us `IxtDWjODKNLBVEIFOuyDTt==` when decoded from base64
- Following the recipe from R3 in the same order we get the password as `51rBr34chBl0ck3r`

## Objectives

### What is the password for the first lock?
> Iamsofluffy

### What is the password for the second lock?
> Itoldyoutochangeit!

### What is the password for the third lock?
> BugsBunny

### What is the password for the fourth lock?
> passw0rd1

### What is the password for the fifth lock?
> 51rBr34chBl0ck3r

### What is the retrieved flag?
> THM{M3D13V4L_D3C0D3R_4D3P7}

## Concepts learnt:

- Introduction to encoding/decoding
- Learn how to use CyberChef
- Identify useful information in web applications through HTTP headers