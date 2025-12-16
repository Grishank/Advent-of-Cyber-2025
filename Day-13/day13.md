# 🎄 Advent of Cyber 2025 — Day 13  
<img src="./images/day13-banner.png" width="900"/>

**Title:** YARA Rules - YARA mean one!  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Malware Detection, Threat Hunting, YARA  
**Room Link:** [YARA Rules - YARA mean one!](https://tryhackme.com/room/yara-aoc2025-q9w1e3y5u7)  
**Status:** ✔ Completed  

---

## 🧭 Overview  
After McSkidy’s disappearance, TBFC’s blue team received a strange package: **a folder full of images** related to Easter preparations.  
Hidden inside these images was a **covert message** from McSkidy, embedded using a keyword and code words.

The mission was to **write a YARA rule** capable of detecting a specific keyword pattern across the image directory, extract the hidden codes, and **decode McSkidy’s message**.

---

# 🧩 Task-by-Task Write-Up

---

## **🛡 Task 1 — What is YARA?**
YARA is a powerful detection tool used to **identify malware and suspicious content** based on patterns rather than filenames or hashes.

Think of YARA as:
- A pattern-matching engine  
- A custom signature system for defenders  
- A core tool for threat hunting and post-incident analysis  

Common use cases:
- Threat hunting  
- Post-breach validation  
- Malware classification  
- Memory analysis  
- Intelligence-driven scans  

---

## **📌 Task 2 — Why YARA Matters**
YARA allows defenders to:
- Define **their own detection logic**
- Detect **new or modified malware**
- Share rules with the community
- Move from passive alerts to **active hunting**

Key advantages:
- Speed  
- Flexibility  
- Control  
- Reusability  
- Visibility  

---

## **🧱 Task 3 — Anatomy of a YARA Rule**
Every YARA rule is built from three core components:

### **Metadata**
Describes the rule (author, date, purpose).

### **Strings**
Indicators YARA looks for:
- Text  
- Hexadecimal byte patterns  
- Regular expressions  

### **Condition**
The logic deciding when a match occurs.

### Example Rule
yara
rule TBFC_KingMalhare_Trace
{
    meta:
        author = "Defender of SOC-mas"
        description = "Detects traces of King Malhare’s malware"
        date = "2025-10-10"

  strings:
        $s1 = "rundll32.exe" fullword ascii
        $s2 = "msvcrt.dll" wide
        $url = /http:\/\/.*malhare.*/ nocase

   condition:
        any of them
}

---
## **🔍 Task 4 — YARA Strings Deep Dive**
Text Strings
Simple and common text indicators.
They can be enhanced using modifiers.

### Modifiers used:

- nocase — Case-insensitive

- wide / ascii — Unicode & ASCII support

- xor — XOR-obfuscated strings

- base64 / base64wide — Encoded content

### Example
- $xmas = "Christmas" wide ascii nocase

### Hexadecimal Strings
Used to detect binary patterns, headers, or shellcode.

Example
- $mz = { 4D 5A }   // PE header
  
## Regular Expression Strings
Used for flexible matching such as:

- URLs

- Commands

- Variable filenames

---
## **🧠 Task 5 — Conditions Logic**

Conditions decide when a rule triggers.

### Common patterns

- $xmas
- any of them
- all of them
- ($s1 or $s2) and not $benign
- any of them and filesize < 700KB

## Conditions help:
- Reduce false positives

- Combine multiple indicators

- Filter by file properties

---

## **🧪 Task 6 — Practical Detection with YARA**
TBFC analysts created a YARA rule to detect IcedID-like loaders.

Key traits:
Small file size

MZ header

Known malicious fragments

### Example Rule

- rule TBFC_Simple_MZ_Detect
  {
    meta:
        author = "TBFC SOC L2"
        description = "IcedID Rule"
        date = "2025-10-10"

   strings:
        $mz   = { 4D 5A }
        $hex1 = { 48 8B ?? ?? 48 89 }
        $s1   = "malhare" nocase

   condition:
        all of them and filesize < 10485760
  }
- Execution
- yara -r icedid_starter.yar C:\

---
## **🧩 Task 7 — Hidden Message Challenge**
Goal
- Scan /home/ubuntu/Downloads/easter

- Detect strings starting with TBFC: followed by alphanumeric characters

- Extract and decode McSkidy’s message

## Regex Used
- /TBFC:[A-Za-z0-9]+/

---
  
### 🏁 Final Answers / Flags
- Images containing TBFC string:
- 5
## Regex used:
- /TBFC:[A-Za-z0-9]+/

## Decoded message from McSkidy:
- Find me in HopSec Island

---

  
## **🎯 Learning Objectives Achieved**
- Understood YARA fundamentals

- Learned when and why to use YARA

- Wrote effective YARA rules

- Used text, hex, and regex strings

- Applied YARA in a real investigation scenario

---  

### 📘 What I Learned Today
- “YARA turns scattered clues into certainty — it’s a defender’s scalpel, not a hammer.”

---

### 🔜 Next Step
- Proceed to Day 14 of Advent of Cyber 2025.












