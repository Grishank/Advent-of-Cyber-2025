# 🎄 Advent of Cyber 2025 — Day 11  
<img src="./images/day11-banner.png" width="900"/>

**Title:** XSS - Merry XSSMas                  
**Date Completed:** Dec 2025     
**Difficulty:** Easy  
**Category:** Web Exploitation, XSS  
**Room Link:** [XSS - Merry XSSMas](https://tryhackme.com/room/xss-aoc2025-c5j8b1m4t6)                                 
**Status:** ✔ Completed  

---

## 🧭 Overview  
McSkidy’s secure message portal is acting strange — suspicious inputs, odd logs, and even Santa’s letters look like code.  
Today’s mission: **Understand and exploit XSS vulnerabilities (Reflected & Stored)** and uncover who’s messing with the portal.

---

# 🧩 Task-by-Task Write-Up

---

## 📝 Task 1 — What is XSS?

**Cross-Site Scripting (XSS)** allows attackers to inject malicious JavaScript into webpages viewed by other users.  
When user input is not sanitized, browsers execute it as code.

Two vulnerabilities covered today:

### **Reflected XSS**
- Payload is reflected immediately in server response.  
- Often delivered via malicious links (phishing).  
- Executes once per request.

Example:
```
<script>alert('XSS')</script>
```

---

### **Stored XSS**
- Payload is **saved on the backend** (DB, file, or server memory).  
- Every user who loads the page triggers the attacker’s script.  
- Much more dangerous.

Example:
```
<script>alert('Stored XSS')</script>
```

---

## 🛡 Preventing XSS
Key defences:

- **Use textContent instead of innerHTML**  
- **Sanitize & encode inputs**  
- **Set cookies as HttpOnly, Secure, SameSite**  
- **Never trust user-controlled data**

---

# 🔎 Task 2 — Exploiting Reflected XSS

Using the search feature on the portal:

Payload used:
```
<script>alert('Reflected Meow Meow')</script>
```

Steps:
1. Enter payload into **Search Messages**  
2. Alert appears → confirms **Reflected XSS**  
3. System Logs confirm payload reflection

Flag revealed:
```
THM{Evil_Bunny}
```

---

# 🐾 Task 3 — Exploiting Stored XSS

Stored XSS happens inside **Send Message** — messages persist on backend.

Payload:
```
<script>alert('Stored Meow Meow')</script>
```

Steps:
1. Submit the message  
2. Reload page → alert triggers every time  
3. Confirms **Stored XSS** vulnerability

Flag revealed:
```
THM{Evil_Stored_Egg}
```

---

# 🏁 Final Answers / Flags

**Q: Which type of XSS requires payloads to be persisted on the backend?**  
```
stored
```

**Q: What’s the reflected XSS flag?**  
```
THM{Evil_Bunny}
```

**Q: What’s the stored XSS flag?**  
```
THM{Evil_Stored_Egg}
```

---

# 🎯 Learning Objectives Achieved
- Difference between Reflected vs Stored XSS  
- How user input becomes executable code  
- How to exploit XSS on real applications  
- Core XSS mitigation strategies  

---

# 📘 What I Learned Today  
> “XSS proves that even a tiny text box can become a full attack surface.”

---

# 🔜 Next Step  
Proceed to **Day 12** of Advent of Cyber 2025.

