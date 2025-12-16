# 🎄 Advent of Cyber 2025 — Day 15  
<img src="./images/day15-banner.png" width="900"/>

**Title:** Splunk — Web Attack Forensics - Drone Alone 
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Blue Team, SIEM, Splunk, Incident Investigation  
**Room Link:** [Web Attack Forensics - Drone Alone](https://tryhackme.com/room/webattackforensics-aoc2025-b4t7c1d5f8)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

TBFC’s drone scheduler web UI began receiving **unusually long HTTP requests** containing Base64-encoded payloads.  
Splunk raised an alert indicating that **Apache spawned an unusual process**, suggesting possible command injection.

Some of these requests caused the web server to execute **obfuscated shell code**, hidden inside Base64 payloads.

As a **Blue Team analyst**, the objective was to:
- Triage the incident
- Identify compromised systems
- Decode attacker payloads
- Reconstruct the full attack chain using Splunk

---

## 🎯 Learning Objectives

- Detect malicious web activity using **Apache access and error logs**
- Investigate attacker actions using **Sysmon telemetry**
- Identify and decode **Base64-encoded payloads**
- Reconstruct an attack timeline using **Splunk**

---

## 🔐 Logging into Splunk

After starting the AttackBox and target machine, Splunk was accessed via browser.

**Splunk Access Details:**
- URL: `http://10.49.183.229:8000`
- Username: `Blue`
- Password: `Pass1234`

After logging in, the **Search Dashboard** was used.

⚠️ Important:  
The Splunk **time range** was adjusted to **Last 7 days / All time** to ensure events were visible.

---

## 🔍 Detect Suspicious Web Commands

The first step was identifying suspicious HTTP requests that may indicate **command injection**.

### Splunk Query
spl
index=windows_apache_access (cmd.exe OR powershell OR "powershell.exe" OR "Invoke-Expression")
| table _time host clientip uri_path uri_query status

### This query searches Apache access logs for:

- cmd.exe

- powershell

- Invoke-Expression

These are common indicators of command execution attempts via web requests.
---

## 🔐 Decoding Base64 Payloads

Encoded PowerShell commands were identified in the logs.

Example Encoded String
- VABoAGkAcwAgAGkAcwAgAG4AbwB3ACAATQBpAG4AZQAhACAATQBVAEEASABBAEEASABBAEEA

The string was decoded using:

- https://www.base64decode.org/

This revealed the attacker’s hidden command.
---

### 🧾 Inspect Apache Error Logs

To verify if the attack reached the backend, Apache error logs were examined.

Splunk Query
- index=windows_apache_error ("cmd.exe" OR "powershell" OR "Internal Server Error")
  
The Raw view was enabled to inspect full error messages.

A 500 Internal Server Error triggered by requests like:
- /cgi-bin/hello.bat?cmd=powershell

indicates the server attempted to process the malicious input.
---

### 🧠 Trace Suspicious Process Creation

Next, Sysmon logs were analyzed to identify processes spawned by Apache.

Splunk Query
- index=windows_sysmon ParentImage="*httpd.exe"

Apache should not spawn system-level processes.

Finding child processes such as:

- cmd.exe

- powershell.exe

confirms a successful command injection reaching the OS.
---

### 🕵️ Confirm Attacker Reconnaissance

Attackers often run reconnaissance commands after gaining execution.

Splunk Query
- index=windows_sysmon *cmd.exe* *whoami*

The whoami command confirms:

- Code execution success

- Attacker checking privilege level
---

### 🧪 Identify Base64 PowerShell Payloads

Finally, Sysmon logs were searched for encoded PowerShell commands.

Splunk Query
- index=windows_sysmon Image="*powershell.exe"
(CommandLine="*enc*" OR CommandLine="*-EncodedCommand*" OR CommandLine="*Base64*")

This detects:

- -EncodedCommand

- Base64 obfuscation techniques

In this scenario, no successful execution was found, indicating defenses prevented payload execution.
---

### 🏁 Final Answers / Flags

What is the reconnaissance executable file name?
- whoami.exe

What executable did the attacker attempt to run through command injection?
- powershell.exe
---

### 🎯 Learning Objectives Achieved

- Detected command injection via Apache logs

- Correlated web activity with Sysmon telemetry

- Decoded Base64 attacker payloads

- Identified post-exploitation reconnaissance

- Reconstructed a full attack chain using Splunk
---

### 📘 What I Learned Today

- “SIEM is not about alerts — it’s about connecting small clues into a complete story.”
---

### 🔜 Next Step

Proceed to Day 16 of Advent of Cyber 2025.

