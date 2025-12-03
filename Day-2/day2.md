# 🎄 Advent of Cyber 2025 — Day 2  
<img src="./images/day2-banner.png" width="900"/>

**Title:** Social Engineering & Phishing — Building the Perfect Trap  
**Date Completed:** Dec 2025  
**Difficulty:** Easy  
**Category:** Social Engineering, Phishing, Red Team  
**Room Link:** [Phishing - Merry Clickmas](https://tryhackme.com/room/phishing-aoc2025-h2tkye9fzU)                           
**Status:** ✔ Completed  

---

## 🧭 Overview  
Due to several recent cyber incidents targeting **The Best Festival Company (TBFC)**, the local red team has scheduled a series of penetration tests. This includes assessing how well employees respond to **phishing attacks**, one of the most common and dangerous social engineering tactics.

Today, I join the red team elves — **Recon McRed, Exploit McRed, and Pivot McRed** — to help plan and execute an authorised phishing campaign.  
The purpose: test if TBFC employees are following their cyber security awareness training.

This task teaches how attackers craft convincing phishing pages, host them, and deliver them using specialized tools like **SET (Social-Engineer Toolkit)**.

---

# 🧩 Task-by-Task Write-Up

---

## **📝 Task 1 — Understanding Social Engineering**
**Social engineering** is the act of manipulating people into making mistakes.  
Attackers exploit human psychology using emotions like:
- urgency  
- curiosity  
- authority  

This is why social engineering is often called **“human hacking.”**

**Illustration:**  
Three red-clad elves stand in a snowy forest.  
- One holds a fishing rod  
- One carries a satchel  
- One holds two fish  
Symbolizing *phishing* — catching victims.

---

## **🐟 Task 2 — Phishing Basics**
Phishing is a *subset* of social engineering using messages such as:
- emails  
- SMS (smishing)  
- voice calls (vishing)  
- QR codes (quishing)  
- social media DMs  

TBFC teaches two versions of **S.T.O.P.** to avoid phishing:

### **S.T.O.P. (All Things Secured)**
- **S**uspicious?  
- **T**elling me to click?  
- **O**ffering an amazing deal?  
- **P**ushing urgency?

### **S.T.O.P. (TBFC internal)**
- **S**low down  
- **T**ype the address manually  
- **O**pen nothing unexpected  
- **P**rove the sender identity  

After many training sessions, it’s time to test if employees learned anything.

---

## **🎣 Task 3 — Building the Trap**
Our objective:  
**Steal credentials using a fake TBFC login page.**

Attack process:
1. Host a fake login page  
2. Capture the credentials entered by the target  
3. Email the link to the target using a realistic sender profile  

A script is already placed at:

```
~/Rooms/AoC2025/Day02
```

Run it using:

```
./server.py
```

You’ll see:

```
Starting server on http://0.0.0.0:8000
```

This means:
- The phishing server is active
- Bound to all interfaces
- Listening on port 8000

Preview the fake page from the AttackBox:

- http://127.0.0.1:8000  
- http://CONNECTION_IP:8000  

---

## **📨 Task 4 — Sending the Phishing Email (SET Toolkit)**
Using **SET (Social-Engineer Toolkit)**, we craft and send a realistic phishing email.

Start SET:

```
setoolkit
```

Choose:
```
1) Social-Engineering Attacks
5) Mass Mailer Attack
1) E-Mail Attack Single Email Address
```

Then configure the phishing email:

- **Target:** factory@wareville.thm  
- **Delivery method:** Use your own server  
- **From address:** updates@flyingdeer.thm  
- **From name:** Flying Deer  
- **SMTP server:** MACHINE_IP  
- **Port:** 25  
- **Subject:** Shipping Schedule Changes  

Email body must include:

```
http://CONNECTION_IP:8000
```

The toolkit sends the email.  
Then you monitor the `server.py` terminal to check if any credentials are entered.

---

## **🚨 Task 5 — Results**
After a short wait, the red team receives *working login credentials* from at least one victim — meaning the phishing attempt succeeded.

This outcome is alarming because:
- An attacker could steal credentials the same way  
- They could access TBFC systems  
- The entire gift delivery system could be compromised  

Immediate investigation is required.

---

# 🎯 Learning Objectives
- Understand **social engineering**  
- Learn the common **types of phishing**  
- Discover how attackers build **fake login pages**  
- Use SET to create and deliver phishing emails  

---

# 📘 What I Learned Today
- How attackers exploit psychological weaknesses  
- How phishing campaigns are structured  
- How login pages can be cloned and hosted  
- How SET automates crafting and sending phishing emails  
- How real organisations test employee awareness  

---

# 🧠 Key Takeaway
> “The weakest link in security is always the human — not the machine.”

---

# 🔜 Next Step  
Proceed to **Day 3** of Advent of Cyber 2025.

