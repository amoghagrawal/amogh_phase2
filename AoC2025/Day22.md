# Day 22: C2 Detection - Command & Carol

> The TBFC is very wary since the last series of attacks by the underlings of King Malhare. They are on full alert for anything happening. But they are getting restless; it is too quiet. Sir Elfo of the TBFC takes the initiative and proposes to hunt for Command and Control traffic using the meticulously collected network traffic.

## Solution

- RITA or Real Intelligence Threat Analytics is used to detect Command & Control (C2) communication
- C2 communication is used to communicated with compromised devices remotely
- RITA only accepts Zeek logs
- We need to convert the pcap file to zeek using `zeek readpcap pcaps/rita_challenge.pcap zeek_logs/rita_challenge`
- We can import the zeek logs into rita using `rita import --logs ~/zeek_logs/rita_challenge/ --database rita_challenge`
- We can view using `rita view rita_challenge`
- We can see 6 hosts communicating with malhare.net
- The highest connections to rabbithole.malhare.net is 40
- We run the search command by using `/` and running the search command `dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc`
- We can see that the source `10.0.0.13` is communicating on the port `80`

## Objectives

### How many hosts are communicating with malhare.net?
> 6

### Which Threat Modifier tells us the number of hosts communicating to a certain destination?
> prevalence

### What is the highest number of connections to rabbithole.malhare.net?
> 40

### Which search filter would you use to search for all entries that communicate to rabbithole.malhare.net with a beacon score greater than 70% and sorted by connection duration (descending)?
> dst:rabbithole.malhare.net beacon:>=70 sort:duration-desc

### Which port did the host 10.0.0.13 use to connect to rabbithole.malhare.net?
> 80

## Concepts learnt:

- Convert a PCAP to Zeek logs
- Use RITA to analyze Zeek logs and analyze the output of RITA