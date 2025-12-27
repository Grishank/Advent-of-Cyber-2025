# 🎄 Advent of Cyber 2025 — Day 20  
<img src="./images/day20-banner.png" width="900"/>

**Title:** Race Conditions - Toy to The World  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Web Security, Application Security, Blue Team  
**Room Link:** [Race Conditions - Toy to The World](https://tryhackme.com/room/race-conditions-aoc2025-d7f0g3h6j9)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

The Best Festival Company (TBFC) launched a **limited-edition SleighToy**, with only **10 units available** at midnight.  
Within seconds, thousands of customers rushed to buy one.

Something went terribly wrong.

More than ten customers received **order confirmation emails**, all claiming they successfully bought the “last” SleighToy.  
By morning, TBFC faced:
- Angry customers  
- Missing inventory  
- Negative stock values  

McSkidy was called in to investigate. She quickly discovered the issue wasn’t fraud — it was a **race condition**.

Sir Carrotbane’s Bandit Bunnies exploited a timing flaw by flooding the checkout system with **simultaneous requests**, proving how dangerous a few milliseconds can be.

---

## 🎯 Learning Objectives

- Understand what **race conditions** are  
- Learn how race conditions affect web applications  
- Identify and exploit race conditions in web requests  
- Understand how concurrent requests manipulate shared resources  
- Explore mitigation techniques to prevent race condition vulnerabilities  

---

## 🧠 What is a Race Condition?

A **race condition** occurs when:
- Two or more actions happen at the same time  
- The outcome depends on the order in which they complete  

In web applications, race conditions often happen when multiple users or automated requests:
- Access shared resources (stock, balances)
- Modify data simultaneously
- Lack proper synchronisation  

This can result in:
- Oversold inventory  
- Duplicate transactions  
- Inconsistent data states  

---

## 🧩 Types of Race Conditions

### ⏱ Time-of-Check to Time-of-Use (TOCTOU)

The system checks a condition first and uses it later — but the data changes in between.

Example:
- Stock checked = 1 item left  
- Two users click “Buy” at the same time  
- Both purchases succeed  

---

### 🔁 Shared Resource Race

Multiple processes modify the same data simultaneously.

Example:
- Two checkout requests update stock at the same time  
- One update overwrites the other  

---

### ⚛ Atomicity Violation

An operation that should happen all at once is split into steps.

Example:
- Payment processed  
- Stock update delayed  
- Another request slips in between  

---

## 🛠️ Configuring the Environment

### Step 1: Route Traffic Through Burp Suite

On the AttackBox:
1. Open **Firefox**
2. Click **FoxyProxy**
3. Select the **Burp profile**

This ensures all traffic flows through Burp Suite.

---

### Step 2: Launch Burp Suite

1. Click the **Burp Suite** icon on the desktop  
2. Select **Temporary project in memory**  
3. Click **Next**
4. Click **Start Burp**

---

### Step 3: Disable Intercept

In Burp Suite:
- Go to **Proxy → Intercept**
- Ensure it says:
Intercept is off

This allows requests to pass normally.

---

## 🧪 Making a Legitimate Purchase

1. Visit:
http://MACHINE_IP

2. Log in using:
Username: atxxxxxxxx
Password: atxxxxxxxx

3. On the dashboard, locate **SleighToy Limited Edition (10 units)**

4. Click **Add to Cart**
5. Click **Checkout**
6. Click **Confirm & Pay**

You should see a **successful order confirmation**.

---

## 🧨 Exploiting the Race Condition

### Step 1: Capture the Checkout Request

1. Open **Burp Suite**
2. Go to **Proxy → HTTP history**
3. Locate the POST request to:
/process_checkout

4. Right-click → **Send to Repeater**

---

### Step 2: Prepare Parallel Requests

1. Go to the **Repeater** tab  
2. Right-click the request tab → **Add tab to group**
3. Create a group named:
cart

4. Right-click the request tab → **Duplicate tab**
5. Create **15 copies**

---

### Step 3: Send Requests in Parallel

1. In Repeater, click **Send dropdown**
2. Select:

4. Right-click the request tab → **Duplicate tab**
5. Create **15 copies**

---

### Step 3: Send Requests in Parallel

1. In Repeater, click **Send dropdown**
2. Select:
Send group in parallel (last-byte sync)

3. Click **Send group (parallel)**

This fires all requests simultaneously, maximising timing overlap.

---

## 🧾 Results

After sending parallel requests:
- Multiple orders succeed
- Stock is oversold
- Inventory may become **negative**

Revisit the web app to confirm:
- Multiple confirmed orders
- Stock inconsistency

---

## 🛡️ Mitigation Techniques

To prevent race condition vulnerabilities:

- Use **atomic database transactions**
- Validate stock **right before commit**
- Implement **idempotency keys**
- Apply **rate limiting**
- Enforce **concurrency controls**

Race conditions are not about hacking faster — they exploit **poor synchronisation**.

---

## 🏁 Final Answers / Flags

### SleighToy Limited Edition Flag
THM{WINNER_OF_R@CE007}

---

### Bunny Plush (Blue) Flag
THM{WINNER_OF_Bunny_R@ce}

---

## 🎯 Learning Objectives Achieved

- Identified race condition vulnerabilities  
- Exploited concurrent request handling flaws  
- Used Burp Suite Repeater effectively  
- Understood real-world impacts of race conditions  
- Learned mitigation strategies for developers  

---

## 📘 What I Learned Today

> “Milliseconds matter — and attackers know exactly how to use them.”

---

## 🔜 Next Step

Proceed to **Day 21** of Advent of Cyber 2025.

