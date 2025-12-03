# 🎄 Advent of Cyber 2025 — Day 3  
<img src="./images/day3-banner.png" width="900"/>

**Title:** Splunk Basics — Did You SIEM?  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** SIEM, Log Analysis, Splunk  
**Room Link:** [Splunk Basics - Did you SIEM?](https://tryhackme.com/room/splunkforloganalysis-aoc2025-x8fj2k4rqp)          
**Status:** ✔ Completed  

---

## 🧭 Overview  
Christmas preparations are in full swing in Wareville — until the SOC dashboard suddenly flashes **red**.  
A ransom note from **King Malhare**, ruler of HopSec Island, appears on the screen. His Bandit Bunnies have launched an attack to sabotage TBFC’s systems and replace Christmas with *EAST-mas*.

With McSkidy missing and the network compromised, the TBFC SOC team turns to **Splunk** to investigate the intrusion, identify the attack vector, and understand how the ransomware infiltrated the system.

This challenge focuses on learning core Splunk investigation skills vital for any SOC analyst.

---

# 🧩 Task-by-Task Write-Up

---

## **📝 Task 1 — Exploring the Logs in Splunk**  
The Splunk environment already contains pre-ingested logs for investigation.

Steps performed:
- Opened **Search & Reporting**
- Used `index=main` to list all logs
- Changed the timeframe to **All Time**
- Identified two data sources:
  - **web_traffic** (web server logs)
  - **firewall_logs** (network filtering logs)

This establishes the baseline dataset for our incident triage.

---

## **📊 Task 2 — Visualizing Log Activity**  
Using SPL (Search Processing Language), event volume was charted using:

```
timechart span=1d count
```

This showed:
- Normal activity on most days  
- A *massive spike* on the day of the attack — clear indication of malicious activity  

This timeline helped narrow down the attack window.

---

## **🕵️ Task 3 — Detecting Anomalies**  
Key fields were inspected:

### **🔹 User Agents**
Most logs showed normal browsers like Mozilla, Chrome, Firefox.  
However, a large cluster of **suspicious user agents** stood out — likely automated tools.

### **🔹 Client IP**
One attacker IP appeared repeatedly, responsible for most suspicious activity.

### **🔹 Path**
Malicious paths such as:
- configuration file probes  
- traversal attempts  
- payload requests  
were visible.

These indicators pointed directly toward the attacker's footprint.

---

## **🧹 Task 4 — Filtering Out Noise**  
Filtered legitimate traffic using SPL to isolate suspicious events.

After excluding common browsers, **only the attacker’s activity remained**, confirming:
- single malicious IP  
- heavy scanning  
- scripted requests  

This allowed focusing solely on the malicious footprints.

---

## **🔍 Task 5 — Tracing the Attack Chain**  

Splunk queries were used (summarized, no spoilers) to confirm each phase:

### **1️⃣ Reconnaissance**  
The attacker probed sensitive files and misconfigurations.  
Tools like **curl** and **wget** were used — confirming automated scanning.

### **2️⃣ Enumeration**  
Path traversal & open redirect attempts were visible.  
These indicated the attacker was testing for deeper access.

### **3️⃣ SQL Injection Attempts**  
Presence of:
- `sqlmap`
- injectable payloads  
- time-based injection patterns  

confirmed active exploitation.

### **4️⃣ Exfiltration Attempts**  
Attacker attempted to download:
- backups  
- logs  
- large archive files  

This suggests data theft as part of a double-extortion model.

### **5️⃣ Ransomware Execution (RCE)**  
The logs showed execution of:
- a malicious **webshell**
- a ransomware binary (`bunnylock.bin`)

This confirmed full remote code execution and compromise of the web server.

### **6️⃣ C2 Communication (Firewall Logs)**  
Firewall logs showed:
- outbound connection  
- from the compromised server (10.10.1.5)  
- to the attacker’s IP  
- with C2-related activity  

This validated command-and-control behavior.

---

# 🎯 Learning Objectives  
- Ingest & analyze logs in Splunk  
- Create & apply field extractions  
- Use SPL to filter & investigate logs  
- Identify attack patterns using real log data  
- Trace a full attacker kill-chain inside a SIEM  

---

# 📘 What I Learned Today  
- How Splunk structures data (indexes, sourcetypes, fields)  
- How to perform initial triage using `index=main`  
- Identifying anomalies through user agents, paths, and IPs  
- Conducting SOC-style investigations using SPL  
- Mapping attacker behavior across reconnaissance → exfiltration → RCE → C2  
- Why SIEM is critical for modern incident response  

---

# 🧠 Key Takeaway  
> “A SIEM is only as powerful as the analyst behind it — SPL turns raw logs into real intelligence.”

---

# 🔜 Next Step  
Proceed to **Day 4** of Advent of Cyber 2025.


