# 🎄 Advent of Cyber 2025 — Day 5  
<img src="./images/day5-banner.png" width="900"/>

**Title:** IDOR — Santa’s Little IDOR  
**Date Completed:** Dec 2025  
**Difficulty:** Easy  
**Category:** Web Security, Access Control, IDOR  
**Room Link:** [IDOR - Santa's little IDOR](https://tryhackme.com/room/idor-aoc2025-zl6MywQid9)                                                                             
**Status:** ✔ Completed  

---

## 🧭 Overview  
The elves of Wareville are already stressed with McSkidy missing — and now the **TryPresentMe** website has become a hotspot for strange activity.

Parents are calling support:

- Gift vouchers aren’t activating  
- They’re receiving targeted phishing emails containing private info  
- A suspicious account named **Sir Carrotbane** held many stolen vouchers  

The TBFC staff removed the account, but something deeper is wrong.  
Today’s task focuses on investigating the website and uncovering a **web vulnerability known as IDOR**.

---

# 🧩 Task-by-Task Write-Up

---

## **📝 Task 1 — What is IDOR?**  
IDOR stands for **Insecure Direct Object Reference** — a form of **authorization bypass** where an attacker modifies an object identifier (like `user_id=10`) to access another user’s data.

Example:  
```
https://site.thm/TrackPackage?packageID=1001
```
Changing `1001 → 1002` may expose another user’s package details.

IDOR happens when:
- The server **trusts user input too much**  
- The server **does not check permissions** before returning data  

This allows attackers to:
- Access other users’ accounts  
- Steal sensitive information  
- Escalate privileges horizontally  

---

## **🔐 Task 2 — Authentication & Authorization (Why IDOR Happens)**  
To understand IDOR, we must understand:

### **Authentication**  
Verifying who you are (username + password → session token).

### **Authorization**  
Verifying what you are allowed to do (view only *your* account).

Important rules:
- Authorization **must** come after authentication  
- If a feature doesn’t require login → IDOR risk becomes huge  
- IDOR is usually **horizontal privilege escalation**  

---

## **🧪 Task 3 — Basic IDOR Exploitation (Changing user_id)**  
The user logs in with:

```
Username: niels  
Password: TryHackMe#2025  
Website: http://MACHINE_IP
```

Using DevTools:
- Open **Network** tab  
- Find the `view_accountinfo` request  
- Notice: `user_id: 10`

Then:
- Open **Application / Storage → Local Storage**
- Edit `auth_user` → change `"user_id": 10` to `"user_id": 11`
- Refresh the page

Suddenly, you’re logged in as a completely different user!

This demonstrates the simplest IDOR.

---

## **🕵️ Task 4 — Hidden IDORs (Encoded References)**  
Even when the value looks “hidden,” IDOR may still exist.

### Examples:

#### **Base64-encoded identifiers**  
Request shows:
```
child_id = Mg==
```
Which decodes to:
```
2
```
You can still perform IDOR by encoding another number into Base64.

#### **Hashed identifiers (MD5/SHA1)**  
When clicking “Edit Child,” the endpoint uses a hash:
```
/child/<md5hash>
```
If the hash is predictable, attackers can replicate it.

#### **Algorithm-based identifiers (UUID v1)**  
Voucher codes looked random, but UUID v1 is time-based.  
By knowing when vouchers were generated, an attacker could brute-force valid voucher UUIDs.

---

## **🔧 Task 5 — Fixing IDOR (Best Practices)**  

### 🛑 Don’ts:
- Don’t rely on Base64, hashing, or obscurity  
- Don’t trust user-supplied object IDs  
- Don’t skip authorization checks  

### 🟢 Do’s:
- Validate permissions **on every request**  
- Ensure the logged-in user *owns* the object they request  
- Use unpredictable identifiers (but not as a replacement for authorization)  
- Log failed access attempts  

The real fix: **server-side authorization checks**, not hiding the ID.

---

# 📘 Flag Answers

**Q1: What does IDOR stand for?**  
```
Insecure Direct Object Reference
```

**Q2: What type of privilege escalation are most IDOR cases?**  
```
Horizontal
```

**Q3: Exploiting the IDOR in view_accounts, what is the user_id with 10 children?**  
```
15
```

---

# 🎯 Learning Objectives  
- Understand authentication vs. authorization  
- Identify insecure direct object references  
- Practically exploit IDOR vulnerabilities  
- Learn how IDOR enables horizontal escalation  
- Learn how to turn IDOR → SDOR (Secure Direct Object Reference)  

---

# 📘 What I Learned Today  
- IDOR is extremely common and dangerous  
- Object references must always be validated server-side  
- Encoding or hashing does *not* prevent IDOR  
- Attackers can enumerate IDs, Base64 values, hashes, or UUIDs  
- Secure design involves robust authorization checks  

---

# 🧠 Key Takeaway  
> “If the server doesn’t verify who owns the data, an attacker will.”

---

# 🔜 Next Step  
Proceed to **Day 6** of Advent of Cyber 2025.

