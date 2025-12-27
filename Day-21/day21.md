# 🎄 Advent of Cyber 2025 — Day 21  
<img src="./images/day21-banner.png" width="900"/>

**Title:** Malware Analysis - Malhare.exe                                   
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Malware Analysis, HTA, Blue Team  
**Room Link:** [Malware Analysis - Malhare.exe](https://tryhackme.com/room/htapowershell-aoc2025-p2l5k8j1h4)  
**Status:** ✔ Completed  

---

## 🧭 Overview  

In Wareville, thousands of files pass through TBFC systems every day — resumes, PDFs, spreadsheets, scripts, and executables.  
Some are legitimate. Others belong to **King Malhare**.

This task focused on a **dangerous but often overlooked file type**: **HTA (HTML Application)**.  
While commonly used for internal automation, HTAs are also heavily abused by attackers for **initial access, payload delivery, and data exfiltration**.

Our mission was to **reverse-engineer a malicious HTA file**, uncover how it tricked TBFC’s elves, and identify exactly what data was stolen.

---

## 🎯 Learning Objectives

- Understand what **HTA files** are and why they exist  
- Learn how attackers abuse HTAs  
- Identify malicious behaviour inside HTA scripts  
- Detect encoded data and network activity  
- Uncover data exfiltration techniques  

---

## 🧠 HTA Overview

HTA stands for **HTML Application**.

An HTA is:
- Built with **HTML, CSS, and JavaScript/VBScript**
- Executed by **mshta.exe**
- Runs as a **desktop application**, not inside a browser

Legitimate uses include:
- Administrative automation
- Internal utilities
- Setup scripts
- Lightweight support tools

However, because HTAs execute code natively, attackers frequently weaponise them.

---

## 🧱 HTA File Structure

A typical HTA contains:

1. **HTA Declaration**  
   Defines application properties (title, window behaviour)

2. **Interface (HTML/CSS)**  
   What the user sees

3. **Script (VBScript / JavaScript)**  
   Logic and actions performed by the application

### Example of a Legitimate HTA
``html
<html>
<head>
    <title>TBFC Utility Tool</title>
    <HTA:APPLICATION 
        ID="TBFCApp"
        APPLICATIONNAME="Utility Tool"
        BORDER="thin"
        CAPTION="yes"
        SHOWINTASKBAR="yes"
    />
</head>

<body>
    <h3>Welcome to the TBFC Utility Tool</h3>
    <input type="button" value="Say Hello" onclick="MsgBox('Hello from Wareville!')">
</body>
</html>

---
## 🧨 How King Malhare Weaponises HTAs

Malicious HTAs are commonly used for:
Initial access (phishing attachments)
Droppers / downloaders
Obfuscation and evasion
Living-off-the-land execution

Common characteristics:
Executed via mshta.exe
Calls built-in tools like powershell.exe, wscript.exe
Uses encoded payloads (Base64, ROT)
Executes downloaded code in memory

---
## 🔍 Analysing a Malicious HTA

Key indicators to inspect:

1. HTA metadata
Check <title> and <HTA:APPLICATION> for social engineering
2. VBScript section
<scrip language="VBScript">

3. Encoded data
Base64 strings
External URLs

4. Execution flow
Variables passed into Run, Execute, or Eval 

---
## 🧪 From Surveys to Security Failures

Multiple elves reported compromised laptops.
The common factor was an email survey attachment.

File location on AttackBox:
/root/Rooms/AoC2025/Day21/survey.hta

To safely inspect:
pluma /root/Rooms/AoC2025/Day21/survey.hta

---
## 🧩 Function Analysis

The HTA contained five VBScript functions:

window_onLoad
Automatically executes on load

getQuestions
Downloads survey questions (but actually executes code)

provideFeedback(feedbackString)
Collects system information and sends it externally

decodeBase64(base64)
Decodes Base64 data

RSBinaryToString(xBinary)
Converts binary data to string

---
## ⚙️ Suspicious Objects Used

The HTA creates several dangerous objects:

InternetExplorer.Application
→ External connections

WScript.Network
→ System enumeration

WScript.Shell
→ Command execution

---
## 🧠 Social Engineering in Code

The survey:

Looks legitimate
Contains real-looking questions
Promises incentives
Uses typosquatted domains
This builds trust before executing malware.

---
## 🧪 Decoding the Payload

The downloaded content:
Was Base64 encoded
Further obfuscated using ROT13
Decoding revealed the final malicious payload.

---
## 🏁 Answers / Flags

HTA Application Title
Best Festival Company Developer Survey

VBScript Function Downloading Questions
getQuestions

Domain Hosting Questions
survey.bestfestiivalcompany.com

Typosquatting Character
i

Number of Survey Questions
4

Promised Prize Location
South Pole

Exfiltrated Host Information
ComputerName,UserName

Exfiltration Endpoint
/details

HTTP Method Used
GET

Code Executing Downloaded Content
runObject.Run "powershell.exe -nop -w hidden -c " & feedbackString, 0, False

Obfuscation Encoding Used
base64

Encryption Scheme Used
rot13

Final Flag
THM{Malware.Analysed}

---
## 🎯 Learning Objectives Achieved

Identified malicious HTA structure
Traced VBScript execution flow
Detected encoded payloads
Uncovered data exfiltration
Understood HTA-based social engineering

---
## 📘 What I Learned Today

“Malware doesn’t always look dangerous — sometimes it looks like a survey.”

---
## 🔜 Next Step

Proceed to Day 22 of Advent of Cyber 2025.



