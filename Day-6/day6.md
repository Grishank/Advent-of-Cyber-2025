# 🎄 Advent of Cyber 2025 — Day 6  
<img src="./images/day6-banner.png" width="900"/>

**Title:** Malware Analysis — Egg-xecutable  
**Date Completed:** Dec 2025  
**Difficulty:** Medium  
**Category:** Malware Analysis, Static & Dynamic Analysis  
**Room Link:** [Malware Analysis — Egg-xecutable](https://tryhackme.com/room/malware-sandbox-aoc2025-SD1zn4fZQt)        
**Status:** ✔ Completed  

---

## 🧭 Overview  
While Wareville sleeps, the SOC at The Best Festival Company (TBFC) receives a suspicious 3AM email from *Elf McClause* containing an executable named **HopHelper.exe**.  
Elf McBlue, experienced in malware investigation, takes charge and begins a full analysis of the file using static and dynamic techniques.

Today’s room explores the fundamentals of **malware analysis**, including sandboxes, safe execution, and tools like **PeStudio, Regshot, and ProcMon**.

---

# 🧩 Task-by-Task Write-Up

---

## **📝 Task 1 — Principles of Malware Analysis**  
Malware analysis helps investigators determine:

- What a malicious file does  
- What systems it interacts with  
- What persistence mechanisms it uses  
- What network communication it attempts  

Two main branches exist:

### **Static Analysis**
Examining the sample *without executing it*.  
Useful for collecting:
- Checksums  
- Strings  
- Imports  
- Resources  

### **Dynamic Analysis**
Executing the malware in a sandbox to observe:
- Registry changes  
- File modifications  
- Network calls  
- Persistence mechanisms  

Never run malware on a real machine — **always use isolated VMs**.

---

## **🧪 Task 2 — Static Analysis with PeStudio**

The HopHelper.exe sample is located in:

```
Desktop/HopHelper/
```

### **1. SHA256 Checksum**
Using PeStudio, we extracted the SHA256:

```
F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33
```

Checksums help analysts identify malware variants and match them with threat intelligence databases.

### **2. Suspicious Strings**
Scrolling through the strings revealed a hidden flag:

```
THM{STRINGS_FOUND}
```

Strings often reveal:
- C2 IPs  
- Malware commands  
- Credentials  
- Hard-coded paths  

---

## **🧪 Task 3 — Dynamic Analysis with Regshot**

### **Registry Persistence**
Regshot was used to take:
- Snapshot **before** execution  
- Snapshot **after** execution  

Comparing them revealed a persistence mechanism:

```
HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper
```

This means the malware ensures it runs at startup by modifying Run keys.

---

## **🛠 Task 4 — Dynamic Analysis with ProcMon**

Using Process Monitor:

1. We executed HopHelper.exe  
2. Captured system interactions  
3. Filtered events by:
   - Process Name = HopHelper.exe  
   - Operation contains "TCP"

This showed the malware communicating using:

```
http
```

Even simple protocols can indicate potential C2 communication.

---

# 📘 Flag Answers

### **Static Analysis: SHA256**
```
F29C270068F865EF4A747E2683BFA07667BF64E768B38FBB9A2750A3D879CA33
```

### **Static Strings Flag**
```
THM{STRINGS_FOUND}
```

### **Dynamic Analysis: Persistence Registry Key**
```
HKU\S-1-5-21-1966530601-3185510712-10604624-1008\Software\Microsoft\Windows\CurrentVersion\Run\HopHelper
```

### **Dynamic Analysis: Network Protocol**
```
http
```

---

# 🎯 Learning Objectives  
- Understand static vs. dynamic malware analysis  
- Use sandboxes to safely run unknown executables  
- Identify suspicious strings, imports, and metadata  
- Detect persistence via Windows Registry  
- Capture malware network behavior with ProcMon  

---

# 📘 What I Learned Today  
- Static analysis reveals quick intel (strings, hashes)  
- Dynamic analysis exposes real behavior (registry, network)  
- Malware often leverages Run keys for persistence  
- Process Monitor is a powerful digital microscope  
- Sandboxing is mandatory for safe investigation  

---

# 🧠 Key Takeaway  
> “Malware analysis turns fear into clarity — observe, analyze, and defend.”

---

# 🔜 Next Step  
Proceed to **Day 7** of Advent of Cyber 2025.


