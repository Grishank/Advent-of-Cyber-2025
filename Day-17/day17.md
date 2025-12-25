# 🎄 Advent of Cyber 2025 — Day 17  
<img src="./images/day17-banner.png" width="900"/>

**Title:** CyberChef - Hoperation Save McSkidy  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Blue Team, Encoding/Decoding, Web Analysis  
**Room Link:** [CyberChef - Hoperation Save McSkidy](https://tryhackme.com/room/encoding-decoding-aoc2025-s1a4z7x0c3)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

McSkidy has been imprisoned in **King Malhare’s Quantum Warren**.  
To prevent any escape, **Sir BreachBlocker III** fortified the prison with multiple logical locks, each protected by different encoding and authentication mechanisms.

Before capture, McSkidy managed to send clues using **harmless bunny images**.  
These clues revealed that **five locks** must be broken to secure an escape route.

As part of the Blue Team, the task was to:
- Inspect web applications
- Decode encoded data
- Abuse weak logic
- Leverage HTTP headers and chat responses
- Break each lock step by step

---

## 🎯 Learning Objectives

- Understand **encoding vs decoding**
- Learn how to use **CyberChef**
- Identify useful information from **HTTP headers**
- Analyze **client-side login logic**
- Apply decoding techniques to real-world scenarios

---

## 🔐 Encoding and Decoding

Encoding is used to transform data to ensure **compatibility** between systems.  
It is **not meant for security**.

| Encoding | Encryption |
|--------|-----------|
| Compatibility | Security |
| No confidentiality | Confidential |
| Standardized | Algorithm + Key |
| Fast | Slower |
| Example: Base64 | Example: TLS |

**Decoding** is the process of reversing encoded data back to its original form.

---

## 🧰 CyberChef Overview

CyberChef is often referred to as the **Cyber Swiss Army Knife**.

| Area | Description |
|----|------------|
| Operations | Available transformations |
| Recipe | Chained operations |
| Input | Raw input data |
| Output | Transformed result |

---

## 🍳 CyberChef Simple Example

Steps:
1. Add **To Base64**
2. Input `IamRoot`
3. Add **From Base64**

This demonstrates **chained operations** and reversible encoding.

---

## 🔎 Inspecting Web Pages

Beyond visible content, web pages expose valuable information through:
- Developer tools
- HTTP headers
- JavaScript logic

Access developer tools:
- Chrome: More tools → Developer tools  
- Firefox: Menu → Web Developer Tools  
- Edge: Settings → Developer tools  

---

## 🧠 Key Investigation Information

- Target URL:
xxxxxxxxxxxxx

Key items to observe:
- Chat messages are **Base64 encoded**
- Guard names are reused in logic
- Headers reveal clues (Network tab)
- Debugger shows login logic
- Bunny images hide hints

---

# 🔐 Lock 1 — Outer Gate

Steps:
1. Identify the **guard name** and encode it in Base64 (username)
2. Extract the **magic question** from headers
3. Encode the magic question in Base64
4. Send it via chat
5. Decode the guard’s response
6. Inspect login logic (Base64)
7. Use encoded username + decoded password

**Password:**
Iamsofluffy

---

# 🔐 Lock 2 — Outer Wall

Steps:
1. Identify and encode guard name
2. Extract and encode magic question
3. Chat returns encoded password
4. Login logic uses **double Base64 encoding**
5. Decode twice
6. Log in

**Password:**
Itoldyoutochangeit!

---

# 🔐 Lock 3 — Guard House

Changes:
- No magic question
- Guard responses may be delayed
- Password uses **XOR + Base64**

XOR key:
cyberchef

Logic:
- XOR password with key
- Encode with Base64

To reverse:
- From Base64
- XOR with same key

**Password:**
BugsBunny

---

## 🧠 XOR Theory

XOR has a reversible property:
- Input XOR key XOR key = Input

This allows attackers (and defenders) to reverse XOR-based obfuscation.

---

# 🔐 Lock 4 — Inner Castle

Logic:
- Password is hashed using **MD5**

Steps:
1. Decode guard response
2. Identify MD5 hash
3. Use **CrackStation**
4. Retrieve plaintext
5. Log in

**Password:**
passw0rd1

---

## 🧠 MD5 Theory

- MD5 is a one-way hash
- Cannot be reversed mathematically
- Precomputed hash databases allow lookup

---

# 🔐 Lock 5 — Prison Tower

Final lock introduces **variable logic**.

Steps:
1. Identify guard name
2. Extract **Recipe ID** from headers
3. Match decoding logic
4. Build correct CyberChef recipe

### Recipe Cheat Sheet

| Recipe ID | Reverse Logic |
|---------|---------------|
| 1 | From Base64 → Reverse → ROT13 |
| 2 | From Base64 → From Hex → Reverse |
| 3 | ROT13 → From Base64 → XOR(key) |
| 4 | ROT13 → From Base64 → ROT47 |

Using the correct recipe allowed extraction of the final password.

**Password:**
51rBr34chBl0ck3r

---

## 🏁 Final Flag

THM{M3D13V4L_D3C0D3R_4D3P7}

---

## 🎯 Learning Objectives Achieved

- Mastered encoding vs decoding concepts  
- Used CyberChef for chained transformations  
- Extracted intelligence from headers & JS logic  
- Applied XOR, ROT, Base64, MD5 techniques  
- Broke multi-layer authentication logic  

---

## 📘 What I Learned Today

> “Encoding is not security — it’s just another layer waiting to be decoded.”

---

## 🔜 Next Step

Proceed to **Day 18** of Advent of Cyber 2025.


