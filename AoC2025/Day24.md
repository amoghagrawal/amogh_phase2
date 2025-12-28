# Day 24: Exploitation with cURL - Hoperation Eggsploit

> According to blue-team intel, the wormhole is held open by a control panel on the Evil Bunnies' web server. The team must shut it down first to cut off reinforcements before facing King Malhare. <br>
> However, the terminal they have is bare. No Burp Suite, no browser, just a command prompt. <br>
> But that's fine. The team will use the command line and cURL to speak HTTP directly: send requests, read responses, and find the endpoints that shut the portal.

## Solution

- By running `curl -X POST -d "username=admin&password=admin" https://10.48.162.117/post.php` we get the first flag: `THM{curl_post_success}`
- We run `curl -c cookies.txt -d "username=admin&password=admin" https://10.48.162.117/cookie.php` to login and save the cookie
- We then reuse the cookie using `curl -b cookies.txt https://10.48.162.117/cookie.php` to get the flag as `THM{session_cookie_master}`
- We create a text file containing possible passwords to bruteforce and then create a script to automatically try them by sending the login request using `curl -s` and checking the response using `grep -q`
- On running the loop file we get the password as `secretpass`
- To make a request using an agent we will run the command `curl -A "TBFC" https://10.48.162.117` to get the flag: `THM{user_agent_filter_bypassed}`

## Objectives

### Make a POST request to the /post.php endpoint with the username admin and the password admin. What is the flag you receive?
> THM{curl_post_success}

### Make a request to the /cookie.php endpoint with the username admin and the password admin and save the cookie. Reuse that saved cookie at the same endpoint. What is the flag your receive?
> THM{session_cookie_master}

### After doing the brute force on the /bruteforce.php endpoint, what is the password of the admin user?
> secretpass

### Make a request to the /agent.php endpoint with the user-agent TBFC. What is the flag your receive?
> THM{user_agent_filter_bypassed}

## Concepts learnt:

- Understand what HTTP requests and responses are at a high level.
- Use cURL to make basic requests (using GET) and view raw responses in the terminal.
- Send POST requests with cURL to submit data to endpoints.
