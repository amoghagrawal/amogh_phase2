# Day 4: AI in Security - old sAInt nick

> The lights glimmer and servers hum blissfully at The Best Festival Company (TBFC), melting the snow surrounding the data centre. TBFC has continued its pursuit of AI excellence. After the past two years, they realise that Van Chatty, their in-house chatbot, wasn’t quite meeting their standards. <br>
> Unfortunately for the elves at TBFC, they are also not immune to performance metrics. The elves aim to find ways of increasing their velocity; something to manage the tedious, distracting tasks, which allows the elves to do the real magic. 

## Solution

- The challenge had 3 objectives:
1. Red: Generate and use an exploit script.
2. Blue: Analyse web logs of an attack that has occurred.
3. Software: Analyse source code for vulnerabilities.
- The first stage was SQL injection in which we used the script given by the AI to get the flag for the second question which was `THM{SQLI_EXPLOIT}`
- After following all three stages we get the first flag - `THM{AI_MANIA}`
- The second stage was analyzing the log details which we got from SQL injection
```
- IP Address: 198.51.100.22 (a user\u2019s IP)
- Time: 3 October 2025 at 09:03
- URL: /login.php (a vulnerable login endpoint)
- Username: alice
- SQL Injection: The password parameter contains "alice%27+OR+1%3D1+--+-&password=test
```
- The third stage was about the `??` operator which can be used to get POST variables 

## Objectives

### Complete the AI showcase by progressing through all of the stages. What is the flag presented to you?
> THM{AI_MANIA}

### Execute the exploit provided by the red team agent against the vulnerable web application hosted at MACHINE_IP:5000. What flag is provided in the script's output after it?
> THM{SQLI_EXPLOIT}

## Concepts learnt:

- How AI can be used as an assistant in cyber security