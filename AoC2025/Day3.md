# Day 3: Splunk Basics - Did you SIEM?

> It’s almost Christmas in Wareville, and the team of The Best Festival Company (TBFC) is busy preparing for the big celebration. Everything is running smoothly until the SOC dashboard flashes red. A ransom message suddenly appears: 
<br>
<img height=250px src="https://tryhackme-images.s3.amazonaws.com/user-uploads/62a7685ca6e7ce005d3f3afe/room-content/62a7685ca6e7ce005d3f3afe-1763099571417.png">

## Solution

- On Splunk we chose the option of Search and Reporting and in the search bar type `index=main` to see all the ingested logs
- We notice two source types - `web_traffic` and `firewall_logs`
- The first four questions concern the source `web_traffic` 
- The first question mentions the attacker IP so by looking at the top IP in `client_ip` we see `198.51.100.55` as the IP with most events
- By filtering the events to just that IP using `index="main" sourcetype=web_traffic client_ip="198.51.100.55"` we see the most events happened on 12th Oct and it was 116 events
- We can see the Havij useragent was used a total of 993 times which is the third answer
- By looking at the `path` column we see that the attacker IP tried downloading the files from the server for  658 times using - `/download?file=etc/passwd`
- The last question wants to see how many bytes were transferred to the C2 server from the attacker IP and the hint mentions using the sum command
- We can get the total number of bytes by using the following command the count comes out to 126167
```
index=main sourcetype=firewall_logs dest_ip="198.51.100.55" reason=C2_CONTACT | stats sum(bytes_transferred)
```

## Objectives

### What is the attacker IP found attacking and compromising the web server?
> 198.51.100.55

### Which day was the peak traffic in the logs? (Format: YYYY-MM-DD)
> 2025-10-12

### What is the count of Havij user_agent events found in the logs?
> 993

### How many path traversal attempts to access sensitive files on the server were observed?
> 658

### Examine the firewall logs. How many bytes were transferred to the C2 server IP from the compromised web server?
> 126167

## Concepts learnt:

- How to interpret custom log data in Splunk
- Use SPL to filter search results and recover useful information