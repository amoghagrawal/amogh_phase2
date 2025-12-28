# Day 20: Race Conditions - Toy to The World

> The Best Festival Company (TBFC) has launched its limited-edition SleighToy, with only ten pieces available at midnight. Within seconds, thousands rushed to buy one, but something strange happened. More than ten lucky customers received confirmation emails stating that their orders were successful. Confusion spread fast. How could everyone have bought the "last" toy? McSkidy was called in to investigate.  

## Solution

- The challenge requires the use of BurpSuite and mainly the Proxy and Repeater tabs
- We add both the sleigh toy to our cart and process the payment and pay for it
- In BurpSuite, in Proxy, under HTTP history we will see a HTTP request for `/process_checkout`
- We send the request to the repeater
- We add the repeat requests to a new tab group
- We will duplicate the tab and then select `Send group in parallel (last-byte sync)` and then `Send group (parallel)` which will cause the timing bug to appear
- We get the first flag as `THM{WINNER_OF_R@CE007}`
- Repeating the same steps for the second item, we get the flag as `THM{WINNER_OF_Bunny_R@ce}`

## Objectives

### What is the flag value once the stocks are negative for **SleighToy Limited Edition**?
> THM{WINNER_OF_R@CE007}

### Repeat the same steps as were done for ordering the SleighToy Limited Edition. What is the flag value once the stocks are negative for **Bunny Plush (Blue)**?
> THM{WINNER_OF_Bunny_R@ce}

## Concepts learnt:

- Understand what race conditions are and how they can affect web applications.
- Learn how to identify and exploit race conditions in web requests.