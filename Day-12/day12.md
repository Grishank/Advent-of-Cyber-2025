# 🎄 Advent of Cyber 2025 — Day 12  
<img src="./images/day12-banner.png" width="900"/>

**Title:** Phishing - Phishmas Greetings 
**Date Completed:** Dec 2025  
**Difficulty:** Easy–Medium  
**Category:** Phishing, Email Security, Social Engineering  
**Room Link:** [Phishing - Phishmas Greetings](https://tryhackme.com/room/spottingphishing-aoc2025-r2g4f6s8l0)  
**Status:** ✔ Completed  

---

## 🧭 Overview  
With McSkidy missing and the **Email Protection Platform offline**, TBFC staff must manually triage every suspicious email.  
Malhare’s **Eggsploit Bunnies** are actively launching phishing campaigns to steal credentials and disrupt SOC-mas.

In this task, I joined the **Incident Response Task Force** to identify phishing attempts, distinguish spam from phishing, and recognise modern attacker techniques.

---

# 🧩 Task-by-Task Write-Up

---

## **📧 Task 1 — Phishing Fundamentals**
Phishing is still one of the **most effective initial access techniques**, targeting people instead of technology.

### Common phishing goals:
- Credential theft  
- Malware delivery  
- Data exfiltration  
- Financial fraud  

Attackers now focus on **precision & persuasion**, often impersonating internal departments or trusted services.

---

## **📨 Task 2 — Spam vs Phishing**
Not every unwanted email is malicious.

### Spam:
- Bulk messages  
- Marketing, promotions, clickbait  
- Usually harmless noise  

### Phishing:
- Targeted deception  
- Designed to trick users  
- Clear malicious intent  

Key lesson: **Analyse intent, not annoyance.**

---

## **🎭 Task 3 — Impersonation & Social Engineering**

### Impersonation
Attackers pretend to be:
- Managers  
- IT departments  
- Internal services  

Red flag:
- Sender domain does not match the company’s official domain.

### Social Engineering Techniques Observed:
- Urgency (“URGENT”, “IMMEDIATELY”)  
- Authority impersonation  
- Side-channel pressure (avoid normal communication paths)  
- Requests for credentials or sensitive actions  

---

## **🔠 Task 4 — Typosquatting & Punycode**

### Typosquatting
- Look-alike domains (e.g. `glthub.com` vs `github.com`)

### Punycode
- Unicode characters replacing Latin letters  
- Domains visually identical but technically different  

Detection tip:
- Check **Return-Path** and email headers for `xn--` encoded domains.

---

## **📬 Task 5 — Email Spoofing**
Spoofed emails appear legitimate but fail authentication.

Key indicators:
- SPF failure  
- DKIM failure  
- DMARC failure  
- Mismatched Return-Path  

If **SPF + DKIM + DMARC fail**, spoofing is almost certain.

---

## **📎 Task 6 — Malicious Attachments**
Classic phishing still works.

Observed:
- HTML / HTA attachments  
- Fake voice messages  
- Files executing outside browser sandbox  

These attachments can:
- Steal credentials  
- Execute scripts  
- Deliver malware  

---

## **📈 Task 7 — Trending Phishing Techniques**

Modern attackers:
- Avoid obvious malware attachments  
- Use **legitimate services** (OneDrive, Google Docs, Dropbox)  
- Redirect users to:
  - Fake login pages  
  - Credential harvesting portals  

### Fake Login Pages
- Common targets: Microsoft 365, Google  
- Look-alike domains  
- Pixel-perfect clones  

### Side-Channel Attacks
- Move conversation to WhatsApp, SMS, calls  
- Escape company monitoring & controls  

---

## **🛡 Task 8 — Incident Response: Email Triage**
My task:
- Classify emails as **phishing or spam**
- Identify **at least 3 indicators** per phishing email
- Collect flags for correct classification

---

# 🏁 Final Answers / Flags

**Email 1 Flag:**  
THM{yougotnumber1-keep-it-going}

**Email 2 Flag:**  
THM{nmumber2-was-not-tha-thard!}

**Email 3 Flag:**  
THM{Impersonation-is-areal-thing-keepIt}

**Email 4 Flag:**  
THM{Get-back-SOC-mas!!}

**Email 5 Flag:**  
THM{It-was-just-a-sp4m!!}

**Email 6 Flag:**  
THM{number6-is-the-last-one!-DX!}

---

# 🎯 Learning Objectives Achieved
- Identified phishing vs spam accurately  
- Recognised modern phishing techniques  
- Analysed impersonation, spoofing & social engineering  
- Understood typosquatting & punycode abuse  
- Practised real-world email triage  

---

# 📘 What I Learned Today  
> “Most breaches don’t start with malware — they start with a convincing email.”

---

# 🔜 Next Step  
Proceed to **Day 13** of Advent of Cyber 2025.













